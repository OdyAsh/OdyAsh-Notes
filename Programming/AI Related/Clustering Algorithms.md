
# Clustering Algorithms Overview

Types of clustering algorithms ([source1](https://link.springer.com/chapter/10.1007/978-981-13-7403-6_9), [source2](https://iprathore71.medium.com/clustering-975f8bc58af0)):
![[Pasted image 20231020075812.png]]
Side note: these are a subset of algorithms from 2019, new algorithms are always emerging :]

A lot of the basic algorithms of each type have a time-series version.

The following subsections contain brief explanation of basic algorithms.

## Partitional Clustering

Illustrations:

[Source](https://computing4all.com/courses/introductory-data-science/lessons/a-few-types-of-clustering-algorithms/)
![[Pasted image 20231020083201.png|375]]

[Source](https://www.researchgate.net/figure/Partitional-Clustering_fig2_312590567)
![[Pasted image 20231020083221.png|475]]

### K-Means

[Source](https://www.codecademy.com/learn/machine-learning/modules/dspath-clustering/cheatsheet)
![[k-means-coedacademy.mp4]]

Also check source above to understand ***Inertia*** metric measure and how to graph it in order to find optimal K value.

### K-Medoids

[source](https://medium.com/@ozturkfemre/unsupervised-learning-in-r-k-medoids-clustering-8645a6521e4)
![[k-medoids-odyash-coedacademy.mp4]]

To put it simply: it is similar to K-means, but instead of creating a centroid at a new coordinates, we choose an existing data sample to be the centroid.


## Density-Based Clustering

Sometimes, we want to cluster data points based on their densities. Example ([source](https://pberba.github.io/stats/2020/07/08/intro-hdbscan/)):
![[Pasted image 20231020083622.png]]

Visualizing the density landscape:
![[Pasted image 20231020083643.png]]

So, we want to get around 5 clusters (visualized in red in the above graph). 

If we try partitional-based methods (e.g., K-means), it won't give us optimal results:
![[Pasted image 20231020083847.png]]

So we should try density-based methods (like HDBSCAN shown on the right graph).

### DBSCAN

Stands for: Density-Based Spatial Clustering of Applications with Noise

[Source1](https://cjauvin.blogspot.com/2014/06/dbscan-blues.html), [Source2](https://pberba.github.io/stats/2020/07/08/intro-hdbscan/)

How DBSCAN differs from K-Means and K-Medoids:

> Instead of relying on created/assigned centroids to create a cluster, we rely on each data point to create its own tiny cluster based on its neighbors, then, these tiny clusters merge into bigger clusters.   


Key parameters: 