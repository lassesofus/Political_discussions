---
title: Network analysis
prev: text-description
---

## Building the network

In order to model the social interactions of the users with one another, we constructed an undirected network where all nodes were the authors. We then created reciprocal edges such that each edge represented that the two authors had replied to each other’s comment or reply at least once. Afterwards we assigned an edge weight based on the total number of replies or comments the two authors had written to one another, and added the inferred political conviction of each author as a node attribute in the network. Lastly we removed all singleton nodes and self-looping edges where an author replied to their own comment. <br>

## The network in numbers

> The constructed network consists of __1346 nodes__ and __3395 links__

In other words, there were 1346 members of r/politics who had both commented on another members post and received a comment from the same other member, at least once. 3395 such pairs of members were registered. On average, an author in the network was connected with 5 other authors with posts to r/politics, however with this value, the degree of the author nodes, spanning from 1 to 50. In order to further investigate the interactions of the users we examined the degree distribution of the authors in our Reddit network, by plotting the probability density for the degrees on a log-scale.

![](/images/probability_density_distibution_degrees_for_Reddit_network.svg)

As a reference we also included the degree distribution of a similar randomly constructed Erdos Renyi network. The random network contains the same number of nodes and links as the Reddit network, and where the probability of two nodes sharing an edge is constant and is calculated using the formula:

$$ p = \frac{2L}{N(N-1)} $$

Lastly we also plotted the mean of the average degrees for the two networks, as the two average degrees are almost identical. 

![](/images/probability_density_distibution_degrees_for_Reddit_and_random_network_NEW.png)

For the random network the probability mass is condensed at a small area with the density dropping significantly after its peak around degree 5. This is because the degree distribution follows a binomial distribution. Also it is interesting to observe that no nodes have a degree larger than 13. The probability mass for the Reddit is the highest for small degrees but then quickly drops off for larger degrees. However it is significantly more heavy-tailed than the one for the random network with the largest observed degree being 51. Therefore it approximately has the appearance of a power-law distribution, which is common for real social networks. This could suggest that there are a few active and popular authors with many social interactions and many other authors with only a few mutual interactions.

Next we calculated the clustering coefficient for our network. This measures the density of links in a node i’s immediate neighborhood on a scale from 0 to 1, for instance $$C_i = 0$$ would mean that there are no links between i’s neighbors. On the contrary, $$C_i = 1$$ implies that each of the i’s neighbors link to each other. 
In our Reddit network the clustering coefficient is 0.017. As the value is relatively low, this may suggest that a few active authors have a large number of connections, but that their neighbors often don’t have a lot of connections and are therefore mostly unconnected.


We also found the average shortest path length for all nodes in the largest connected component in our network to be 4.253. This means that an author on average can reach any other author in around 4 or 5 links (if they are in the same connected component). Consequently we assume that our network follows the 'small world property, commonly found in social networks.

## Visualizing the network

We then visualised the network using the Netwulf package. Nodes with the political conviction attribute "Trump" were colored red while nodes with the attribute "Biden" are blue. We also varied the size of the nodes proportional to their strength, which is the sum of the weights of the node's corresponding edges. Lastly we displayed the names of the 8 users with the largest degree - not factoring in the weights. The degree of a node in an undirected network is the number of edges that connect the node to other nodes.


![](/images/politics_network_new.svg)

From the graph we observe that the red and blue nodes are quite interconnected, and visually there doesn't seem to be two distinct communities for the supporters of Trump and Biden - however this will be investigated further. In some cases we observe a number of interconnected blue nodes that could look like “hubs” - however this might be caused by the disproportion between blue and red nodes - 872 vs 474 nodes respectively.

As seen in the figure, most of the nodes only have a few edges, while some nodes have a large degree. This might correspond to a few popular authors that interact mutually with many of the users. Most of the users only have a single mutual interaction. All of this is quite common for real social networks.

It is interesting to investigate if authors primarily interacted with other users of similar political conviction. Therefore we calculate the percentage of interactions between authors with the same political conviction - based on the edge weights. We find that around 56% of the interactions happened between users with a similar political conviction. This could suggest that the users communicate slightly more often with people that share their political belief, as this might be easier mentally and leads to a less polarizing discussion. However they still interact relatively often with someone they disagree with politically - as on the other hand, political disagreement might give users a larger incentive to reply to a comment. It is also important to keep in mind that our assumptions of the users political opinions contain some shortcomings, as they was inferred from the sentiment and do not represent a ground truth - whether the author actually supports Trump or Biden. Therefore they might be different from the users' true political opinions and our analysis is only an approximate estimate.

## Investigating the partition

We wanted to investigate if authors with the conviction of 'Trump' and 'Biden' can be separated into two distinct communities within the graph, and use modularity as a measure in order to evaluate the partitioning. Modularity is defined in the range [-1,1] and measures how much the network deviates from the expected number of edges between nodes in a community if all of its wirings had been randomly constructed. Thus, higher modularity for a given network partition indicates better community structure, meaning that separate communities are only sparsely connected compared to the densely connected individual communities. When the modularity *M* of a subgraph *C* is positive, it means that the *C* has more links than expected at random and could thus represents a potential community. If the modularity is zero then the connectivity between the nodes in the subgraph is random and explained by the degree distribution, therefore *C* is probably not a community. Furthermore if the modularity is negative *C* does also not form a community.

The modularity of the “Trump”/”Biden” partitioning is found to be around 0.017, which is relatively close to 0. Therefore it is unlikely that the authors with the 'Trump' and 'Biden' convictions form two communities in the network. This means that users with similar political conviction do not interact significantly more with each another than with other users. This also supports our previous findings that users interact more broadly across the political spectrum. Therefore we are interested in examining what communities then exist in the network. In this regard we use the Louvain algorithm to find the best partitioning of the graph, i.e. the partitioning that maximizes the overall modularity of the network. The algorithm finds 24 communities in the network with a modularity of 0.537. This suggests that the partitioning is reasonably good with stronger community structures. It is relatively unlikely the edges between the nodes in the communities have been created at random.

We then visualise the largest community using the Netwulf package.

![](/images/politics_network_largest_community.svg)
*The largest community in the partition maximizing the modularity of the network.*

We observe that the community contains a large number of both red red and blue nodes and that they are relatively interconnected. This suggests that users often interact with others that do not share their political belief, which also supports the general trend observed earlier.





