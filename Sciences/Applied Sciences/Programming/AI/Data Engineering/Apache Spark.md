#apache-spark

[source 2](https://www.databricks.com/blog/2014/01/21/spark-and-hadoop.html), [source 3](https://www.youtube.com/watch?v=AGgyf9bO_8M&list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi), [source 4](https://emerginginsightsnow.com/2015/05/17/apache-spark-ecosystem-grows-rapidly-has-hadoop-met-its-match/), [source 5](https://mydataexperiments.com/2017/04/11/hadoop-ecosystem-a-quick-glance/), [source 6](https://inoxoft.com/blog/key-differences-between-mapreduce-and-spark/), [source 7](https://www.youtube.com/watch?v=GAK3mbI_sPY&list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi&index=3), [source 8](https://www.quora.com/What-is-the-difference-between-spark-and-pyspark), [source 9](https://www.youtube.com/watch?v=YEGnTKRHpu8&list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi&index=3), [source 10](https://www.javatpoint.com/apache-spark-architecture), [source 11](https://mallikarjuna_g.gitbooks.io/spark/content/), [source 12](<https://www.databricks.com/glossary/what-are-spark-applications#:~:text=The%20driver%20process%20runs%20your,the%20executors%20(defined%20momentarily).>), [source 13](https://www.youtube.com/watch?v=71ntq5LImRc), 
Side notes:
* ([s11](https://mallikarjuna_g.gitbooks.io/spark/content/)) is amazing for mastering Spark. It is neither a book, nor a bunch of articles; it's something in between, and its explanations are straight to the point. Kudos to [Jacek Laskowski](https://pl.linkedin.com/in/jaceklaskowski)

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

You can compare the ecosystem above with [Hadoop's ecosystem](Hadoop.md#Hadoop's%20Ecosystem), noting that the latter's libraries aren't all built-in.

Side note 1: the Spark's affiliations, supported third-libraries, and built-in libraries ([s4](https://emerginginsightsnow.com/2015/05/17/apache-spark-ecosystem-grows-rapidly-has-hadoop-met-its-match/#:~:text=Spark%20Support%20Grows%20Quickly%20Among%20Platform%20Providers)):

![](Media-Temp/Pasted%20image%2020240124164315.png)


## Spark vs Hadoop's MapReduce

#apache-spark  #hadoop  #mapreduce  #caching  #disk-oriented  #memory-oriented

![](Media-Temp/Pasted%20image%2020240125101019.png)

([s6](https://inoxoft.com/blog/key-differences-between-mapreduce-and-spark/#anchor-comparing-spark-and-hadoop-mapreduce-differences))

Other differences ([s7, 8:40](https://youtu.be/GAK3mbI_sPY?list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi&t=520)):

![](Media-Temp/Pasted%20image%2020240125101955.png)

Visualization of <mark style="background: #FFF3A3A6;">in-memory caching</mark> ([s7, 3:14](https://youtu.be/GAK3mbI_sPY?list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi&t=194)). I.e., how Spark is <mark style="background: #FFF3A3A6;">memory-oriented</mark> while Hadoop is <mark style="background: #FFF3A3A6;">disk-oriented</mark>:

![](Media-Temp/Pasted%20image%2020240125101213.png)

Side note: At the very end, both the Spark and Hadoop jobs store the final processed data into the hard disk.

# Spark Architecture

![](Media-Temp/Pasted%20image%2020240125121533.png)

([s10](https://www.javatpoint.com/apache-spark-architecture#:~:text=Let%27s%20understand%20the%20Spark%20architecture))

## Spark Driver

#apache-spark  #spark-architecture  #spark-driver  #driver-process  #driver-program  

<mark style="background: #FFF3A3A6;">Spark driver</mark> ([s11](https://mallikarjuna_g.gitbooks.io/spark/content/spark-driver.html)) is the Spark application’s driver process:
* A <mark style="background: #FFF3A3A6;">driver process</mark>  runs your main() function, sits on a node in the cluster, and is responsible for three things ([s12](<https://www.databricks.com/glossary/what-are-spark-applications#:~:text=The%20driver%20process%20runs%20your,the%20executors%20(defined%20momentarily).>)):
	* maintaining information about the Spark Application.
	* responding to a user’s program or input
	* analyzing, distributing, and scheduling work across the executors (defined momentarily).

Spark driver is a JVM process that <mark style="background: #D2B3FFA6;">hosts</mark> [SparkContext](https://mallikarjuna_g.gitbooks.io/spark/content/spark-sparkcontext.html) for a Spark application, and also hosts the [Web UI](https://mallikarjuna_g.gitbooks.io/spark/content/spark-webui.html) for the environment.. It is the <mark style="background: #FFF3A3A6;">master node</mark> in a Spark application ([s11](https://mallikarjuna_g.gitbooks.io/spark/content/spark-driver.html)).

Spark driver splits a Spark application into tasks and schedules them to run on executors ([s11](https://mallikarjuna_g.gitbooks.io/spark/content/spark-driver.html)).

<mark style="background: #FFB86CA6;">Spark driver creates Spark Context, RDDs, and executes transformations and actions</mark> ([s11](https://mallikarjuna_g.gitbooks.io/spark/content/spark-driver.html)) .

Overview visualization of what the driver process does ([s12](<https://www.databricks.com/glossary/what-are-spark-applications#:~:text=The%20driver%20process%20runs%20your,the%20executors%20(defined%20momentarily).>)):

![](Media-Temp/Pasted%20image%2020240125142054.png)

Spark driver's internal services (adapted from [s11](https://mallikarjuna_g.gitbooks.io/spark/content/spark-driver.html)):

![](Media-Temp/Pasted%20image%2020240125143003.png)

## Spark Context

#apache-spark  #spark-architecture 

Side note: Most of the following info until the visualization below are from ([s11](https://mallikarjuna_g.gitbooks.io/spark/content/spark-sparkcontext.html)).

<mark style="background: #FFF3A3A6;">Spark context</mark> is the entry oint to Spark for a Spark application.

Note: You could also assume that <mark style="background: #ADCCFFA6;">a Spark Context instance is a Spark application</mark>.

It [sets up internal services](https://mallikarjuna_g.gitbooks.io/spark/content/spark-sparkcontext-creating-instance-internals.html) and establishes a connection to a [Spark execution environment (deployment mode)](https://mallikarjuna_g.gitbooks.io/spark/content/spark-deployment-environments.html).

Once a [`SparkContext` instance is created](https://mallikarjuna_g.gitbooks.io/spark/content/spark-sparkcontext.html#creating-instance) you can use it to [create RDDs](https://mallikarjuna_g.gitbooks.io/spark/content/spark-sparkcontext.html#creating-rdds), [accumulators](https://mallikarjuna_g.gitbooks.io/spark/content/spark-sparkcontext.html#creating-accumulators) and [broadcast variables](https://mallikarjuna_g.gitbooks.io/spark/content/spark-sparkcontext.html#broadcast), access Spark services and [run jobs](https://mallikarjuna_g.gitbooks.io/spark/content/spark-sparkcontext.html#runJob) (until `SparkContext` is [stopped](https://mallikarjuna_g.gitbooks.io/spark/content/spark-sparkcontext.html#stop)).

Visualization of Spark Context's internal workings ([s11](https://mallikarjuna_g.gitbooks.io/spark/content/spark-sparkcontext.html) ):

![](Media-Temp/Pasted%20image%2020240125144217.png)

# PySpark

#pyspark  

## PySpark vs Apache Spark

#pyspark  #apache-spark 

![](Media-Temp/Pasted%20image%2020240125102807.png)

([s8](https://www.quora.com/What-is-the-difference-between-spark-and-pyspark#:~:text=Let%E2%80%99s%20consider%20an%20example%20to%20make%20things%20easier%20to%20understand))

## PySpark vs Pandas

#pyspark  #pandas  #immutable  #lazy-execution  #eager-execution  #pyspark-transform

![](Media-Temp/Pasted%20image%2020240125103033.png)

([s9, 1:30](https://youtu.be/YEGnTKRHpu8?list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi&t=92))

Side note 1: "access is slower" in PySpark because it has to retrieve (i.e., access) the data from multiple nodes.


# Resilient Distributed Datasets (RDDs)

#apache-spark  #rdd  

TODO.

# RDD vs Spark DataFrame vs Spark Datasets

#apache-spark  #rdd  #spark-dataframe  #dataframe  #spark-dataset #pyspark-dataframe  #pandas-dataframe  #pandas

![](Media-Temp/Pasted%20image%2020240126144452.png)

([s13](https://www.youtube.com/watch?v=71ntq5LImRc))

![](Media-Temp/Pasted%20image%2020240126144538.png)

([s13](https://www.youtube.com/watch?v=71ntq5LImRc))

Check the [PySpark](PySpark.md) note for [difference](PySpark.md#PySpark%20DataFrame%20vs%20Pandas%20DataFrame) between PySpark's DataFrame and Pandas' DataFrame.

## Spark Schema

A schema in Spark defines the column names and associated data types for a DataFrame ([source](https://www.oreilly.com/library/view/learning-spark-2nd/9781492050032/ch03.html)). Defining a schema up front as opposed to taking a schema-on-read approach offers three benefits:

* Spark doesn't have to infer data types. 
* Spark won't create a separate job just to read a large portion of your file to ascertain the schema.
* You can detect errors early if data doesn’t match the schema.

You can define a Spark schema programmatically or using a DDL string. Example of the former:

```python
# In Python
from pyspark.sql.types import * 
schema = StructType([
	StructType(List(StructField("Id",IntegerType,false), 
	StructField("First",StringType,false), 
	StructField("Last",StringType,false), 
	StructField("Url",StringType,false), 
	StructField("Published",StringType,false), 
	StructField("Hits",IntegerType,false),
	StructField("Campaigns",ArrayType(StringType,true),false)))
])
```

Example of the latter:

```python
# Define schema for our data using DDL 
schema = "`Id` INT, `First` STRING, `Last` STRING, `Url` STRING, `Published` STRING, `Hits` INT, `Campaigns` ARRAY<STRING>"
```

# Data Lineage Graph (DLG)

#apache-spark  #data-lineage-graph

Side note: apparently, DLG is not a well-known acronym for data lineage graph, but I'll personally use it when referencing this term multiple times :\].