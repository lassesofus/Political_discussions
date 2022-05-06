---
title: Text analysis
prev: data-description
next: network-analysis
---

The U.S. elections are one of the most observed international events, as they affect and influence different countries’ policy-making approaches and economies. Hence, various hidden aspects of elections are drawn out and analyzed using sentiment analysis, but it also has limitations; for example, it is hard to recognize sarcasm trivially. In some cases, the negative sentiments are classified as positive due to the writing styles employed. Note, the project does not cover these shortcomings.

## Word clouds

Social media might not represent complete sentiment in elections, since all voters are not present, but provides a sample space of people's opinions. One way of interpreting the texts left by users is by word clouds; a graphical representation of the term frequency - inverse document frequencies ([TF-IDF](https://www.wikiwand.com/en/Tf%E2%80%93idf)). This gives greater prominence to words appearing frequently in the source text, ie. larger words are most impactful. By aggregating the comments based on 'Trump' or 'Biden' and tokenizing, the following two word clouds were generated:

Trump                      |  Biden
:-------------------------:|:-------------------------:
![alt](/images/WordCloud_Trump.png) | ![alt](/images/WordCloud_Biden.png)  


Generally, the results show the same words with varying degrees of importance. Due to the likeness the scope of possible analysis is limited. Noteworthy differences may include "vote", "president", and "covid". The latter might be due to the inherent criticism of the Trump administration's response to Covid-19, one of the primary talking points of the election. 


The word clouds, while being a lens into the vocabulary of writers on Reddit, does not yield distinctive enough of an analysis to draw out anything of major value. Hence, the following carries into the dictionary based methods.

## Sentiment analysis

Investigating the evolution of the sentiments over the course of the election seems a natural extension to the analysis. Aggregating the comments dataset mitigates contextual issues, because there is generally more consistency in how positive and negative words are used in longer texts, which is verified by the rule-of-thumb of 10.000 tokens for each document and can be seen below:

![](/images/DailyDoc.png)
*The daily aggregated number of tokens for the comments in the collected dataset.*

The dip in the tail of this histogram is represented in the days following the election, of which the total daily length of comments on the submissions drastically fell off. Overall, it seems reasonable to continue conducting the analysis disregarding the final three days of 2020-11-04 till 2020-11-07. 

Using the [Hedonometer](https://hedonometer.org/words/labMT-en-v1/)[^1], or labMT lexicon, is a general purpose sentiment dictionary assembled by the Computational Story Lab at the University of Vermont. It was constructed by taking the 5,000 most frequently used words from Twitter, New York Times, Google Books, and music lyrics. In total, there are 10,022 words. Words were rated on a continuous scale from 1 to 9 by crowd workers on Amazon Mechanical Turk, where 1 is the least happy and 9 is the most. The average happiness of each token in the daily documents of Joe Biden and Donald Trump were computed:

![](/images/Avghscore.png)
*Average sentiment expressed in comments on r/politics for the two presidential candidates.*

Comments pertaining to Biden indeed fluctuate more compared to his counterpart, which seems pretty stable around 5.5, the latter accounted for due to the 4:1 ratio of Trump vs. Biden comments. On the election day, both candidates seem to drop based off of the Reddit comments. This might be partially due to the oppositions scolding the results, and in turn the respective candidate, as it is rarely unknown who will win before the last vote is counted.

![](/images/polling_data.svg)
*Polling data as presented in the Data section.*

Based on the polling data presented previouosly, there is an indication of Biden's higher happiness score correlating with more votes. One may also believe, that if the general populace opinion of a candidate is positive, it will reflect in the amount of people voting for them.

## Shifts on election day
The shifterator package allows for visualizing pairwise comparisons between texts by word shifts, extracting the essence difference and how they do so. Here, the idea is to compare the sentiments of comments on election day with the 33 preceding days'. The following plot has been made:

![](/images/shifteratorGraph.svg)
*Investigating the words that caused the largest change in the sentiment on 11-03-2020 compared to the preceding weeks.*

Inspecting the results, the primary difference of sentiments across time span between the two documents centres itself around crime, protests, the Covid-19 pandemic, and monetary problems such as taxes. Most noticeably, there is a trend towards a more negative sentiment on election day than previously. Many Trump-supporters were on the streets and harassed the vote counting offices, so it is not a surprise that these words occur in a more negative light, as the losing side tried to stamp the election as fraudulent.


## Partitioning redditors based on comments

To create a binary partitioning of the redditors active on r/politics in the objective period, we simply concatenated all the comments relating to Trump and Biden respectively for each redditor and calculated a compound sentiment score for each group of joined comments using the VADER module from the nltk.sentiment library. Whichever group of comments had a higher sentiment score would determine the inferred political conviction of the redditor. The Valence Aware Dictionary and sEntiment Reasoner (VADER) module has been specifically created to work with text produced on social media. One of the great features of this module is that it is quite robust in terms of the needed data cleaning and processing to function properly. Typical processing steps like tokenization and stemming as well as removing stop words are consequently not required to have the VADER module work well and provide an indication of the sentiment of a body of text. 

Having come up with a rather naïve inference of the political conviction of the redditors, the binary partitioning was made simply by dividing the redditors on this computed *conviction* attribute. This partitioning had 64 % inferred Biden supporters and 36% inferred Trump supporters, which would be used in our network analysis. 

[^1]: [Positivity of the English language](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0029484)