---
title: Data description
prev: "/"
next: network-analysis
---


# The submissions 
Visitors at r/politics will quickly notice that the majority of the submissions posted on the site are by users linking to news articles published on news media sites like CNN or The Huffington Post. The headlines of these linked articles are then shown on r/politics as the titles of the submissions. Other users can then comment on the linked article, which is what ultimately constitutes the actual user-generated content on the site.

__Figure 1__
![](/images/example_of_submission.png)
*One of the downloaded submissions mentioning "Trump".*

Using the [Pushshift API](https://github.com/pushshift/api), we focused our extraction of the submissions from r/politics to only include the ones fulfilling the following criteria:

* __They contained "Trump" or "Biden" in the title__ <br>
While submissions containing other words and names than "Trump" and "Biden" (e.g. "Republican" and "Democrat") might be used to provide equally good indications of the political convictions of redditors, this textual query allowed us to limit the scope of the project while still extracting data essential to the aim of this project.
* __They had received more than five comments__ <br>
This requirement was to prevent us from downloading submissions with no or only a very small comments section, as we'll be using the comments to conduct the later sentiment analysis and produce a partitioning of the redditors.
* __They had been published between 10-1-2020 and 11-3-2020__ <br> 
This period covered approximately a month before the most recent U.S. presidential election that took place on 11-3-2020. Ideally, we would have covered several months leading up to the election day, in order to detect longer term trends in the data. However, that would prove to be computationally infeasible, given the amount of data this would yield.

This extraction resulted in a total of 9044 submissions posted on r/politics from 01-10-2020 to 03-11-2020. Below we show number of daily submissions posted to the site together with the rolling 3-day average. The graph shows a quite clear weekly seasonality in the number of daily submissions, with lows typically occuring on Mondays. <br>

__Figure 2__
![](/images/submissions_per_day_big.png)
*Number of daily submissions mentioning either "Trump" or "Biden" posted on the r/politics subreddit between 01-10-2020 and 03-11-2020.*

## Submissions variables

For each submission, we collected six variables and computed a seventh "politician" variable, all of which was consolidated in a table, an exerpt of which is shown below.

__Figure 3__
![](/images/sub_data_exerpt.png)
*Subset of the table containing all the submissions data.*

__Description of variables__ <br>
* __dates:__ Simply stating when the submissions was made.
* __title:__ Being the title of the submission. Usually the header of the linked article.
* __id:__ A unique identifier for a particular submission.
* __author:__ The profile name of the author of the submissions.
* __num_comments:__ The number of comments received on the particular submission.
* __url:__ The link stated in the text of the submission.
* __politician:__ Stating whether the submission title mentions either "Trump" or "Biden".


![](/images/subs_distribution.png)


| __Summary statistics of the submissions__ |  | 
|---|---|
| Total number of submissions: | 9018 |
| Total number of submissions mentioning Trump: | 7205 |
| Total number of submissions mentioning Biden: | 1813 |
| Number of unique authors: | 2912 |
| Average number of submissions per author: | 3.1 |
| Average number of comments per submission: | 150.5 |


> Nulla in justo hendrerit, tincidunt mauris et, porta est. Donec in leo vitae est ultrices dapibus id nec tortor. Maecenas ut ipsum eu nisl cursus facilisis scelerisque eu ex. Aliquam euismod elementum libero, at vehicula ipsum.

Nam commodo lorem quis tortor euismod, ut ultrices orci aliquet. Sed eget dui nec sem ullamcorper convallis id nec ante. Aliquam ultricies a massa quis semper. Donec suscipit augue ut sagittis hendrerit. Aliquam erat volutpat. Proin aliquet maximus nibh, id aliquet justo maximus at. Sed accumsan ante id aliquam pellentesque. 


Aliquam nec hendrerit quam. Suspendisse maximus eros sollicitudin, accumsan turpis eu, blandit nulla. Nunc lorem elit, molestie at libero gravida, placerat consectetur ante. Sed tincidunt viverra tellus a vehicula.


1. Lorem ipsum dolor sit amet
1. Lorem ipsum dolor sit amet
1. Lorem ipsum dolor sit amet

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam blandit lobortis turpis. Praesent porttitor, turpis eu posuere molestie, sem dolor scelerisque sapien, eu aliquet ante felis ac metus. Pellentesque semper ultricies urna. Aenean auctor, turpis ut convallis ultrices, eros tellus bibendum risus, eu varius velit ante et diam. 

* Lorem ipsum dolor sit amet
* Lorem ipsum dolor sit amet
* Lorem ipsum dolor sit amet

In suscipit lorem orci, eu placerat nibh dignissim ut. Nullam consequat nisl dui, in ornare risus porttitor sed. Integer vitae nibh semper purus ultrices rutrum. Pellentesque non diam ornare, imperdiet elit a, tempus lacus. Suspendisse viverra euismod dapibus.

Suspendisse non tellus faucibus, dapibus leo at, elementum magna. Fusce quis ante ex. In non ex eleifend, luctus risus quis, dapibus velit. Nulla facilisi. Integer iaculis arcu at fermentum varius. Donec auctor dolor non dolor pulvinar luctus. Mauris vestibulum lacinia nisl, a dictum erat molestie sed. Vivamus vel blandit turpis, nec sollicitudin massa. Nunc velit eros, tristique elementum congue eget, auctor dictum tellus. 

Quisque iaculis, sem quis imperdiet faucibus, nunc lorem feugiat purus, vestibulum condimentum turpis turpis ut ante. Donec vestibulum lectus ut ullamcorper condimentum. Curabitur fermentum nulla vitae arcu sollicitudin pulvinar.

<img src="/images/dtu-logo.png" width="200" />

Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae; Suspendisse eu tellus ut erat porttitor luctus. Vivamus aliquam auctor massa, in auctor orci. Ut quis enim ut lorem consectetur blandit dictum eu mauris.