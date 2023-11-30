
# Data Pipeline Architectures

[amazing source](https://www.montecarlodata.com/blog-data-pipeline-architecture-explained/)

Note: for most of the following sections, we'll refer to data pipeline architectures as (DPAs), even though this isn't a common abbreviation.

## Definition

Data pipeline architecture:
* Is the process of designing **how data is surfaced from its source system to the consumption layer**. 
* Is **not** a linear movement of data from source A to target B, 
	* but rather consist of a series of highly complex and interdependent processes. 
	* For example, data may be extracted from multiple sources, reorganized, and joined at different times before ultimately being served to its final destination.
* Involves (in some order):
	* **extraction** 
		* from a source system
	* **transformation** 
		* where data is combined with other data and put into the desired format
	* **loading** 
		* into storage where it can be accessed
	* This is commonly abbreviated and referred to as an **ETL or ELT pipeline**.
* Is useful because:
	* It solves the 5 v’s posed by big data
	* It fulfills use case requirements while being cost/maintenance efficient.

Visualization of the data pipeline paradigm:

![](Media-Temp/Pasted%20image%2020231126040134.png)

Notes:
* "E" - Extract
* "I" - Integrate
* "T" - Transform
* "L" - Load

## Designs Overview

![](Media-Temp/Pasted%20image%2020231126040547.png)

Below, we'll talk about the [5 Data pipeline architecture designs and their evolution](https://www.montecarlodata.com/blog-data-pipeline-architecture-explained/#5-data-pipeline-architecture-designs-and-their-evolution)

### ETL

Visualization of ETL [DPA](#Data%20Pipeline%20Architectures) design:

![](Media-Temp/Pasted%20image%2020231126040647.png)

* **The Hadoop era**, roughly 2011 to 2017, arguably ushered in big data processing capabilities to mainstream organizations. 
* Data was primarily hosted in on-premises databases with non-scalable storage. 
* Despite **Hadoop’s** parallel and distributed processing, compute was a limited resource as well. 
	* Therefore, <mark style="background: #ADCCFFA6;">storage and computing (processing) were coupled together</mark>.
* As a result, data engineers spent considerable time modeling data and optimizing queries to fit within these constraints. 
* [DPA](#Data%20Pipeline%20Architectures) typically <mark style="background: #ADCCFFA6;">consisted of hardcoded pipelines that cleaned, normalized, and transformed the data prior to loading into a database using an ETL pattern</mark>.
* Some companies still apply this ETL pattern in the cloud,
	* particularly for production pipelines where [data contracts](https://www.montecarlodata.com/blog-data-contracts-explained/) can help reduce data downtime.

### ELT (Modern Data Stack, MDS)

Visualization of ELT [DPA](#Data%20Pipeline%20Architectures) design:

![](Media-Temp/Pasted%20image%2020231126041539.png)

* **The modern data stack era**, roughly 2017 to present data, <mark style="background: #ADCCFFA6;">adopted cloud computing and modern data repositories that decoupled storage from compute</mark> such as [data warehouses, data lakes, and data lakehouses](https://www.montecarlodata.com/blog-data-lake-vs-data-warehouse/). 
	* This also led to alleviating cost and physical compute/storage limitations.
	* Therefore, data engineers started to optimize [DPA](#Data%20Pipeline%20Architectures) for speed and agility. 
		* Data could now be extracted and loaded prior to being transformed for its ultimate use (hence, ELT instead of ETL).
* Due to the <mark style="background: #ADCCFFA6;">scale/flexibility of ELT</mark>, companies were able to focus on:
	* widespread analytics
	* experimentation
	* machine learning applications

#### ETL vs ELT

[source 1](https://www.montecarlodata.com/blog-etl-vs-elt/), [source 2](https://blog.hubspot.com/website/etl-vs-elt) (which used [this](https://learn.microsoft.com/en-us/azure/architecture/data-guide/relational-data/etl) Microsoft source), [source 3](https://www.guru99.com/etl-vs-elt.html)

Visualizations to illustrate the differences:

ETL:

![](Media-Temp/Pasted%20image%2020231126064059.png)

ELT:

![](Media-Temp/Pasted%20image%2020231126064142.png)

ETL vs ELT:

![](Media-Temp/Pasted%20image%2020231126064344.png)

Detailed differences:

| Parameters                                   | ETL                                                                                                          | ELT                                                                                             |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| **Process**                                  | Data is transformed at staging server and then transferred to Datawarehouse DB.                              | Data remains in the DB of the [Datawarehouse](https://www.guru99.com/data-warehousing.html). ✅ |
| **Code Usage**                               | Used for<br><br>- Compute-intensive Transformations<br>- Small amount of data                                | Used for High amounts of data ✅                                                                |
| **Transformation**                           | Transformations are done in ETL server/staging area.                                                         | Transformations are performed in the target system                                              |
| **Time-Load**                                | Data first loaded into staging and later loaded into target system. Time intensive.                          | Data loaded into target system only once. Faster.✅                                             |
| **Time-Transformation**                      | ETL process needs to wait for transformation to complete. As data size grows, transformation time increases. | In ELT process, speed is never dependant on the size of the data. ✅                            |
| **Time- Maintenance**                        | It needs highs maintenance as you need to select data to load and transform.                                 | Low maintenance as data is always available.✅                                                  |
| **Implementation Complexity**                | At an early stage, easier to implement.✅                                                                    | To implement ELT process organization should have deep knowledge of tools and expert skills.    |
| **Support for Data warehouse**               | ETL model used for on-premises, relational and structured data.                                              | Used in scalable cloud infrastructure which supports structured, unstructured data sources. ✅  |
| **Data Lake Support**                        | Does not support.                                                                                            | Allows use of Data lake with unstructured data.✅                                               |
| **Complexity of Dealing with Relevant Data** | The ETL process loads only the important data, as identified at design time.✅                               | This process involves development from the output-backward and loading only relevant data.      |
| **Cost**                                     | High costs for small and medium businesses.                                                                  | Low entry costs using online Software as a Service Platforms.✅                                 |
| **Lookups**                                  | In the ETL process, both facts and dimensions need to be available in staging area.                          | All data will be available because Extract and load occur in one single action.✅               |
| **Aggregations**                             | Complexity increase with the additional amount of data in the dataset.                                       | Power of the target platform can process significant amount of data quickly.✅                  |
| **Calculations**                             | Overwrites existing column or Need to append the dataset and push to the target platform.                    | Easily add the calculated column to the existing table.✅                                       |
| **Maturity**                                 | The process is used for over two decades. It is well documented and best practices easily available.✅       | Relatively new concept and complex to implement.                                                |
| **Hardware**                                 | Most tools have unique hardware requirements that are expensive.                                             | Being Saas, hardware cost is not an issue.✅                                                    |
| **Support for Unstructured Data**            | Mostly supports relational data                                                                              | Support for unstructured data readily available.✅                                              |
| **Security & Compliance**                    | Easy (as sensitive data can be removed or encrypted prior to storage in data warehouse).✅| Difficult (as more steps may be required to ensure compliance with protocols)|

Therefore, we can see that ELT is better/faster/more-flexible than ETL in most aspects **except** the following:
* Implementation/relevant-data complexity
	* The architecture is initially easier to implement and the important data is identified at design time.
* Maturity
	* It is well documented and best practices are well-established.
* Security
	* Sensitive data are dealt with prior to storage in a data warehouse.

Use cases: external factors based on business needs dictates which is better to use, but in general:
* Use ETL when:
	* You have intensive data transformations that rarely vary.
	* You have data that contains a wealth of personal identifying information (PII).
	* Systems are already built around legacy architecture.
* Otherwise, ELT is preferred.

#### MDS Definition

[source](https://towardsdatascience.com/modern-or-not-what-is-a-data-stack-e6e09e74ae7f)

Definition:
* A "data stack" in a business context is the <mark style="background: #FF5582A6;">combination of multiple technologies that allow companies to make use of data for their decision making</mark>.
* Alternatively, it refers to the multiple modular SaaS solutions that comprise the [data platform](https://www.montecarlodata.com/blog-what-is-a-data-platform-and-how-to-build-one/) and pipeline ([source](<https://www.montecarlodata.com/blog-data-pipeline-architecture-explained/#:~:text=The%20term%20modern%20data%20stack%20refers%20to%20the%20multiple%20modular%20SaaS%20solutions%20that%20comprise%20the%20data%20platform%20and%20pipeline%20(more%20on%20those%20later).>)).
* The "modern" part refers to developments in recent years, in particular:
	* **The rise of cloud platforms** 
		* that offer cheaper and more flexible pricing solutions to store large volumes of data.
	- **The emergence of new data companies** 
		- that offer a higher level of expertise in a specific part of a company’s data stack.

In short, a "modern data stack" (MDS) is a "data stack" with special characteristics:
* Cheaper and more **efficient storage solutions** for high volumes of data 
	* which tends to favor a shift from ETL to ELT.
		* E - Extract
		* T - Transform
		* L - Load
* Possibility to **combine several data technologies** in order to avoid the "all-in-one" costly solutions.
	* Note 1: the traditional "all-in-one" solutions tend to have a worse price-quality ratio as they have a more generalist approach compared to these emerging data companies.
	* Note 2: combining several data technologies is called a "one tool per specific task" solution.

#### MDS Core Blocks

To perform all the necessary tasks for data management at a company, any data stack must include the following blocks:

![](Media-Temp/Pasted%20image%2020231125140856.png)

Very high-level view of example technologies of each block:

![](Media-Temp/Pasted%20image%2020231125160653.png)

High-level view of example technologies of each block ([source](https://www.altexsoft.com/blog/modern-data-stack/)):

![](Media-Temp/Pasted%20image%2020231125160507.png)

Low-level view of example technologies of each block ([source](https://tanay.substack.com/p/understanding-the-modern-data-stack)):

![](Media-Temp/Pasted%20image%2020231125160826.png)

Lower-level view of example technologies of each block ([source](https://medium.com/vertexventures/thinking-data-the-modern-data-stack-d7d59e81e8c6)):

![](Media-Temp/Pasted%20image%2020231125162131.png)

(Side note: I've highlighted key terms/technologies that I've personally heard of/used.)

In-depth level view of example technologies of each block ([source](https://www.timextender.com/blog/data-empowered-leadership/the-modern-data-stack-is-broken)):

![](Media-Temp/Pasted%20image%2020231125163538.png)


Example technologies in the ML/AI/Data (MAD) landscape can be found [here](https://mattturck.com/wp-content/uploads/2021/12/2021-MAD-Landscape-v3.pdf) ([source](https://mattturck.com/data2021/#:~:text=FULL%20LIST%20IN%20SPREADSHEET%20FORMAT%3A%C2%A0%20despite%20how%20busy%20the%20landscape%20is%2C%20we%20cannot%20possibly%20fit%20in%20every%20interesting%20company%20on%20the%20chart%20itself.%C2%A0%20As%20a%20result%2C%20we%20have%20a%20whole%20spreadsheet%20that%20not%20only%20lists%20all%20the%20companies%20in%20the%20landscape%2C%20but%20also%20hundreds%20more%20%E2%80%93%20CLICK%20HERE)) (extremely detailed).

A detailed sheet of most technology tools and their categories/sub-categories can be found [here](https://airtable.com/appqPmTMFrs1nssms/shrXVKG1JI9EHyoFE/tbl8oBlGhRFr9iBBY). I suggest using this when searching about a specific technology (e.g., spark) to find its category/sub-category.

We'll now explain each of the core blocks presented in the first diagram of this section.

##### Extract

* **Data from a variety of sources are extracted**. 
	* This can be done via scripts written in Python, or via native connectors offered by service providers. 
* The best suited solution will depend on the technological choices made but also on **the way raw data can be extracted**: 
	* **API** (probably the easiest way)
	* secure file transfer protocol (**SFTP**)
	* **web scrapping**, etc.

##### Load

* The data extracted should then be stored in the appropriate infrastructure. 
* **Use** data **lakes** and/or data warehouses (**DTW**) **to load data into (a) central place(s)**. 
* Interestingly, some providers like Databricks or Snowflake tend to offer a **third-way** with innovative data platforms that **combine** the advantages of both the data lake (**unstructured and large data**) and the data warehouse (**structured and curated data**).

##### Transform

* Transform the data before it can be exploited for further analyses. 
* This is where data is processed through several layers with two main goals:
	* **Make data clean** 
		* (e.g. avoiding wrong values, standardizing formats)
	* **Make data usable** 
		* (e.g. by consolidating data from multiple sources, aggregating it)

##### Leverage

* **Data Output** is seen in this block.
	* It can be reports and interactive dashboards but also ad-hoc analyses, data discovery tool, etc.
* This data is what the stakeholders see.

##### Store

* Storage is a foundational element in MDS.
* It is where **storage gets configured/adapted to the needs of the whole data stack** in terms of volume, refresh frequency, types of usage, etc.
* This element enables the [load](#Load) and [transform](#Transform) blocks to store/transform data.

##### Govern

* Governance is a foundational element in MDS.
* It is the "maintenance" part of the MDS.
	* All other blocks constitute the "construction part" of the MDS.
* Data Governance Tools (DGT) maintain data quality across all blocks to ensure that data is correctly treated from its source to its final destination.

#### MDS Considerations

Regarding the choice of the technologies used in each MDS block, consider the following:
* "all in one place" vs "one tool per specific task"
* "doing on your own" vs "delegating implementation to providers"
	* The former is usually done using open-source technologies.
	* The latter can result in a [Vendor Lock-in](../../../Business/Economics/Economic%20Terms.md#Vendor%20Lock-in).
* Staff capabilities.
* Cost constraints.
* Time constraints.

### Streaming

![](Media-Temp/Pasted%20image%2020231126170336.png)

Streaming DPA:
* The pattern can be described as 
	* **stream**
		* Thus, inability to fully validate data quality or model the data.
		* However, gives it advantage of dealing with near-real time data, while previous DPAs dealt with batch data pipelines.
	* collect
	* process
	* store
	* analyze
* Runs parallel to [MDS](#ETL) pipelines.
* Used mainly for data science or machine learning use cases.

### Zero ETL

![](Media-Temp/Pasted%20image%2020231126173729.png)

Zero-ETL:
* Is a set of integrations that eliminates or minimizes the need to build ETL data pipelines.
* Is **transferred directly** from one system to another **without** the need for any intermediary steps to **transform** or clean the data. ([source](https://medium.com/starschema-blog/so-whats-all-this-talk-about-zero-etl-integration-aa3b0ca9612b))
	* This can be useful when no complex data transformation or manipulation is needed.
* Is also considered to be a data replication tool.
	* A replication tool will **transfer data in near-real-time** without requiring any intermediate processing or manipulation.
* Lacks in data governance
	* As it relies on the systems involved in the transfer to handle these tasks.
* Is difficult to integrate with other systems outside the ecosystem due to relying on direct data transfer.

Zero-ETL use case example:
* 