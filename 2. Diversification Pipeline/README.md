# Introduction

### Pseudo-code walk-through
To provide more insight into the actual diversification algorithm, this jupyter notebook was set up. However, the actual algorithm used for the study highly depends on the Blendle enrichment proces and datastructure. Since this environment can not be shared publicly, sharing the actual code will not be benefitial. Therefore, it was chosen to create a pseudo-code walk-through of the algorith.

### Content

1. [Enrichments](#enrichment)
2. [Diversity Function](#Diversity-Functions)
3. [Reranking](#Re-ranking)

# Enrichment

```
x = number of assumed introduction paragraphs of article
y = number of assumed concluding paragraphs of article
```

### 1. Problem Definition
The pipeline below describes the enrichment process related to the problem defintion framing function.
* It is assumed that a trained topic-model is available.
* The methods returns the topic distribution over the x introduction paragraphs.

```
enrichmentPipeline = Pipeline('cleaner', 'tokenizer', 'stemmer', 'topic-model')

For article i in dataset:
   For first x paragraphs p in i:
       enrichmentPipeline.enrich(p)
       
   return topic-distribution over x introduction paragraphs

```

### 2. Causal Attribution
The pipeline below describes the enrichment process related to the causal attribution framing function.
* The method uses both the Google Translate API (could be neglected if articles are in supported languages) and IBM Watson API.
* The method returns the IBM watson category hierarchy for each body paragraph (https://cloud.ibm.com/apidocs/natural-language-understanding#categories).

```
enrichmentPipeline = Pipeline('googleTranslate', 'ibmWatson('categories')')

For article i in dataset:
   bodyParagraphs[] = i.paragraphs - x - y
   For paragraph p in bodyParagraph:
       enrichmentPipeline.enrich(p)
       
   return ibm_categories_hierarchy
```

### 3. Moral Evaluation
The pipeline below describes the enrichment process related to moral evaluation framing function. 
* The method uses both the Google Translate API (could be neglected if articles are in supported languages) and IBM Watson API.
* The method returns the IBM sentiment score for each body paragraph (https://cloud.ibm.com/apidocs/natural-language-understanding#sentiment).

```
enrichmentPipeline = Pipeline('googleTranslate', 'ibmWatson('sentiment')')

For article i in dataset:
   bodyParagraphs[] = i.paragraphs - x - y
   For paragraph p in bodyParagraph:
       enrichmentPipeline.enrich(p)
       
   return ibm_sentiment_score
```

### 4. Treatment Recommendations
The pipeline below describes the enrichment process related to treatment recommendation framing function.
* The method checks for each sentence in the concluding paragraphs if it contains a treatment recommendation
* If the sentence includes a treatment recommendation, the sentence is send to IBM Watson (categories)
* The methods returns the category hierarchy of the sentences with a treatment recommendation


```
keywords = ['suggest', 'recommend', 'hopefully', 'go for', 'request', 'it would be nice', 'adding', 'should come with', 'should be able', 'could come with', 'i need', 'we need', 'needs', 'needs to', 'need to', 'would like to', 'would','love to', 'i wish', 'i hope', 'i want', 'hopefully', 'if only', 'would be better if', 'would that', 'i can has','do want','should', 'there should be', 'i cannot', 'ability to','ability of']

modal_words = ['can', 'would', 'could', 'must', 'may', 'shall', 'might', 'should', 'will', 'ought to']

function checkSentence(sentence):
    for word w in sentence:
        if w in keywords:
            return true
        if (s[w].pos in ['NN','NNS','NNP','NNPS','PRP','PDT','DT'] && ] s[w+1].pos in ['VB','VBP']):
            return true
        if (s[w].lemma in modal_words && s[w+1].pos == 'VB'):
            return true
            
enrichmentPipeline_1 = Pipeline('googleTranslate', 'coreNLP('tokenize','ssplit','pos','depparse','parse','lemma')')
enrichmentPipeline_2 = Pipeline('ibmWatson('categories)')

    
For article i in Datasaet:
    For last y paragraphs p in i:
        enrichment = enrichmentPipeline_1.enrich(p)
            For sentence s in enrichment:
                if checkSentence(s):
                    enrichmentPipeline_2.enrich(p)
    return ibm_categories_hierarchy
```

# Diversity Functions

### Problem Definition
The following pseudo-code calculates the diversity score between two articles related to the problem definition framing function.
* The kullback leibler divergence between two topic distribution was used (assuming all probabililties are > 0)
* The method returns the kullback leibler divergence between all pairs of articles

```
For article i in dataset:
    For article j in [dataset - i]:
       return kl_Divergence(i, j)
```

### Causal Atrribution

The following pseudo-code calculates the diversity score between two articles related to the causal attribution framing function.
* The weighted jaccard index is calculated between the category arrays of all paragraphs combinations of two articles
* Two setups were used: equal contribution of each hierarchy level or increasing contribution for increasing hierarchy levels
* The method returns the mean jaccard index of all paragraph combinations of two articles (negative because jaccard returns similarity)

```
For article i in dataset:
    For article j in [dataset - i]:
       For all paragraph combinations s,t of i and j:
           jaccard[s,t] = weighted_jaccard_index(s.categories, t.categories)
    return -1 * mean(jaccard)
   
```

### Moral Evaluation
The following pseudo-code calculates the diversity score between two articles related to the moral evaluation framing function.
* The score of a combination of two paragaphs is calculated by the jaccard index of the parahraph combination times the absolute difference in ibm sentiment score (thus more overlapping paragrahs have a higher contribution)
* The method returns the mean sentiment score of each paragraph combination of two articles

```
For article i in dataset:
    For article j in [dataset - i]:
       For all paragraph combinations s,t of i and j:
           sentiment[s,t] = abs(sentiment(s) - sentiment(t)) * jaccard(s,t)
    return mean(sentiment)
   
```

### Treatment Recommendation

The following pseudo-code calculates the diversity score between two articles related to the treatment recommendation framing function.
* The weighted jaccard index is calculated between the category arrays of combinations of sentences in which a treatment recommendation was found
* Two setups were used: equal contribution of each hierarchy level or increasing contribution for increasing hierarchy levels
* The method returns the mean jaccard index over all sentence combinations (negative because jaccard returns similarity)

```
For article i in dataset:
    For article j in [dataset - i]:
       For all combinations of sentences with a treatment recommendation s,t of i and j:
           jaccard[s,t] = weighted_jaccard_index(s.categories, t.categories)
    return -1 * mean(jaccard)
   
```

# Re-ranking

```
weighfactors = [w1, w2, w3, w4]
d_1[i, j] = problem definition diversity score article i, j
d_2[i, j] = causal attribution diversity score article i, j
d_3[i, j] = moral evaluation diversity score article i, j
d_4[i, j] = treatment recommendation diversity score article i, j
   
```

### Normalize Diversity Scores + fill missing values

* First, the diversity matrices related to each framing function are normalized
* Afterwards, missing values (if for example no data was available for a framing function) are replaced by the mean of the matrix

```
min_max_normalize(d_1, d_2, d_3, d_4)

For article i in dataset:
   For article j in [dataset - i]:
       if d_x[i, j] == 0:
           d_x[i, j] = mean(d_x)

```

### Calculate Total Diversity Score
The method below calculates the total diversity score between two articles
* The sore is a simple weighted sum of the diversity scores related to each framing function

```
For article i in dataset:
    For article j in [dataset - i]:
       diversity[i,j] = (w1 * d_1[i,j]) + (w2 * d_2[i,j]) + (w3 * d_3[i,j]) + (w4 * d_4[i,j])
    
    return diversity
   
```

### Calculate Relevance Score
The method below calculates the relevance score between two articles
* The sore is implemented as a TF-IDF score between the content of both articles
* In the original method the sklearn TfidfVectorizer was used

```
For article i in dataset:
    For article j in [dataset - i]:
       relevance[i,j] = TF_IDF(i, j)
       
    return min_max_normalize(relevance)
   
```

### MMR
The method describes the MMR function
* The method outputs a list of recommendations of a certain size
* The variable λ includes the threshold between diversity and relevance

```
function getRecommendations(original_article, size, λ):
    article_choices = dataset = original_article
    output = []
    While output.length < size:
        For article i in article_choices:
            score[i] = (relevance[original_article, i] * λ) - ((1-λ) * diversity[original_article, i])
        recommendation = index(max(score))
        output.append(recommendation)
        article_choices = article_choices - recommendation

``` 
