
# Data Pipeline Architectures

[amazing source](https://www.montecarlodata.com/blog-data-pipeline-architecture-explained/)




# MDS Definition

[source](https://towardsdatascience.com/modern-or-not-what-is-a-data-stack-e6e09e74ae7f)

Definition:
* A "data stack" in a business context is the <mark style="background: #FF5582A6;">combination of multiple technologies that allow companies to make use of data for their decision making</mark>.
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

# MDS Core Blocks

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


We'll now explain each of the core blocks presented in the first diagram of this section.

## Extract

* **Data from a variety of sources are extracted**. 
	* This can be done via scripts written in Python, or via native connectors offered by service providers. 
* The best suited solution will depend on the technological choices made but also on **the way raw data can be extracted**: 
	* **API** (probably the easiest way)
	* secure file transfer protocol (**SFTP**)
	* **web scrapping**, etc.

## Load

* The data extracted should then be stored in the appropriate infrastructure. 
* **Use** data **lakes** and/or data warehouses (**DTW**) **to load data into (a) central place(s)**. 
* Interestingly, some providers like Databricks or Snowflake tend to offer a **third-way** with innovative data platforms that **combine** the advantages of both the data lake (**unstructured and large data**) and the data warehouse (**structured and curated data**).

## Transform

* Transform the data before it can be exploited for further analyses. 
* This is where data is processed through several layers with two main goals:
	* **Make data clean** 
		* (e.g. avoiding wrong values, standardizing formats)
	* **Make data usable** 
		* (e.g. by consolidating data from multiple sources, aggregating it)

## Leverage

* **Data Output** is seen in this block.
	* It can be reports and interactive dashboards but also ad-hoc analyses, data discovery tool, etc.
* This data is what the stakeholders see.

## Store

* Storage is a foundational element in MDS.
* It is where **storage gets configured/adapted to the needs of the whole data stack** in terms of volume, refresh frequency, types of usage, etc.
* This element enables the [load](#Load) and [transform](#Transform) blocks to store/transform data.

## Govern

* Governance is a foundational element in MDS.
* It is the "maintenance" part of the MDS.
	* All other blocks constitute the "construction part" of the MDS.
* Data Governance Tools (DGT) maintain data quality across all blocks to ensure that data is correctly treated from its source to its final destination.

# MDS Considerations

Regarding the choice of the technologies used in each MDS block, consider the following:
* "all in one place" vs "one tool per specific task"
* "doing on your own" vs "delegating implementation to providers"
	* The former is usually done using open-source technologies.
	* The latter can result in a [Vendor Lock-in](../../../Business/Economics/Economic%20Terms.md#Vendor%20Lock-in).
* Staff capabilities.
* Cost constraints.
* Time constraints.

