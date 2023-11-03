
# Table of Contents
...

# Clustering Algorithms Types (Overview)

Types of clustering algorithms ([source1](https://link.springer.com/chapter/10.1007/978-981-13-7403-6_9), [source2](https://iprathore71.medium.com/clustering-975f8bc58af0)):
![Pasted image 20231020075812](../../Media/Default/Pasted%20image%2020231020075812.png)
Side note: these are a subset of algorithms from 2019, new algorithms are always emerging :]

A lot of the basic algorithms of each type have a time-series version.

The following subsections contain brief explanation of basic algorithms.

# Partitional Clustering

Illustrations:

[Source](https://computing4all.com/courses/introductory-data-science/lessons/a-few-types-of-clustering-algorithms/)
![375](../../Media/Default/Pasted%20image%2020231020083201.png)

[Source](https://www.researchgate.net/figure/Partitional-Clustering_fig2_312590567)
![475](../../Media/Default/Pasted%20image%2020231020083221.png)

## K-Means

[Source](https://www.codecademy.com/learn/machine-learning/modules/dspath-clustering/cheatsheet)
![k-means-coedacademy](../../Media/AI/k-means-coedacademy.mp4)

Also check source above to understand ***Inertia*** metric measure and how to graph it in order to find optimal K value.

## K-Medoids

[source](https://medium.com/@ozturkfemre/unsupervised-learning-in-r-k-medoids-clustering-8645a6521e4)
![k-medoids-odyash-coedacademy](../../Media/AI/k-medoids-odyash-coedacademy.mp4)

To put it simply: it is similar to K-means, but instead of creating a centroid at a new coordinates, we choose an existing data sample to be the centroid.

## Kernel K-Means



# Density-Based Clustering

## When to Use Density-Based Clustering

Sometimes, we want to cluster data points based on their densities. Example ([source](https://pberba.github.io/stats/2020/07/08/intro-hdbscan/)):
![Pasted image 20231020083622|550](../../Media/Default/Pasted%20image%2020231020083622.png)

Visualizing the density landscape:
![Pasted image 20231020083643](../../Media/Default/Pasted%20image%2020231020083643.png)

So, we want to get around 5 clusters (visualized in red in the above graph). 

If we try partitional-based methods (e.g., K-means), it won't give us optimal results:
![Pasted image 20231020083847](../../Media/Default/Pasted%20image%2020231020083847.png)

So we should try density-based methods (like HDBSCAN shown on the right graph).

## Terminologies

[Main Source](https://www.atlantbh.com/clustering-algorithms-dbscan-vs-optics/)

### Epsilon (ε) and minPoints (minPts)

- **Epsilon (ε)**
	- the maximum "distance" between two points for one to be considered as in the neighborhood of the other. 
		- For example in the visualization below, all black points are neighbors of the "main" pink point, but the yellow point is not a neighbor:
		  ![[Pasted image 20231025210730.png]]
		- Note: "A distance" can be defined as any type of distance function
			- Side note: a "distance function" (e.g., Euclidian, dynamic time wrapping (DTW), etc.), is not to be confused with a "distance type" (e.g., [[#Types of Distances (Core, Reachability)|core distance, reachability distance]])
- **minPoints (minPts)**
	- the minimum number of points in a neighborhood of a radius **ε** for a point to be considered as a **core point** (this includes the point itself).
		- For example in the visualization above, if `minPoints <= 4`, then the pink point is considered a **core point**
		- Notice that this definition is closely tied to the definition of **core point** (mentioned below)

### Types of Points (Core, (Directly) (Density) Reachable, Noise, Connected)

- **Core point**
	- a point _p_ is called a core point if at least **minPoints** (including itself) are within distance **ε** of it.
- **Directly reachable point** (i.e., **Direct density reachable point**)
	- If point *q* is within distance **ε** from a core point *p*, then *q* is directly reachable from *p*.
	- Note 1: *p* has to be a **core point**.
	- Note 2: *q* itself doesn't have to be a **core point**.
		- Side note: If *q* it is not a **core point**, then it is called a **border point**.
	- Note 3: This relationship can be symmetric or asymmetric ([source: G4G](https://www.geeksforgeeks.org/ml-dbscan-reachability-and-connectivity/)). For example:
	  ![[Pasted image 20231028200716.png|400]]
- **Reachable point** (i.e., **Density reachable point**) ^l5ybzr
	- If there is a **path of core points** from *p* to *q*, then *q* is reachable from *p*
		- Note 1: A "path" is formed by a series of **directly reachable** points starting from *p*.
		- Note 2: *p* and all points in the "path" must be **core points**.
		- Note 3: *q* doesn't have to be a core point.
			- Side note: If *q* it is not a **core point**, then it is called a **border point**.
		- Note 4: This relationship can be symmetric or asymmetric ([source: G4G](https://www.geeksforgeeks.org/ml-dbscan-reachability-and-connectivity/)). For example:
		  ![[Pasted image 20231028201729.png|450]] ^93uj4q
- **Border point**
	- If *q* is a **directly reachable point** or a **reachable point** from *p* and is not a **core point**, then *q* is a **border point** to *p*.
	- Example of this is can be found in point *q* in the visualization above.
- **Noise Point (i.e., Outlier)**
	- If a point is not **reachable** from any other point, it is considered to be an outlier or noise point.
	- Example of this is can be found in point *z* in the visualization above.
		- Explanation: *z* is only present in *q*'s ε-neighborhood, but *q* is not a **core point**, so the **reachable point** definition is not applicable to *z*.
- **Connected point** (i.e., **Density connected point**)
	- Definition 1: If there is a **path of core points** from *p* to *q*, then *q* is connected to *p*, and ***vice versa***.
		- In other words, ***connected point*** has a similar definition as [[Clustering Algorithms#^l5ybzr|reachability point]], but the [[Clustering Algorithms#^93uj4q|symmetric property]] will now apply to both *p* and *q* (i.e., *p* is connected to *q*, and *q* is connected to *p*). Example:
		  ![[Pasted image 20231028203614.png|425]]
	- Definition 2 ([source 1](https://towardsdatascience.com/dbscan-make-density-based-clusters-by-hand-2689dc335120#:~:text=3.%20Density%20Connected%3A%20Two%20points%20are%20called%20density%20connected%20if%20there%20is%20a%20core%20point%20which%20is%20density%20reachable%20from%20both%20the%20points.), [source 2](https://www.geeksforgeeks.org/ml-dbscan-reachability-and-connectivity/#:~:text=from%20object%20q.-,Connectivity,-%E2%80%93)): If there're two points *p* and *q* that are ***reachable*** from a ***core point*** *o*, then *p* and *q* are ***connected***.
	- Note: definition 1 and 2 both mean the same thing; they're just different ways of defining a **connected point**.

Example 2:
![[Pasted image 20231025212504.png]]

### Types of Distances (Core, Reachability)

* **Core distance**
	* Given a **minPoints** value, it is the minimum distance required for _p_ to be considered a core point.
		* For example, in the visualization below, assuming `minPoints=4`, then if ε had a slightly less value, then `b` won't be a neighbor of `a`, and `a` will not be a **core point** anymore. Therefore, the current value of ε is considered the **core distance** (i.e., minimum distance) of `a`:
		  ![[Pasted image 20231025210730.png]]
* **Reachability distance** (of *q* <mark style="background: #FFB8EBA6;">with respect to</mark> *p*)
	* Mathematically, it is `max(core_distance_p, d(q,p))`, where:
		* *p* is a **core point**.
			* Side note: if *p* is not a core point, then *q* will not have a reachability distance to *p*. 
		* `core_distance_p` is *p's* **core distance**.
		* `d(q,p)` is *p's* **ε** required to make *q* **directly reachable** to *p*. 
			* Tip: If you're confused, re-read the definition of a **directly reachable point** in the [[#Types of Points (Core, (Directly) (Density) Reachable, Noise, Connected)|Types of Points]] section
	* In other words, *q's* **reachability distance** to a core point *p* is the maximum between *p's* core distance and the smallest distance such that _q_ is directly reachable from _p_ (i.e., the smallest **ε** required for *q* to be a neighbor of *p*).
	* Note: the intuition behind the **reachability distance** aims to answer the following question:
		* Should I expand *p's* **ε** in order for *q* to be a neighbor of *p*?
			* If yes, then the new **ε** will be `ε_pq`
			* If no, then **ε** will remain as `core_distance_p`
	* Example:
	  ![[Pasted image 20231025215910.png]]

### Reachability Plot (Graph)

* The reachability plot is a visualization that shows the **reachability distance** of each point <mark style="background: #FFB8EBA6;">with respect to</mark> its **nearest core point** ([source](https://cdanielaam.medium.com/understanding-optics-clustering-hands-on-with-scikit-learn-1786bddc71f5#:~:text=the%20reachability%20plot.-,Reachability%20plot,-%E2%86%92%20Represents%20distance%20to))
* This plot helps us visualize the density hierarchy of clusters. For example ([source](https://youtu.be/CV0mWaHOTA8?t=1488)), in the plot below, we can see that the right-most yellow cluster could be further divided into 3 highly dense clusters:
  ![[Pasted image 20231027195700.png]]
  side-note: each bar on the x-axis represents an ordered point in the dataset, while the y-axis represents these points' reachability distance <mark style="background: #FFB8EBA6;">with respect to</mark> their respective preceding points. Explanation of this and of the algorithm used to plot this visualization is in the OPTICS section, so feel free to see that section, then come back here. ^6t454f
* The valleys in the reachability plot represent areas of high density, while the peaks represent points that are far away from the core points. These peaks can also be referred to as outliers or cutoff points ([source](https://cdanielaam.medium.com/understanding-optics-clustering-hands-on-with-scikit-learn-1786bddc71f5#:~:text=the%20reachability%20plot.-,Reachability%20plot,-%E2%86%92%20Represents%20distance%20to)).
	* Regarding "cutoff points": they are the **Epsilon (ε)** that we set such that <mark style="background: #D2B3FFA6;">all points above the "cut" are classified as noise</mark>, and each time that there is a break when reading from left to right signifies a new cluster ([source](https://scikit-learn.org/stable/modules/clustering.html#hdbscan:~:text=all%20points%20above%20the%20%E2%80%98cut%E2%80%99%20are%20classified%20as%20noise%2C%20and%20each%20time%20that%20there%20is%20a%20break%20when%20reading%20from%20left%20to%20right%20signifies%20a%20new%20cluster.)).
	* Example of setting **Epsilon** = 0.5: ([source 1](https://scikit-learn.org/stable/modules/clustering.html#optics), [source 2](https://scikit-learn.org/stable/auto_examples/cluster/plot_optics.html)):
	  ![[Pasted image 20231027201602.png]]
	* When **Epsilon** = 2:
	  ![[Pasted image 20231027202128.png]]
	  Note: regarding the highlighted purple cluster: "the blue and red clusters are adjacent in the reachability plot (i.e., have similar values on y-axis and near each other on x-axis), and can be hierarchically represented as children of a larger parent cluster." ([source](https://scikit-learn.org/stable/modules/clustering.html#optics:~:text=the%20blue%20and%20red%20clusters%20are%20adjacent%20in%20the%20reachability%20plot%2C%20and%20can%20be%20hierarchically%20represented%20as%20children%20of%20a%20larger%20parent%20cluster.)). However, the purple parent cluster wasn't created when **Epsilon** was 0.5, as the clusters appeared to be cut-off on the x-axis (i.e., they aren't near each other anymore). Visualization of this:
	  ![[Pasted image 20231027202507.png]] 
	* Example when **Epsilon** is automatically determined using OPTICS algorithm (instead of being manually set in the DBSCAN algorithm):
	  ![[Pasted image 20231027202959.png]]
	  Ok, but in this case, what is the cut-off value?? Answer: Actually, there are multiple cut-off values decided by the steepness of each cluster's slope, where the user can define a parameter `xi` to set this slope threshold ([source](https://scikit-learn.org/stable/modules/clustering.html#optics:~:text=The%20default%20cluster%20extraction%20with%20OPTICS%20looks%20at%20the%20steep%20slopes%20within%20the%20graph%20to%20find%20clusters%2C%20and%20the%20user%20can%20define%20what%20counts%20as%20a%20steep%20slope%20using%20the%20parameter%20xi)). Alternatively, check [this](<https://pro.arcgis.com/en/pro-app/latest/tool-reference/spatial-statistics/how-density-based-clustering-works.htm#:~:text=For%20Multi%2Dscale%20(OPTICS)%2C%20the%20work,separations%20between%20clusters%20(resulting%20in%20more%20clusters).>) source to see the term "**cluster sensitivity**" used instead of slopes.



Illustration 2 ([source](<https://www.atlantbh.com/clustering-algorithms-dbscan-vs-optics/#:~:text=Figure%204.%20Demo%20of%20OPTICS%20algorithm%20(Anja%20Plakalovic)>)):
![[opitcs-algo-vis.mp4]]
side note: I don't think the `Reachability` column in the last video frame is correct, but was altered to make the [reachability plot](https://www.atlantbh.com/clustering-algorithms-dbscan-vs-optics/#:~:text=Figure%205.%20Reachability%20plot%20(Anja%20Plakalovic)) obvious looking, so take this example with a grain of salt.

## DBSCAN

Stands for: Density-Based Spatial Clustering of Applications with Noise

[Source1](https://cjauvin.blogspot.com/2014/06/dbscan-blues.html), [Source2](https://pberba.github.io/stats/2020/07/08/intro-hdbscan/), [implementation Source3](https://cjauvin.blogspot.com/2014/06/dbscan-blues.html)

How DBSCAN differs from K-Means and K-Medoids:

> Instead of relying on created/assigned centroids to create a cluster, we rely on each data point to create its own tiny cluster based on its neighbors, then, these tiny clusters merge into bigger clusters.   


Key parameters: [[#Epsilon (ε) and minPoints (minPts)|Epsilon (eps) (𝜀) and minPoints (minPts)]]

Based on these two parameters, points are classified as [[#Types of Points (Core, (Directly) (Density) Reachable, Noise, Connected)|core point, border point, or outlier]], and can be visualized here ([full explanation source](https://towardsdatascience.com/dbscan-clustering-explained-97556a2ad556)):
![[Pasted image 20231020161129.png]]
Where:
Core point -> Red
Border point -> Yellow
Outlier -> Blue
minPts -> 4
Side note: in the image above, all of the points (except point `N`) will form a single cluster at the end. If you don't understand why, check out the algorithm steps and example demonstration below. 

Algorithm steps:
1. Choose `eps` and `minPts` values
2. Choose a random unlabeled point `x`.
3. Check if `x` is a ***core point***.
	1. If no
		1. Label as ***noise*** 
		2. Repeat (2. and 3.).
	2. If yes
		1. Label `x` and its neighbors to a cluster name (e.g., `X`).
		2. For each neighbor point, check if it is a ***core point***
			1. If yes
				1. Label its neighbors to cluster `X`
				2. Recurse the for loop on its ***unvisited*** neighbors
			2. If no, move on to next neighbor point
4. Repeat (2. and 3.), with a different cluster label, until all points are visited. 

Algorithm steps' visualization with example:
(side note: algorithm steps in the video are similar to steps above; just written differently.)
![[dbscan-vis-with-steps.mp4]]
As we can see in the example above, 5 points formed a single cluster called `X`, while the top-left blue point didn't form any clusters.

Another visualization that initially marks visited non-core points as ***noise*** ([source](https://dashee87.github.io/data%20science/general/Clustering-with-Scikit-with-GIFs/#:~:text=by%20the%20parameters.-,DBSCAN,-Density%2Dbased%20spatial)):
![[dbscan-better-vis.mp4]]
Side note: hide the video's play bar to see the bottom text in the video.

Disadvantages of the DBSCAN algorithm: 
* Assumes that all cluster densities are equal ([source](https://www.atlantbh.com/clustering-algorithms-dbscan-vs-optics/#:~:text=DBSCAN%20algorithm%20actually%20assumes%20that%20the%20densities%20of%20different%20clusters%20are%20equal))  ^yz3hs7
	* This is because DBSCAN uses ***one constant distance value (ε)*** together with one density threshold (_minPts_) to determine whether a point is in a dense neighborhood.
		* The ***constant distance value (ε)*** issue (i.e., global parameter *(ε)*) can be avoided by extending DBSCAN to use [[#OPTICS Ordering (Sorting) Algorithm|OPTICS]] algorithm.
* Can be sensitive to the scale of the data and the number of dataset samples, so we might need to iterate over several values of 𝜀 to get good results ([source](https://pberba.github.io/stats/2020/01/17/hdbscan/#:~:text=Note%20that%20this%20can%20be%20sensitive%20to%20the%20scale%20of%20the%20data%20and%20the%20sample%20size.%20You%20might%20need%20to%20iterate%20over%20several%20values%20of%20%F0%9D%9C%80%20to%20get%20good%20results.)).

### OPTICS Ordering (Sorting) Algorithm

OPTICS:
* Stands for *Ordering Points To Identify Clustering Structure*.
* Used to overcome the [[Clustering Algorithms#^yz3hs7|global parameter issue of DBSCAN]], which allows this algorithm to find clusters *with different densities* and their hierarchies. Example:
  ![[Pasted image 20231028165320.png]]
  ([source: slide 2 and 7](https://pt.slideshare.net/rpiryani/optics-ordering-points-to-identify-the-clustering-structure?next_slideshow=true))
* Is considered a generalization of DBSCAN that relaxes the `eps` requirement from a single value to a value range. ([scikit-learn source](https://scikit-learn.org/stable/modules/clustering.html#optics))
	* The key difference between DBSCAN and OPTICS is that the OPTICS algorithm builds a [[#Reachability Plot (Graph)|reachability graph]], which assigns each sample both a reachability_ [[#Types of Distances (Core, Reachability)|distance]], and a spot within the cluster `ordering_` [[Clustering Algorithms#^6t454f|attribute]]; these two attributes are assigned when the model is fitted, and are used to determine cluster membership. 

#### OPTICS Algorithm Details

TODO: add images from youtube video


TODO: move bullet points below to section after the algo details section
* scikit-learn implementation details: 
	* `cluster_method` argument, `xi`, and `dbscan` values ([source](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.OPTICS.html#:~:text=cluster_methodstr%2C%20default,xi%E2%80%9D%20and%20%E2%80%9Cdbscan%E2%80%9D.))
		* `cluster_method`:  
			* The method used to extract clusters using the calculated reachability and ordering. Possible values are “xi” and “dbscan”.
			* `dbscan` -> a DBSCAN-like method
			* `xi` -> automatic technique proposed in [1](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.OPTICS.html#r2c55e37003fe-1)
		* `xi` (default=0.05)
			* A float between 0 and 1
			* Used only when `cluster_method='xi'`.
			* Determines the ***minimum steepness on the reachability plot that constitutes a cluster boundary***. 
				* For example, an upwards point in the reachability plot is defined by the ratio from one point to its successor being at most 1-xi. 
	* `max_eps` vs `eps` parameters ([source 1](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.OPTICS.html), [source 2](https://scikit-learn.org/stable/modules/clustering.html#optics)):
		* `max_eps` (default: `np.inf`):
			* The maximum distance between two samples for one to be considered as in the neighborhood of the other. 
			* ***Default value of `np.inf` will identify clusters across all scales***; 
			* reducing `max_eps` will result in shorter run times.
		* `eps` (default: `None`):
			* Is considered by `OPTICS` class only if `cluster_method` is set to `dbscan`
			* Same definition of `max_eps`
			* when it is set to a close value to `max_eps`, then OPTICS' output will be close to DBSCAN's output. ([source](https://scikit-learn.org/stable/modules/clustering.html#optics:~:text=It%20is%20also%20important%20to%20note%20that%20OPTICS%E2%80%99%20output%20is%20close%20to%20DBSCAN%E2%80%99s%20only%20if%20eps%20and%20max_eps%20are%20close.)) 
				* Note: when it is set to the default value (i.e., `None`), then `eps = max_eps`
		* If OPTICS is run with `max_eps=inf` (default), then DBSCAN style cluster extraction can be performed repeatedly in linear time for any given `eps` value using the `cluster_optics_dbscan` method. Setting `max_eps` to a lower value will result in shorter run times, and can be thought of as the maximum neighborhood radius from each point to find other potential reachable points.



## HDBSCAN

[Amazing Source](https://pberba.github.io/stats/2020/07/08/intro-hdbscan/), [Phenomenal Source that is an in-depth explanation of the Amazing Source](https://pberba.github.io/stats/2020/01/17/hdbscan/)


HDBSCAN Stands for: _Hierarchical Density-based Spatial Clustering of Applications with Noise_

High-level logical steps of HDBSCAN:
1. Estimate the densities 
2. Pick regions of high density
3. Combine points in these selected regions

Note: we use this dataset as a recurring example throughout the upcoming sections:
![[Pasted image 20231021113546.png]]
Let's call it ***the HDBSCAN dataset***. ^mo6nvm

### The Two Methods of Estimating Densities

* To estimate the density of a group of data, there are two methods ([source](https://pberba.github.io/stats/2020/01/17/hdbscan/#:~:text=We%20need%20other%20ways%20to%20get%20the%20empirical%20PDF.%20Here%20are%20two%20ways%3A)):
	* Using minPts based on a given eps (𝜀-radius)
		* This is the DBSCAN method, and is explained in the [[#DBSCAN]] section.
	* Using ***core distance*** that is automatically calculated from the furthest K-th nearest neighbor.
		* This is the HDBSCAN method.
		* It is the complement of the DBSCAN method;
			* Instead of setting 𝜀 then counting the neighbors as threshold, we determine the number of neighbors "K" that we want and find the smallest value of 𝜀 that would contain these K neighbors:
			  ![[Pasted image 20231021142203.png]] ^x0k7le
			* This means that the core distance can now vary between groups of data (as seen in the image above). This was NOT the case with [[#DBSCAN]], where we had to manually specify a constant 𝜀-radius.
		* Unlike the previous method, this method is sensitive only to the number of dataset samples, and is NOT sensitive to data scaling;
			* If we scale each dimension equally, then all core distances will proportionally increase.
		* Core distance is inversely proportional with the data's estimated densities. For example (this is a random example):
		   ![[Pasted image 20231021113306.png]]
			* Side note 1: the estimate of density doesn't necessarily have to be `1 / core distance`, but can be any formula which captures how the density increases when the distance decreases and vice versa.
			* Side note 2: the right graph above is called a *density landscape*, but represented in 2D.


### Visualizing HDBSCAN Density Landscape and Level-Sets

Now, coming back to [[Clustering Algorithms#^mo6nvm|the HDBSCAN dataset]], we can visualize its ***3D density landscape*** like this:

![[Pasted image 20231021113711.png]]

Now, we said that we'll use HDBSCAN's ***core distance*** method to estimate densities. Therefore, we get an estimated density for the dataset based on the [[Clustering Algorithms#^x0k7le|value K]] that we provide. However, HDBSCAN will automatically use multiple K values (from high to low values) to get multiple ***level-sets*** (i.e., estimated densities).

For example, the visualizations below have the following 3 K values: 30, 25, 20, which will give us the average core distances: 0.025, 0.045, 0.6 ("average", as core distances change from a point to another, as seen in the [[Clustering Algorithms#^x0k7le|estimating densities section]]):
![[Pasted image 20231021150434.png]]

### Cluster Selection

### Using Global Threshold (Which is Incorrect)

Important question: how "highly dense" should a group of data be to be considered a cluster? In other words, what's the threshold? Answer always depends of the data, but instead of manual hyper parameter tuning, HDBSCAN tries to find the optimal threshold value for us :]

Let's try this by defining a ***global threshold*** called λ. Now, we can have _different number of clustering based on different thresholds_. Example:
![[Pasted image 20231021114121.png]]
Left has 2 clusters, right has 3 clusters.

Imagine islands on the ocean, where the sea level is the threshold and the different islands are your clusters. The land below the sea level is noise. As the sea level goes down, new islands appear and some islands combine to form bigger islands.
Here are several clusters that result as we lower the sea level. (With K=30):
* Contour map perspective:

* Scatter Chart Perspective:


However, Returning back to the illustration at the start of this section:
![[Pasted image 20231021114121.png]]
The question here is: should we consider this:
![[Pasted image 20231021120939.png]]
as a cluster? or does this part have too few data to be a cluster? 

What about this graph?:
![[Pasted image 20231021133948.png]]
Now, should the yellow (i.e., right) group of data be a cluster? 

These questions are why ***global thresholding don't work, and why we should assess if a group of data should be clustered*** <mark style="background: #FF5582A6;">based on its nearby data points</mark>.

<mark style="background: #FF5582A6;">HDBSCAN splitting strategy</mark> aims to fix this issue.

### HDBSCAN Splitting Strategy

HDBSCAN splitting strategy is used to select clusters ***from varying densities***.

To define the splitting strategy, we need to define a few terms first:
* 
* the threshold λ
	* Implementation wise, it is defined as [[#Epsilon (ε) and minPoints (minPts)|Epsilon (𝜀)]], automatically calculated as the [[#Epsilon (ε) and minPoints (minPts)|minPoints]] is automatically 
* level-set
	* it is the current cluster configuration of the data, given a chosen threshold λ