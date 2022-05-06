---
title: Data Description
prev: "/"
next: text-analysis
---
During this project, we worked with three data sets

1. Submissions from the r/politics subreddit mentioning "Trump" or "Biden posted between 10-01-2020 and 11-2-2020.
2. The comments sections of the above submissions.
3. Polling data obtained from [FiveThirtyEight](https://data.fivethirtyeight.com/).

In the following, we will describe these datasets and give an overview of their most important properties. 

# 1. The Submissions 

Visitors at r/politics will quickly notice that the majority of the submissions posted on the site are by users linking to news articles published on news media sites like CNN or The Huffington Post. The headlines of these linked articles are then shown on r/politics as the titles of the submissions. Other users can then comment on the linked articles, which is what ultimately constitutes the actual user-generated content on the site.

![](/images/example_of_submission.png)
*One of the downloaded submissions mentioning "Trump".*

Using the [Pushshift API](https://github.com/pushshift/api), we focused our extraction of the submissions from r/politics to only include the ones fulfilling the following criteria:

 * __They contained "Trump" or "Biden" in the title__ <br>
While submissions containing other words and names than "Trump" and "Biden" (e.g. "Republican" and "Democrat") might be used to provide equally good indications of the political convictions of redditors, this textual query allowed us to limit the scope of the project while still extracting data essential to the aim of this project. Note that we omitted any submissions stating both "Trump" and "Biden" to avoid ambiguity about which of the candidates the submissions related to. 

* __They had received more than five comments__ <br>
This requirement was to prevent us from downloading submissions with no or only a very small comments section, which would be irrelevant as we'll be using the comments to conduct the later sentiment analysis and produce a partitioning of the redditors.

* __They had been published between 10-1-2020 and 11-2-2020__ <br> 
This period covered approximately a month before the most recent U.S. presidential election that took place on 11-3-2020. 

This extraction resulted in a total of 9,018 submissions posted by 2,912 different redditors. In the figure below, we show how these submissions were dispersed over the period preceding 11-03-2020. The graph shows a quite clear weekly seasonality in the number of daily submissions, with lows typically occuring on Mondays. <br> 

![](/images/submissions_per_day_new.svg)
*Number of daily submissions mentioning either "Trump" or "Biden" posted on the r/politics subreddit between 10-01-2020 and 11-02-2020.*

## Submission attributes

For each submission, we collected six attributes and computed a seventh *"Politician mentioned"* attribute, all of which was consolidated in a table, an exerpt of which is shown below.

![](/images/sub_data_df_new.png)
*Subset of the table containing all the submissions data.*

__Description of attributes__ <br>
* __Timestamp:__ Simply stating when the submissions was made.
* __Title:__ Being the title of the submission. Usually the header of the linked article.
* __ID:__ A unique identifier for a particular submission.
* __Author:__ The profile name of the author of the submission.
* __Number of comments:__ The number of comments received on the particular submission.
* __URL:__ The link stated in the text of the submission.
* __Politician mentioned:__ Stating whether the submission title mentions either "Trump" or "Biden".

Based on the "Politician mentioned" attribute of the collected submissions, we discovered that the majority of the submissions (7,205 of the total 9,018) mentioned "Trump" as seen in the chart below. <br>

![](/images/subs_distribution_NEW_2.svg)
*Approximately 80% of the downloaded submissions mentioned Trump and not Biden.*

Below we have gathered some summary statistics of the collected submissions. 

| __Statistics of the final submissions dataset__ |  | 
|---|---|
| Total number of submissions: | 9,018 |
| Total number of submissions mentioning Trump: | 7,205 |
| Total number of submissions mentioning Biden: | 1,813 |
| Number of unique authors: | 2,912 |
| Average number of submissions per author: | 3.1 |
| Average number of comments per submission: | 150.5 |


# 2. The Comments

For each of the 9,018 submissions, we downloaded the associated comments section, excluding any comments made by the most common moderator bots, like the *AutoModerator* bot who posts a comment to every submission on r/politics to remind users of the rules and guidelines of the subreddit.


![](/images/AutoMod.png)
*Image of a comment by the AutoModerator bot, one of the autonomous authors whose comments were omitted.*

Furthermore, our query to extract comments from the r/politics subreddit was also focused to only include comments fulfilling the following criteria: 

* __They were related to one of the downloaded submissions.__ <br> 

* __They were posted no later than 11-10-2020.__ <br> 
 By including comments posted up to one week after the election day, we would ensure that we would also have some comments for any submissions made on the day before the election day, without including comments that were made way after the objective period, which would not be representative of the sentiment during the objective period.

 ## Preprocessing of comments

To ensure that we only included authors with a good amount of comments on which to base our inference of the authors' political conviction, we excluded comments made by authors with less than 50 comments. 

As we wanted to create a binary partition of the active users on r/politics into Trump and Biden supporters based on their posts to the site, it was necessary to assign a label to each of the comments stating whether the comment related to either Trump or Biden. Our first approach to this labelling was to simply assign the "Politician mentioned" attribute of the submission to which each comment was connected by being part of its comments section. However, this labelling introduced some ambiguity in the case of  comments explicitely mentioning the candidate "opposite" of the one mentioned in their related submission. E.g. if the original submission mentioned Trump and one of its related comments mentioned Biden. Consequently, we decided to exclude these "ambiguous" comments and the entire part of the comments section stemming from these comments, as determining which of the candidates was refered to by these comments would be more non-trivial, given our rather naïve method of processing the natural language used in the comments. 

This resulted in a pruning of the comments section of each of the submissions, which can be visualized as a tree-like structure seen below with the root being the original submission and the branches being comments to this submission. 

__Figure 5__
![](/images/Pruning.svg)
*Illustration of how the comments section of each submission was pruned to avoid ambiguity regarding which of the presidential candidates the individual comments refered to. The root of the illustrated comments section tree is the original submission and the boxes below this are comments in its comments section. In each box, it is stated whether the post mentions, Trump, Biden or none of them ("...Bla bla..."). If a comment mentioned a candidate opposite of the one mentioned in the original submission, this comment and the entire part of the comments section stemming from this comment would be omitted, here marked by the red crosses.*

After this pruning of the comments sections, our original approach of labelling comments based on the "Politician mentioned" attribute of the related submission worked as intended. 

With these requirements, we ended up downloading a total of 91,672 comments posted by 1,553 unique authors. In the graph below, the daily number of comments is displayed. There seems to be a slight downwards trend in the daily comments made to the downloaded submissions, with comments dropping dramatically after the 11-02-2020, being the last day for which submissions were downloaded. 

![](/images/comments_per_day_new.svg)
*Number of daily comments included in the comments sections of the downloaded submissions.*

Finally, after having pruned the comments dataset, we excluded all comments made by redditors with less than 30 comments left in the pruned dataset.
Below we have gathered some summary statistics of the collected comments. 

| __Statistics of the final comments dataset__ |  | 
|---|---|
| Total number of comments: | 91,672 |
| Average number of characters per comment: | 138.25 |
| Total number of comments related to Trump: | 77,030 |
| Total number of comments related to Biden: | 14,642 |
| Number of unique comment authors: | 1,553 |
| Average number of comments per author: | 59.03 |


# 3. The Polling Data
The polling data used in this project is collected from FiveThirtyEight. The dataset contains polling results from our objective period, generated by different polling firms like YouGov and SurveyMonkey. Each poll has been generated over a smaller time window, typically spanning a couple of days, and with varying number of respondents. By the end of the polls, the percentage of respondents who have voted for a specific candidate has been registered. We have not investigated further how the individual polling firms have performed the polls, but we put our faith in their ability to make polls representative of the American population.

We calculated the simple average of the polls with identical ending dates and created the below plot showing the average daily polling percentages for the two presidential candidates. We see that during the last few weeks up till the election, Biden was in the lead, with Trump seeming to gain popularity during the last week before the election. 

![](/images/polling_data.svg)

