
[source 1](https://intellipaat.com/blog/interview-question/data-engineer-interview-questions/)

# What is Data Engineering?

Data engineering is the process of converting the raw entity of data into useful information that can be used for various purposes.

# OLTP vs OLAP

[source](https://medium.com/t%C3%BCrk-telekom-bulut-teknolojileri/whats-the-difference-between-oltp-and-olap-bdcafdffb1c3)

**OLTP** and **OLAP** look similar but refer to different kinds of database systems. Both of them are online processing systems. When we talk about databases, most people think of **OLTP**. <mark style="background: #FF5582A6;">We can suppose that OLTP systems provide source data to the OLAP data warehouse systems that help us to analyze the data</mark>.

![](Media-Temp/Pasted%20image%2020231111070425.png)

* OLTP -> Online Transactional Processing
* OLAP -> Online Analytical Processing

**Common tasks**:
* OLTP
	- What is the userID of the current user?
	- What is the current location of the user?
	- Delete billing information of a specific user or group.
	- Update user information.
- OLAP
	- - What’s the user life-time value of an application?
	- What’s the average age of users on a web platform?
	- User activities over time.
	- All data warehouse tasks.

Common systems:
* OLTP
	* MySQL
	- Oracle Database
	- PostgreSQL
	- Microsoft SQL
	- IBM DB2
- OLAP
	- Hadoop
	- Amazon Redshift
	- IBM Netezza
	- HP Vertica
	- KDB+

![](Media-Temp/Pasted%20image%2020231111071016.png)
([same source](https://medium.com/t%C3%BCrk-telekom-bulut-teknolojileri/whats-the-difference-between-oltp-and-olap-bdcafdffb1c3))


# What is Data Modeling?

defining all the different data types that a business collects, as well as the relationships between those bits of data.

Entity Relationship Diagram (ERD) is an example on how to apply data modeling.


## What are some of the design schemas used when performing Data Modeling?

There are two schemas when one works with data modeling. They are:
- Star schema
- Snowflake schema

Differences: ([source](https://www.integrate.io/blog/snowflake-schemas-vs-star-schemas-what-are-they-and-how-are-they-different/))
- Star schema dimension tables are not normalized while snowflake schema's dimension tables are normalized. 
- [Snowflake](https://trial.snowflake.com/?owner=SPN-PID-28241&utm_source=Xplenty&utm_medium=Blog&utm_campaign=SPIN) schemas will use less space than star schemas to store dimension tables but are more complex.
- Star schemas will only join the fact table with the dimension tables, leading to simpler, faster SQL queries.
- Snowflake schemas have no redundant data, so they're easier to maintain.
- Snowflake schemas are good for [data warehouses](https://www.integrate.io/blog/what-is-a-data-warehouse/) whereas star schemas are better for [datamarts](https://www.integrate.io/glossary/what-is-data-mart/) with simple relationships.

![](Media-Temp/Pasted%20image%2020231111065641.png)
([same source](https://www.integrate.io/blog/snowflake-schemas-vs-star-schemas-what-are-they-and-how-are-they-different/))

![](Media-Temp/Pasted%20image%2020231111070033.png)
([same source](https://www.integrate.io/blog/snowflake-schemas-vs-star-schemas-what-are-they-and-how-are-they-different/))


# What is Hadoop?

[source](https://intellipaat.com/blog/interview-question/data-engineer-interview-questions/)

* Hadoop is an open-source, Java based framework used for data storage/manipulation, and used for running applications on units called clusters.
	* managed by _Apache Software Foundation_ ([source](https://taylankabbani96.medium.com/mapreduce-programming-model-a7534aca599b#:~:text=managed%20by%20Apache%20Software%20Foundation)).
* Provisions large space for data storage and great processing power to handle limitless jobs and tasks concurrently.

## What are some of the important components of Hadoop?

There are many components involved when working with Hadoop, and some of them are as follows:
- **Hadoop Common**: Commonly used libraries/utilities by the Hadoop application.
- **Hadoop File System (HDFS)**: 
	- Stores data when working with Hadoop
	- Provides a distributed file system with very high bandwidth.
- **Hadoop YARN (Yet Another Resource Negotiator)**: 
	- Manages resources in the Hadoop system. 
	- Performs task scheduling.
- **Hadoop MapReduce**: It is a programming model that **allows access to large-scale data processing by performing parallel processing** across Big Data using a large number of nodes (multiple computers). ([source](<https://taylankabbani96.medium.com/mapreduce-programming-model-a7534aca599b#:~:text=perform%20parallel%20processing%20across%20Big%20Data%20using%20a%20large%20number%20of%20nodes%20(multiple%20computers).>))
	- A programming model is an execution model coupled to an API or a particular pattern of code.
		- a programming language consists of a syntax plus an execution model. The execution model specifies the behavior of elements of the language.
	- Comparing traditional vs MapReduce approach of managing data in a Master/Slave distribution system ([source](https://taylankabbani96.medium.com/mapreduce-programming-model-a7534aca599b#:~:text=Another%20big%20advantage%20offered%20by%20MapReduce%20is%20what%20we%20call%20Data%20Locality)):
	  
	  ![](Media-Temp/Pasted%20image%2020231111074048.png)
	  
		- Another MapReduce advantage: **Data Locality.** Simply put, data locality is bringing the processing unit to the data 
			- I.e., <mark style="background: #FF5582A6;">data locality means performing computation process on the site where the data is being saved instead of sending the data to the unit</mark>, which will significantly reduce the network traffic and consequently running time.
	- MapReduce steps are explained [here](https://taylankabbani96.medium.com/mapreduce-programming-model-a7534aca599b#:~:text=MapReduce%20programming%20Steps), a brief example:
	  
	  ![](Media-Temp/Pasted%20image%2020231111074329.png)

### MapReduce

[main source](https://data-flair.training/blogs/how-hadoop-mapreduce-works/), [source 2](https://www.talend.com/resources/what-is-mapreduce/), [source 3](https://taylankabbani96.medium.com/mapreduce-programming-model-a7534aca599b#:~:text=MapReduce%20programming%20Steps)

First, watch [this great computerphile video](https://www.youtube.com/watch?v=cvhKoniK5Uo) on MapReduce.

[Another optional video](https://www.youtube.com/watch?v=6ehu2jEEXWE) regarding shuffle and sort step specifically (noting that "shuffle" is referred to as "copy" in that video).

IMPORTANT NOTE: "key-value pair" will be abbreviated to KVP.

MapReduce job execution flow (i.e., flow chart):

![](Media-Temp/Pasted%20image%2020231111084115.png)

Each flow chart component is explained below:
* Input files
	* The data used for a MapReduce task.
	* Typically lives in **HDFS**. 
	* The format of these files is arbitrary.
* InputFormat
	* Selects the files or other objects that are used for input.
		* I.e., selects the **input files**
	* defines how **input files** are split and read.
	* Creates **InputSplits**.
	* Details are found [here](https://data-flair.training/blogs/hadoop-inputformat-types/).
* InputSplits
	* Logically represent the data which will be processed by an individual **Mapper**
		* This "logical representation" means "splits"
			* A "split" is data divided into "records"
				* A "record" is a [key-value pair](https://data-flair.training/blogs/key-value-pairs-hadoop-mapreduce/), which is later processed by a map task.
		* Doesn’t contain actual data, but a reference to the data.
			* Therefore, the "logical representation" is simply **instructions** on how data should be split into KVPs.
			* However, RecordReader is the component responsible for the actual splitting and creation of KVPs.
	* The number of InputSplits is equal to the number of map tasks.
	*  Details are found [here](https://data-flair.training/blogs/inputsplit-in-hadoop-mapreduce/).
* RecordReader
	* Communicates with the **InputSplit** to convert the data into KVPs.
		* This "communication" happens until the file reading is completed.
		* This "conversion" happens using a chosen **InputFormat** [type](https://data-flair.training/blogs/hadoop-inputformat/) (usually, [TextInputFormat](https://data-flair.training/blogs/hadoop-inputformat/#:~:text=4.2.-,TextInputFormat,-It%20is%20the))
		* These "key-value pairs" are created using byte offset (unique number) to each line present in the file. (in the case of TextInputFormat). These pairs are then sent to the **mapper** for further processing.
			* Also called "input key-value pairs"
* Mapper
	* Processes each input record (i.e., input KVP) from RecordReader.
	* Outputs KVPs called "**intermediate key-value pairs**".
		* These KVPs are first written to the local disk, not HDFS, as this is temporary data and writing on HDFS will create unnecessary copies.
		* These KVPs are then sent to the **combiner** for further processing.
* Combiner
	* Performs aggregations on the **mappers**’ output.
		* This aggregation minimizes the data transfer between mapper and **reducer**.
		* Example of MapReduce process without/with combiner ([source](https://data-flair.training/blogs/hadoop-combiner-tutorial/)):
		  
		  ![](Media-Temp/Pasted%20image%2020231111091026.png)
		  
		  Side note: it can be seen from the blue/green blocks above that each combiner runs individually on each mapper server.
		  
		* This aggregation is also KVPs that are passed to the **partitioner** for further work.
	* The combiner is an optional process.
* Partitioner
	* Optional: It is implemented when there are more than one reducer.
	* It translates the intermediate KVPs resulting from mappers (or the substitute intermediate KVPs from the combiners) to another set of KVPs, which are then assigned to corresponding reducers. ([source](https://data-flair.training/blogs/hadoop-partitioner-tutorial/))
		* This "translation" is done by computing a hash value for each key (of the input KVP).
		* This "assignment" is done by the **shuffling and sorting** step of the MapReduce job execution flow chart.
		* The "assignment step" is done by dividing these computed KVPs onto different reducers, such that each reducer has the same computed hash key in all of the KVPs sent to it.
			* Note 1: the number of partitioners is equal to the number of reducers available ([source](https://data-flair.training/blogs/hadoop-partitioner-tutorial/#:~:text=How%20many%20Partitioners%20are%20there%20in%20Hadoop)). 
	* The number of partitioners is equal to the number of reducers ([source](https://data-flair.training/blogs/hadoop-partitioner-tutorial/#:~:text=How%20many%20Partitioners%20are%20there%20in%20Hadoop)). 
	* A partitioner allows even distribution of the map (or combiner) output over the reducer, to balance the reducers' workload.
* Shuffling and sorting
	* This step is done by the **partitioner** ([source](https://www.quora.com/What-is-the-purpose-of-the-shuffle-operation-in-Hadoop-MapReduce#:~:text=Suffling%20happens%20in%20between%20map%20and%20reduce%20stage%20where%20data%20of%20same%20key%20needs%20to%20be%20taken%20to%20same%20reducer.%20It%20is%20done%20through%20the%20use%20of%20a%20partitioner))
	* Shuffling:
		* It is the process of transferring data from the mappers (or combiners) to reducers.
			* This "process" consists of the following logic:
				* Data from the mapper are grouped by the key.
				* They are then split among reducers.
					* **Sorting** of these keys happen while sending to reducers.
					* Example visualization, where the input is from the **mapper** step ([source](https://youtu.be/cvhKoniK5Uo?t=127)):
					  
					  ![mapreduce-shuffling-sorting-computerphile](Media-Temp/mapreduce-shuffling-sorting-computerphile.mp4)
					  
					  as a GIF:
					  
					  ![mapreduce-shuffling-sorting-computerphile](Media-Temp/mapreduce-shuffling-sorting-computerphile.gif)
					  
					* Another example, where the input is from the **combiner** step ([source](https://stackoverflow.com/questions/22141631/what-is-the-purpose-of-shuffling-and-sorting-phase-in-the-reducer-in-map-reduce)):
					  
					  ![](Media-Temp/Pasted%20image%2020231111102324.png)
					  
					* Note (unsure): <mark style="background: #D2B3FFA6;">Usually</mark>, every reducer obtains all KVPs <mark style="background: #D2B3FFA6;">with the same key</mark> (which was grouped-by in the shuffling step). However, sometimes, a reducer can contain KVPs with more than one key (like "node 2" in the gif above). 
						* When this is the case, each reducer employs ***reducer tasks*** for KVPs of each key. 
	* Sorting: 
		* Done simultaneously with the shuffling step, as seen in the gif above.
		* Done on the key, not the value.
			* KVPs are then "merged" in the reducers.
				* The notation of this merging can be seen in the gif above, for example: `<a,1>, <a,1>, <a,1>` will be `a(1,1,1)`
		* Can be also done on the value by passing a **secondary sorting** logic to each reducer. ([source](https://data-flair.training/blogs/shuffling-and-sorting-in-hadoop/#:~:text=5.%20Secondary%20Sorting%20in%20MapReduce))
* Reducer
	* Takes the KVPs from the **mapper** (or **combiner**) as input.
	* Runs a reducer function on each of them to the generate a KVP output, which is stored in **HDFS**.
	* Includes the following methods ([source](https://intellipaat.com/blog/interview-question/data-engineer-interview-questions/#30)):
		* **setup()**: Configures input data parameters and cache protocols.
		- **cleanup()**: Removes the temporary files stored.
		- **reduce()**: Called one time for every key.
	* Details are found [here](https://data-flair.training/blogs/reducer-in-hadoop-mapreduce/).
* RecordWriter
	* It writes these output KVPs from the **reducer** to the output files using one of the **OutputFormat** types.
* OutputFormat
	* Determines ***how*** the **RecordWriter** will write the KVPs to output files.


## NameNode vs DataNode

![|400](Media-Temp/Pasted%20image%2020231111133505.png)

([source](https://pediaa.com/what-is-the-difference-between-namenode-and-datanode-in-hadoop/))

![](Media-Temp/Pasted%20image%2020231111133706.png)

([source](https://dzone.com/articles/an-introduction-to-hdfs))

### What is a NameNode in HDFS?

[source](https://pediaa.com/what-is-the-difference-between-namenode-and-datanode-in-hadoop/#NameNode)

* NameNode stores this metadata of all the files in HDFS. 
	* Metadata includes file permission, names, and location of each block. 
		* A block is a minimum amount of data that can be read or write.
* NameNode keeps track of the files in all clusters
* NameNode maps these blocks to dataNodes. Furthermore, nameNode manages all other dataNodes. 
* **Master node** is an alternative name for nameNode.

### What is a DataNode in HDFS?

[source](https://pediaa.com/what-is-the-difference-between-namenode-and-datanode-in-hadoop/#DataNode)

* The nodes other than the nameNode are called dataNodes. 
* **Slave node** is another name for dataNode. 
* The data nodes store/retrieve/update **blocks** as instructed by the nameNode.
	* When Hadoop encounters a large file, it automatically slices the file into smaller chunks called blocks.
	* 

#### Hadoop Block 

[source](https://www.edureka.co/community/12658/block-scanner-hdfs)

* When Hadoop encounters a large file, it automatically slices the file into smaller chunks called blocks.
* A **Block scanner** runs periodically on every DataNode to verify whether the data blocks stored are corrupt or not.
	* This verification happens by performing a [checksum](https://www.educative.io/answers/how-does-checksum-work).
	* If a block is corrupted, the following happens:
		* The DataNode will report about the corrupted block to the NameNode.
		* The corrupted data block will not be deleted until the replication count of the correct replicas matches with the replication factor (3 by default).
	* Theis process allows HDFS to maintain the integrity of the data when a client performs a read operation.


### How NameNode and DataNode Communicate

[source](https://www.linkedin.com/pulse/block-report-heart-beat-naveen-n/)

The NameNode and the DataNode communicate via **messages**. There are two messages that are sent across the channel:

- Block reports:
	- Includes:
		- **Registration**: Data node registration information
		- **blocks**: Information about the blocks, which contains: 
			- block ID
			- block length
			- block generation timestamp
			- state of the block replica (finalized, waiting to be recovered, etc.)
	- This information is used by the Name Node for:
		- **Process first block report**: 
			- If it is a first time report for the newly registered Data Node, it just adds all the valid replicas. It ignores all the invalid blocks, till the next block report.
		- **For updating the information about blocks**: 
			- The (Data Node -> Blocks) map is updated in the Name Node. 
				- The new block report is compared with the old report and information about successful blocks, corrupted blocks, invalidated blocks etc. is updated
- Heartbeats
	- Includes:
		- **Registration**: Data node registration information
		- **Capacity**: Total storage capacity available at Data Node
		- **dfsUsed**: Storage used by HDFS
		- **remaining**: Remaining storage available for HDFS
		- **blockPoolUsed**: Storage used by the block pool**xmitsInProgress**: Number of transfers from this Data Node to others
		- **xceiverCount**: Number of active transceiver threads
		- **xmitsInProgress**: Number of transfers from this Data Node to others
		- **cacheCapacity**: Total cache capacity available at Data Node
		- **cacheUsed**: Amount of cache used
	- This information is used by the Name Node in the following ways:
		- **Health of the Data Node**: Should this data node be marked as dead or alive?
		- **Registration of new Data Node**: If this is a newly added Data Node, its information is registered
		- **Update the metrics of the Data Node**: The information sent in the heart beat is used for updating the metrics of the node
		- **Issue commands to the Data Node**: The Name Node can issue following commands to the Data Node, based on the information received in the heart beat: 
			- BlockRecoveryCommand (to recover specified blocks)
			- BlockCommand (for transferring blocks to another Data Node, for invalidating certain blocks)
			- Cache/Uncache (commands for caching / uncaching the blocks)

## Hadoop Streaming

[source](https://data-flair.training/blogs/hadoop-streaming/)

Regarding Hadoop streaming:
* It is a Hadoop utility that allows enables us to create or run MapReduce scripts in any language, as mapper/reducer
	* By default, the Hadoop MapReduce framework is written in Java and provides support for writing map/reduce programs in Java only, so Hadoop streaming alleviates this issue.
* It uses Unix streams as the interface between the Hadoop and our MapReduce program so that we can use any language which can read/write from/to standard input/output.

Visualization:

![](Media-Temp/Pasted%20image%2020231111134634.png)

([same source](https://data-flair.training/blogs/hadoop-streaming/))

Hadoop Streaming with regards to the MapReduce Job Execution Flow:

![](Media-Temp/Pasted%20image%2020231111134742.png)


# Big Data's Five V's

[source](https://www.theknowledgeacademy.com/blog/4-vs-of-big-data/)

* Volume
	* Trillions of gigabytes of data are created worldwide every day, and the numbers will only rise in the years to come. 
	* Most of this massive quantity of data generated daily is due to the widespread use of mobile phones.
* Velocity
	* It refers to the speed at which data is generated and processed. 
		* For example, the data is processed instantaneously if you send a text or post anything on social media.
* Variety
	* Data comes in many types.
* Veracity
	* Refers to the data's trustworthiness.
	* Denotes the data's accuracy and quality.
* Value
	* Is often not mentioned compared to the former 4 characteristics.
	* Refers to the data's significance.
	* Data, when organized and processed in the right way, can be converted into valuable information.

# What is ETL?

* ETL stands for Extract, Transform, Load. 
* It is a process used in data engineering to:
	* Extract data from source systems
	* Transform it into a suitable format
	* Load it into a target system, typically a data warehouse or a data lake. 
* It allows organizations to collect, clean, and transform data from various sources <mark style="background: #FF5582A6;">into a structured and usable format for analysis</mark>. 
* Without ETL, data would remain in its raw, often unstructured state, making it difficult to analyze and gain insights from.

![](Media-Temp/Pasted%20image%2020231111161123.png)

([source](https://ilegra.com/blog/we-need-to-talk-about-data-build-tool-from-etl-to-dbt/))

with [data build tool](https://ilegra.com/en/we-need-to-talk-about-data-build-tool/) (dbt):

![](Media-Temp/Pasted%20image%2020231111161137.png)


# Data Warehouse (DWH) vs Data Lakes

[source](https://intellipaat.com/blog/interview-question/data-engineer-interview-questions/#21)

* A data warehouse is a structured/organized repository of data. 
	* Stores structured data and enforces schema consistency.
	* Designed for querying and reporting.
* A data lake is a more flexible storage system that can handle structured, semi-structured, and unstructured data. 
	* Allows for data to be ingested without a predefined schema.
	* Designed for big data (i.e., data storage) and data exploration. 

![](Media-Temp/Pasted%20image%2020231111162233.png)

([source](https://datasciencedojo.com/blog/data-lake-vs-data-warehouse/))

# What is the CAP theorem, and how does it relate to distributed systems in data engineering?

[source](https://intellipaat.com/blog/interview-question/data-engineer-interview-questions/#23)

* The CAP theorem, also known as Brewer’s theorem, states that in a distributed system, it’s impossible to achieve all three of the following simultaneously:
	*  Consistency
	* Availability
	* Partition tolerance
* Only two qualities can be present at the expense of the third. 
* This theorem is critical in distributed systems because it helps in making design trade-offs. 
	* For example, in the face of network partitions (P), you might have to choose between ensuring strong data consistency (C) or high availability (A).
* More details [here](https://docs.google.com/document/d/1g5eEh2P-7rEl01lEY5yctjD5gEuqgWrq87ZKIOMyDQs/edit#heading=h.q3bct89ssw25).

## What is the purpose of partitioning in distributed data processing frameworks like Hadoop or Spark?

[source](https://intellipaat.com/blog/interview-question/data-engineer-interview-questions/#24)

Definition:
* Partitioning divides a large dataset into smaller, manageable subsets called partitions.

Uses:
* It helps in parallelizing data processing tasks across cluster nodes.
	* each node can work on its partition concurrently.
* Reduces data movement and improves data locality.


# Data Serialization

same source

* Data serialization is the process of **converting** complex data structures or objects **into a format** that can be **easily stored, transmitted**, or reconstructed.
* It allows data to be easily read.
* Helps in data interchange between different systems, by ensuring data compatibility.
	* For example, between a producer and a consumer.
		* Example of a "producer and consumer" scenario: In data processing, producers generate data, which is then placed into a shared data store or message queue. Consumers then retrieve the data and perform processing, such as aggregation or transformation. This pattern is often used for processing large volumes of data in real time. Frameworks like Apache Spark do this. ([source](https://medium.com/@karthik.jeyapal/system-design-patterns-producer-consumer-pattern-45edcb16d544#:~:text=Data%20Processing,Think%20Apache%20Spark))
* Common serialization formats include JSON, Avro, and Parquet.

# Data Skew

In the context of distributed data processing, data skew:
* Refers to an imbalance in the distribution of data across partitions or nodes in a distributed system.
	* So some nodes taking significantly longer to process their data.
* Can be mitigated by employing techniques like:
	* data Shuffling
	* custom partitioning strategies
	* dynamic load balancing
	* using appropriate data structures and algorithms (DSA).

# Data Lineage

Data lineage:
* Refers to the **tracking of data as it moves through** various stages of **a data pipeline** or system.
* Helps in understanding where the data is produced, how it’s transformed, and where it’s consumed.
* Helps in ensuring compliance, as it provides a clear audit trail for data, ensuring data governance and regulatory requirements are met.
* Aids in debugging, troubleshooting, and optimizing data pipelines.


