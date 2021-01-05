# Search Queries

Below an overview of the search queries can be found. These queries were used to retrieve the dataset thar was both used in the offline and online evaluation of the study.


### Dataset
For the dataset only opinion pieces in Dutch were used. The choice of article type is motivated
by the focus group session presented in Section 3, in which the
structure of this article type is put forward as the primary heuristic
to find framing aspects. We picked topics that we expected a) to be
present on the Blendle platform at the time when we performed
the online user study; b) to contain different viewpoints addressed
in the news; and c) to balance issues that more current versus longstanding. The dataset consists of four ongoing topics: Black Lives
Matter, Coronavirus, U.S. Elections - as more current topics, and the
dominance and privacy issues around Big Tech - as a long-standing
topic.

We collected our dataset from an archive containing more than
5 million Dutch news articles. The archive is known to undergo
checks for articles quality, to remove undesirable content, such as
the weather or short actualities. For each topic, we used the search
terms (queries) and restrictions shown in Table 1. We provide the
list of search terms in their original language, Dutch, because we do
not want to add additional bias through translation. Additionally,
since the proposed method heavily relies on the structure of the
article, we set up a filter for the minimum number of words to 450
and a filter for the minimum number of paragraphs to 5

### Queries

| Topic        | Search Query           | Start Date  |
| ------------------ |---------------| ----- |
| Black Lives Matter | (’black lives matter’ OR ’racisme debat’ OR ’blm-demonstraties’ OR ’George Floyd’ OR ’racisme-debat’) AND NOT (’belastingdienst’ OR ’corona’) | June 15 2020 |
| Coronavirus        | ’corona’ OR ’covid-19’ OR ’mondkapjes’ OR ’mondkapje’ OR ’mondmasker’ OR ’mondkapjesplicht’ OR ’coronatest’ OR ’coronatesters’ OR ’rivm’ OR ’virus’ OR ’viroloog’ OR ’golf’ OR ’topviroloog’ OR ’uitbraak’ OR ’uitbraken’ OR ’coronaregels’ OR ’versoeplingen’ OR ’staatssteun’ OR ’vaccin’ | June 1 2020 |
| U.S. Elections     | ’Donald Trump’ AND (’presidentsverkiezingen’ OR ’Verkiezingen’ OR ’campagne’ OR ’verkiezingsstrijd’ OR ’verkiezingscampagne’ OR ’Joe biden’) | June 1 2020 |
| Big Tech           | (’macht’ OR ’machtig’ OR ’privacy’ OR ’data’ OR ’privacyonderzoek’ OR privacy-schandaal’) AND (’big tech’ OR ’tech-bedrijven’ OR techbedrijven’) | 2018 |



