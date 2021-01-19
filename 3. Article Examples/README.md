# Re-ranking Example

This page includes an example of the re-ranking algorithm. First, the details of the dataset are provided. Afterwards, the re-ranking table for different values of λ are presented. Finally, a side-by-side comparison of the content of two recommendation lists is included.

__Content:__
1. [Dataset](#dataset)
2. [Re-ranking table](#Re-ranking-table)
3. [Content Example](#content-example)

## Dataset
The following dataset was used in the example:
* __Dataset:__ Corona Virus (52 articles)
* __List size _s_:__ 3
* __Cross-validation _k_:__ 10-fold

Due to contractual limitations, we were not allowed to include all article data. Per article, the following information is included:
* Title of article
* First 75 words of article body
* Publisher ID of article 
* Link to article on Blendle (one needs a subscription to actually read the full article)

__This information can be found in json fromat in the subfolder called 'articles'.__

## Re-ranking table

The table below involves an example output of the re-ranking algorithm. For each article in the dataset, the algorithm composed a re-ranking of the remaining articles in the dataset. Both a re-ranking based purely on relevance (the baseline) and a re-ranking fully based on diversity (λ=0)  are included. The first 10 items in the re-ranking are shown. 

|Article ID|λ=0 (full relevance)|   λ=0.5    |λ=0 (full diversity)|
|---------:|--------------------|------------|--------------------|
|         0|[1, 37, 25]         |[2, 37, 36] |[39, 50, 18]        |
|         1|[15, 2, 20]         |[15, 2, 20] |[39, 7, 8]          |
|         2|[33, 1, 15]         |[33, 16, 15]|[7, 16, 42]         |
|         3|[5, 13, 10]         |[5, 0, 10]  |[39, 50, 0]         |
|         4|[12, 3, 51]         |[51, 37, 28]|[7, 37, 39]         |
|         5|[3, 25, 28]         |[3, 23, 28] |[39, 47, 37]        |
|         6|[8, 3, 5]           |[8, 5, 3]   |[39, 7, 47]         |
|         7|[13, 3, 26]         |[13, 10, 3] |[39, 50, 47]        |
|         8|[9, 51, 6]          |[9, 51, 6]  |[7, 39, 47]         |
|         9|[8, 10, 3]          |[8, 0, 10]  |[16, 47, 7]         |
|        10|[13, 5, 8]          |[13, 8, 3]  |[7, 47, 37]         |
|        11|[24, 3, 1]          |[1, 35, 47] |[39, 37, 51]        |
|        12|[22, 36, 28]        |[22, 28, 36]|[7, 39, 37]         |
|        13|[3, 41, 15]         |[51, 10, 3] |[39, 51, 37]        |
|        14|[16, 23, 36]        |[28, 36, 22]|[39, 7, 28]         |
|        15|[36, 1, 21]         |[1, 36, 2]  |[16, 39, 47]        |
|        16|[21, 15, 28]        |[15, 21, 28]|[7, 8, 47]          |
|        17|[24, 45, 3]         |[28, 3, 24] |[2, 34, 50]         |
|        18|[6, 13, 1]          |[6, 13, 51] |[2, 39, 50]         |
|        19|[28, 36, 2]         |[1, 22, 28] |[37, 7, 39]         |
|        20|[1, 15, 13]         |[1, 15, 13] |[7, 47, 39]         |
|        21|[36, 16, 15]        |[16, 36, 15]|[39, 7, 37]         |
|        22|[25, 12, 34]        |[25, 16, 34]|[47, 50, 39]        |
|        23|[28, 5, 14]         |[28, 5, 36] |[39, 7, 47]         |
|        24|[11, 29, 17]        |[2, 21, 29] |[39, 50, 47]        |
|        25|[22, 5, 1]          |[22, 1, 5]  |[7, 39, 37]         |
|        26|[3, 7, 6]           |[39, 6, 46] |[39, 37, 50]        |
|        27|[23, 1, 28]         |[23, 28, 22]|[7, 16, 46]         |
|        28|[33, 36, 16]        |[16, 37, 33]|[7, 47, 39]         |
|        29|[24, 1, 21]         |[2, 24, 21] |[39, 51, 47]        |
|        30|[43, 5, 50]         |[50, 28, 24]|[39, 37, 7]         |
|        31|[44, 36, 2]         |[44, 2, 15] |[39, 7, 37]         |
|        32|[5, 1, 36]          |[5, 36, 15] |[7, 42, 37]         |
|        33|[2, 28, 1]          |[2, 28, 37] |[7, 39, 37]         |
|        34|[2, 22, 21]         |[2, 22, 28] |[50, 0, 39]         |
|        35|[11, 4, 7]          |[11, 51, 7] |[50, 0, 39]         |
|        36|[15, 21, 43]        |[15, 21, 43]|[39, 7, 37]         |
|        37|[0, 28, 33]         |[28, 0, 22] |[19, 7, 39]         |
|        38|[21, 16, 33]        |[16, 21, 15]|[39, 7, 32]         |
|        39|[0, 1, 23]          |[0, 23, 42] |[51, 47, 46]        |
|        40|[13, 5, 8]          |[8, 22, 13] |[7, 39, 47]         |
|        41|[13, 14, 29]        |[13, 22, 18]|[7, 37, 39]         |
|        42|[41, 21, 39]        |[39, 21, 24]|[7, 32, 37]         |
|        43|[36, 21, 30]        |[36, 37, 21]|[35, 37, 39]        |
|        44|[31, 36, 23]        |[31, 2, 28] |[7, 39, 51]         |
|        45|[17, 28, 13]        |[0, 28, 15] |[7, 16, 51]         |
|        46|[26, 28, 49]        |[49, 7, 50] |[39, 51, 47]        |
|        47|[22, 23, 21]        |[22, 23, 13]|[51, 39, 46]        |
|        48|[2, 25, 28]         |[2, 17, 28] |[14, 35, 39]        |
|        49|[50, 36, 31]        |[50, 36, 34]|[39, 7, 47]         |
|        50|[49, 30, 43]        |[49, 2, 36] |[39, 47, 7]         |
|        51|[8, 13, 15]         |[13, 8, 15] |[47, 39, 46]        |


## Content Example

Below, a side-by-side comparison of content of the baseline and diverse recommendation list is presented. The lists are calculated to be recommended for the first article (id=0) in the dataset. 



|     Article ID     |                               Title                               |Publisher|                                                                                                                                                                                                                                                     First 75 words                                                                                                                                                                                                                                                     |                  Blendle Link                   |
|--------------------|-------------------------------------------------------------------|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|
|__Original Article__|                                                                   |         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                                 |
|                   0|1,5 meter                                                          |adn      |De 1,5 metermaatschappij bestaat niet. In treinen, bussen en vliegtuigen is het onmogelijk om die afstand te bewaren. Tandartsen, schoonheidsspecialisten en kappers kunnen hun werk niet doen als ze niet dichtbij mogen komen. Maar het is al net zo onrealistisch om een bezoek aan de supermarkt te brengen met een persoonlijke ruimte van 1,5 meter om je heen. Of als fietser door de stad te rijden. We slalommen ons een onmogelijke weg door de wereld                                                        |http://blendle.com/item/bnl-adn-20200604-12058748|
|__Baseline List__   |                                                                   |         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                                 |
|                   1|Tijd om weer te leven, maar helaas                                 |adn      |We kunnen twee weken later wel concluderen dat de demonstratie op de Dam niet tot een tweede golf heeft geleid, evenmin als Koningsdag, Hemelvaart en Pinksteren. Ik weet niet hoe het met jullie zit, maar in mijn omgeving lijkt het leven bijna weer normaal. Nu we lunchen op terrassen en bier drinken in cafés, praten over andere dingen dan corona, de voorpagina's niet meer worden beheerst door het virus en we ook geen moeite hebben                                                                       |http://blendle.com/item/bnl-adn-20200613-12077731|
|                  37|Panopticum                                                         |vkn      |Mijn uitgever had hem al aangekondigd in een van vele corporate e-mails die we over het thuiswerken mogen ontvangen. En deze week lag hij dan op de deurmat. De Safekey. Een sleutelhanger met een plastic haak, goed om zonder aanraken deurklinken naar beneden te duwen, liftknoppen in te drukken, kortom je handen schoon te houden in de publieke ruimte. Neem hem mee als je weer op pad gaat! Ik ga dan net naar de legendarische                                                                               |http://blendle.com/item/bnl-vkn-20200710-12142695|
|                  25|O God der hygiëne                                                  |vkn      |Als ik zoete tranen over mijn wangen wil voelen biggelen, dan kijk ik naar dat filmpje waarin stervende chimpansee Mama haar oude verzorger Jan van Hooff omhelst. Ik smelt geheid weg bij die liefde tussen mens en dier. Zie je wel, verschillende levensvormen kunnen echt contact met elkaar maken! Inmiddels heeft die verbondenheid van al het leven zich getoond in een minder zoete variant. Wij worden collectief omhelsd - maar op knellende wijze, door een                                                  |http://blendle.com/item/bnl-vkn-20200615-12084547|
|__Diverse List__    |                                                                   |         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                                                 |
|                  39|Nertsvertoning                                                     |vkn      |Het is allang geen voorpaginanieuws meer, en dat is best gek. Misschien omdat de coronabesmetting in een nertsenfokkerij in het Brabantse Aarle-Rixtel maandag al de 23ste in een paar weken tijd was. Je zou zeggen dat dit de noodzaak alleen maar vergroot om ons te bevrijden van die achterlijke leedindustrie, maar Nederland trekt z'n schouders op en loopt verder, schouder aan schouder de winkelstraat door. Verdoofd door het virus van onverschilligheid. En dus worden alle                               |http://blendle.com/item/bnl-vkn-20200714-12150438|
|                  50|Mondkapplicht schaadt wél burgerlijke vrijheid                     |vkn      |Met de zomerse opleving van het virus leeft ook de discussie over mondkapjes op. Het regeringsstandpunt is nog steeds: een niet-medisch mondkapje beschermt u niet. Het kan meerwaarde hebben, mits bij zorgvuldig gebruik. Talloze andere landen stellen mondkapjes verdergaand verplicht in het openbare leven. Ziet Nederland iets over het hoofd? Er is geen betrouwbaar bewijs dat mondkapjes helpen. Je hoort vaak: 'baat het niet, dan schaadt het niet'. Maar hier moet niet lichtzinnig over worden            |http://blendle.com/item/bnl-vkn-20200728-12180104|
|                  18|Covid-19 toont hoe zelfredzaamheid in de armste landen is aangetast|trn      |De inzet van ontwikkelingssamenwerking is de laatste decennia veelal gericht geweest op het versterken van de veerkracht van de allerarmsten. Veel projecten beogen - direct of indirect - deze mensen te leren om beter om te gaan met veranderingen en tegenslagen. Dit klinkt nuttig, zeker in tijden van crisis. Maar is dit wel gerechtvaardigd? Wetenschappelijk onderzoek in verschillende landen naar de effecten van de coronacrisis op huishoudens die afhankelijk zijn van kleinschalige landbouw, laat zien |http://blendle.com/item/bnl-trn-20200716-12155257|
