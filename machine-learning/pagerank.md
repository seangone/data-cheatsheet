# PageRank

[Source 1](https://wizardforcel.gitbooks.io/dm-algo-top10/content/pagerank.html)

[Source 2](https://zhangyi.gitbooks.io/spark-in-action/content/chapter2/pagerank.html)

PageRank是Google专有的算法，用于衡量特定网页相对于搜索引擎索引中的其他网页而言的重要程度。它由Larry Page 和 Sergey Brin在20世纪90年代后期发明。PageRank实现了将链接价值概念作为排名因素。
PageRank将对页面的链接看成投票，指示了重要性。

## Idea

Key idea: rank pages by linkage too

- how many pages that point to a page?
- how important these pages are?

Eg.

- USC.edu can be important
    - because many pages point to it
- Your home page can be important
    - if it is pointed to by USC

Explanation:

- Probability that a random surfer lands on the page

例如网页Y被X1，X2，X3，X4四个网页所链接，且这四个网页的权重分别为0.001，0.01，0.02，0.04，则网页Y的Rank值=0.01+0.02+0.03+0.04=0.071。但问题是，如何获得X1,X2,X3,X4这些网页的权重呢？答案是权重等于这些网页自身的Rank。然而，这些网页的Rank又是通过链接它的网页的权重计算而来，于是就陷入了“鸡与蛋”的怪圈。解决办法是为所有网页设定一个相同的Rank初始值，然后利用迭代的方式来逐步求解。

假设一个由4个页面组成的小团体：A，B，C和D。如果所有页面都链向A，那么A的PR（PageRank）值将是B，C及D的Pagerank总和。

$$PR(A) = PR(B)/L(B) + PR(C)/L(C) + PR(D)/L(D)$$

L(Node)是以Node为起点的链接数量。

- Detail 1 It might happen that L(Node) = 0

Revised:

$$PR(A) = (PR(B)/L(B) + PR(C)/L(C) + PR(D)/L(D)) * d + \frac{1-d}{N}$$


- Detail 2 It might happen that one page points to itself.

Revised:

We assume that one person visit this page that points to itself and randomly go to another random page.

$$PR(A) = \alpha \sum_{p_j \in M_{p_i}}{\frac{PR(p_j)}{L(p_j)}} + \frac{1-d}{N}$$




