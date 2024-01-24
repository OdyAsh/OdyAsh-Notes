#apache-spark

[source 1](https://medium.com/analytics-vidhya/solving-complex-big-data-problems-using-combinations-of-window-functions-deep-dive-in-pyspark-b1830eb00b7d), [source 2](https://www.databricks.com/blog/2014/01/21/spark-and-hadoop.html), [source 3](https://www.youtube.com/watch?v=AGgyf9bO_8M&list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi), [source 4](https://emerginginsightsnow.com/2015/05/17/apache-spark-ecosystem-grows-rapidly-has-hadoop-met-its-match/), [source 5](https://mydataexperiments.com/2017/04/11/hadoop-ecosystem-a-quick-glance/)

# Spark vs Hadoop

## How Apache Spark Fits into Hadoop

#apache-spark  #hadoop  #hdfs  #standalone-spark-deployment  #simr-deployment  #hadoop-yarn-depolyment  #mapreduce 

* <mark style="background: #FFB86CA6;">Spark is intended to enhance, not replace, the Hadoop stack.</mark>
* Spark reads/writes data from/to storage systems like HDFS. In other words, <mark style="background: #FFB86CA6;">Spark cares about performing computations on the data (i.e., data processing).</mark>

There are three ways to deploy Spark in a Hadoop cluster: standalone, YARN, and SIMR (Spark in MapReduce):

![](Media-Temp/Pasted%20image%2020240124151740.png)

([s2](https://www.databricks.com/blog/2014/01/21/spark-and-hadoop.html#:~:text=there%20are%20three%20ways%20to%20deploy%20Spark%20in%20a%20Hadoop%20cluster%3A%20standalone%2C%20YARN%2C%20and%20SIMR.))

* <mark style="background: #FFF3A3A6;">Standalone Spark deployment</mark>: Statically allocate resources to part (or all) of a Hadoop cluster, and <mark style="background: #FFB8EBA6;">run Spark side-by-side with Hadoop's MapReduce</mark> (MR). This is a good choice for [Hadoop 1.x users](Hadoop.md#Hadoop%20Core%20Components%20(V1.0%20vs%20V2.0)).
* <mark style="background: #FFF3A3A6;">Hadoop YARN deployment</mark>: [Hadoop 2.x users](Hadoop.md#Hadoop%20Core%20Components%20(V1.0%20vs%20V2.0)) who use YARN can simply run Spark on YARN without any pre-installation or administrative access required.
* <mark style="background: #FFF3A3A6;">Spark In MapReduce (SIMR)</mark>: For the [Hadoop 2.x users](Hadoop.md#Hadoop%20Core%20Components%20(V1.0%20vs%20V2.0)) who are not running YARN yet, they can use SIMR to <mark style="background: #FFB8EBA6;">launch Spark jobs inside MapReduce to just experiment with Spark</mark> and use its shell within a couple of minutes after downloading it!

Important note: Spark doesn't have to use Hadoop's ecosystem. For example, look at the tools/methods underlined in red below ([s3](https://youtu.be/AGgyf9bO_8M?list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi&t=685)):

![](Media-Temp/Pasted%20image%2020240124162013.png)

## Spark Ecosystem vs Hadoop Ecosystem

#apache-spark  #hadoop  #data-ecosystem  

<mark style="background: #D2B3FFA6;">Hadoop requires external libraries to perform certain functionalities, while Spark may have these functionalities built-in it's ecosystem</mark> ([s3, 13:40](https://youtu.be/AGgyf9bO_8M?list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi&t=822)). This is why Spark can sometimes get confused with Hadoop; as Spark's ecosystem has become big enough to the point where it can rely on other built-in or supported third-party libraries to establish a data stack different than Hadoop's data stack.

Subset of Spark's built-in libraries' ecosystem ([s4](https://emerginginsightsnow.com/2015/05/17/apache-spark-ecosystem-grows-rapidly-has-hadoop-met-its-match/)):

![](Media-Temp/Pasted%20image%2020240124163832.png)

You can compare the ecosystem above with [Hadoop's ecosystem](Hadoop.md#Hadoop%20Ecosystem), noting that the latter's libraries aren't all built-in.

Side note 1: the Spark's affiliations, supported third-libraries, and built-in libraries ([s4](https://emerginginsightsnow.com/2015/05/17/apache-spark-ecosystem-grows-rapidly-has-hadoop-met-its-match/#:~:text=Spark%20Support%20Grows%20Quickly%20Among%20Platform%20Providers)):

![](Media-Temp/Pasted%20image%2020240124164315.png)

# Important Concepts

## Window

#pyspark #window-specification


Essentially ([s1](https://medium.com/analytics-vidhya/solving-complex-big-data-problems-using-combinations-of-window-functions-deep-dive-in-pyspark-b1830eb00b7d)):

![](Media-Temp/Pasted%20image%2020240118135116.png)

suppose you have this PySpark code:

```python
from pyspark.sql.window import Window
from pyspark.sql.functions import sum

window_spec = Window.orderBy("Age")
df_with_cumsum = df.withColumn("CumulativeSalary", sum("Salary").over(window_spec))
```

Explanation:

In the context of PySpark, a <mark style="background: #FFF3A3A6;">window specification defines ***how to*** apply a function to a group of rows</mark> (i.e., a <mark style="background: #FFF3A3A6;">frame</mark>) in a DataFrame. 

A window specification is used with <mark style="background: #FFF3A3A6;">window functions, which are designed to perform calculations across sets of rows that are related to the current row.</mark> This is similar to how an aggregate function operates but with a focus on individual rows.

Here's an in-depth look at the components of a window specification within PySpark:

- **Partitioning**: The `partitionBy` method can be used to divide the data into partitions (or groups) based on the values of one or more columns. Each partition is treated as an independent group for window calculations. If `partitionBy` is not specified, the entire dataset is treated as a single partition.

- **Ordering**: The `orderBy` method is used to define the ordering of the rows within each partition. In the case of cumulative sum, as in your example, ordering determines the sequence in which the rows' values will be added together.

- <mark style="background: #FFF3A3A6;">Frame Specification: This defines which rows will be included in the frame for each row's calculation.</mark> The frame can be specified using methods like `rowsBetween` or `rangeBetween`. If not explicitly defined, the frame includes all rows in the partition from the start up to the current row, which is suitable for cumulative calculations.

In the code snippet above, the window specification is defined as `window_spec = Window.orderBy("Age")`. This means that the window function will operate over the rows ordered by the "Age" column, and since there is no `partitionBy` clause, the entire DataFrame is assumed to be a single partition.

The cumulative sum is then calculated using `sum("Salary").over(window_spec)`, which means <mark style="background: #CACFD9A6;">for each row in the DataFrame, PySpark will sum up the "Salary" values of all rows up to and including the current row, based on the order defined by "Age".</mark> This cumulative sum is then added to the DataFrame as a new column called "CumulativeSalary".

The concept of window specification in PySpark is essential for performing advanced analytics where you need to carry out calculations across groups of rows <mark style="background: #FF5582A6;">while still retaining the individual row-level detail</mark>.

