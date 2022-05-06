---
title: Text analysis
prev: data-description
next: network-analysis
---

The U.S. elections are one of the most observed international events, as they affect and influence different countries’ policy-making approaches and economies. Hence, various hidden aspects of elections are drawn out and analyzed using sentiment analysis, but it also has limitations; for example, it is hard to recognize sarcasm trivially. In some cases, the negative sentiments are classified as positive due to the writing styles employed. Note, the project does not cover these shortcomings. 

Social media might not represent complete sentiment in elections, since all voters are not present, but provides a sample space of people's opinions. One way of interpreting the texts left by users is by word clouds; a graphical representation of the word frequency that gives grater prominence to words appearing frequently in the source text. The larger the size of the word, the more impactful it is. By grouping each comment's body of text based on containing 'Trump' or 'Biden' and tokenizing, the following two word clouds were generated:

Trump                      |  Biden
:-------------------------:|:-------------------------:
![alt](/images/WordCloud_Trump.png) | ![alt](/images/WordCloud_Biden.png)  


*Analysis of WordCloud*

Investigating the evolution of the sentiments over the course of the election seems a natural extension to the analysis. Verifying the rule-of-thumb of having approximately 10.000 tokens for dictionary based methods to work confidently is the first step, which is shown in the figure below:

![](/images/DailyDoc.png)

The dip in the tail of this histogram is represented in the days following the election, of which comments on the submissions drastically fell off. Overall, it seems reasonable to continue conducting the analysis disregarding the final three days.

Using the [Hedonometer](https://hedonometer.org/words/labMT-en-v1/)[^1] happiness rating data the average happiness of each token in the daily documents of Joe Biden and Donald Trump were computed.

![](/images/Avghscore.png)

Comments pertaining to Biden indeed fluctuate more compared to his counterpart, which seems pretty stable around 5.5, the latter accounted for due to the 5-to-1 ratio of Trump vs. Biden comments. On the election day, both candidates seem to drop based off of the Reddit comments. This might be partially due to the oppositions scolding the results and in turn the candidates, respectively, as it is rarely unknown who will win before the last vote is counted.












[^1]: [Positivity of the English language](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0029484)