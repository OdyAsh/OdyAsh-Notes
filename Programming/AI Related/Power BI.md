# Power BI Basics
## Power BI Core Components

[Microsoft Source](https://learn.microsoft.com/en-us/training/modules/get-started-with-power-bi/5-summary-cleanup)

**Microsoft Power BI** is a comprehensive set of software tools, apps, and connectors that transform data into interactive insights. It accommodates various data sources and can be tailored to match your organization's complexity.

- **Power BI Desktop** for authoring reports made up of datasets and visualizations.
- **Power BI service** for creating dashboards from published reports and distributing content with apps.
- **Power BI Mobile** for on-the-go access to the Power BI service content, designed for mobile.

## Selecting a Storage Mode

[M source](https://learn.microsoft.com/en-us/training/modules/get-data/6-storage-mode)

The most popular way to use data in Power BI is to **import it into a Power BI dataset**. Importing the data means that the data is stored in the Power BI file and gets published along with the Power BI reports.

The three different types of storage modes you can choose from:
- Import
	- Create a local Power BI copy of your datasets from your data source. You can use all Power BI service features with this storage mode, including Q&A and Quick Insights. Data refreshes can be scheduled or on-demand.
		- This "local copy" is stored using Microsoft's ***VertiPaq*** compression engine; As soon as the data is loaded in Power BI, Vertipaq engine performs a series of algorithms on the data to compress it as much as possible. This optimizes the memory footprint and DAX query time in Power BI ([source](https://powerbitraining.com.au/vertipaq-engine-and-best-practices-in-dax/#:~:text=Vertipaq%20is%20the%20compression%20engine,query%20time%20in%20Power%20BI.)). 
- DirectQuery
	- query the specific tables that you'll need by using native Power BI queries, and the required data will be retrieved from the underlying data source.
- Dual (Composite)
	- identify some data to be directly imported and other data that must be queried. Any table that is brought in to your report is a product of both Import and DirectQuery modes. Using the Dual mode allows Power BI to choose the most efficient form of data retrieval.

## Reports vs Dashboards vs Apps
[Microsoft source 1](https://learn.microsoft.com/en-us/training/modules/get-started-with-power-bi/3-building-blocks-of-power-bi) and [2](https://learn.microsoft.com/en-us/training/modules/get-started-with-power-bi/4-exercise-touring-and-using-power-bi)
### Reports vs Dashboards

![[Pasted image 20230929210107.png]]
([source](https://learn.microsoft.com/en-us/power-bi/create-reports/service-dashboards))

![[Pasted image 20230929210329.png]]
([source](https://k21academy.com/microsoft-azure/data-analyst/dashboards-vs-reports-in-power-bi/))

### Dashboards vs Apps

![[Pasted image 20230929210445.png]]
([source](https://www.coatesdatastrategies.com/blog/why-use-a-power-bi-app))

A Dashboard:
* Is built from parts of other Reports, "Tiles" which give access to the full Report
* Can be used as a "table of contents" or "1,000 foot view" of the important parts of your Reports.
* Is not paginated, but built as an infinite scroll.
* Can fit well on a mobile device by default.
* Can have "Tiles" of text etc. which when clicked will go to other web resources.
* Cannot be shared via "Teams"
* Is **shared** using the "classic" sharing mechanism, you have to enter **each recipient individually**.
* **Updates when the underlying Report Visual or data changes**.

An App:
* Is **built from multiple Reports and Dashboards** within a single Workspace.
* Can have a "Navigation" menu on the left which can use show different Report names in a specified order.
* Copies the Report into the App, (but not the Dataset) so changes to the Report can be made without the App reflecting them. You need to Update the App for changes to show. This allows "staging" of changes.
* Can be shared via "Teams"
* Can be shared to AD security groups and distribution lists, and Microsoft 365 Groups.
* If you've got one or two reports then a Dashboard may work well for you.
* But if you have multiple reports, to be shared with multiple groups of users you really need an App. Apps also provide a simple change mechanism, **App users won't see Report changes until you update the App, so you can work on the next version without users seeing the changes. But a Dashboard will update as soon as you have made a change to the Reports that feed it**.

Put briefly, Dashboards are OK for small implementations, but Apps are more scalable, secure and manageable for larger solutions.
([source](https://community.fabric.microsoft.com/t5/Service/Power-BI-dashboard-vs-Power-BI-app/m-p/2738348))

### Visualizing The Three

App example:
![[Pasted image 20230929211052.png]]
([source](https://learn.microsoft.com/en-us/training/modules/get-started-with-power-bi/4-exercise-touring-and-using-power-bi))

Dashboard example is the same as the image above, but only the dashboard tab:
![[Pasted image 20230929211103.png]]

Report example:
![[Pasted image 20230929211134.png]]
(note: the "Top 100 Contributors" is a page in the report, so the report contains 6 pages in total)

# Parameter Value Types

([source](https://www.youtube.com/watch?v=twBUmqVOGgg))
There are two types: 
* Power BI Query Parameters.
	* By changing these you can **change the data that is loaded** in it your Power BI model.
* Parameters used in Power BI Reports.
	* by changing these parameters users can **change what is shown on the report**.
	* Example ([source](https://www.youtube.com/watch?v=1eurc0EY2Xg)):
	  ![[Pasted image 20231014212908.png]]
	  then:
	  ![[Pasted image 20231014212949.png]]
	  then, repeat the two images' steps above to create `Y Axis` parameter. Then, create an empty bar chart visual, and the parameters as fields:
	  ![[Pasted image 20231014213104.png]]
	  Result:
	  ![[Pasted image 20231014213148.png]]


# Custom Invoke Functions

https://www.youtube.com/watch?v=ynr9VE9QQXc

# Change The Source File

[M source](https://learn.microsoft.com/en-us/training/modules/get-data/2-data-files#:~:text=Change%20the%20source,select%20Close.)
# Querying Methods

## SQL vs T-SQL

([source](https://pediaa.com/what-is-the-difference-between-sql-and-tsql/))
![[Pasted image 20230930081913.png]]

# Import Errors

[Microsoft source](https://learn.microsoft.com/en-us/training/modules/get-data/8-performance-issues)

## Data Type Errors

Sometimes, when you import data into Power BI, the columns appear blank. This situation happens because of an error in interpreting the data type in Power BI. The resolution to this error is unique to the data source. For instance, if you're importing data from SQL Server and see blank columns, you could try to convert to the correct data type in the query.

Instead of using this query:

`SELECT CustomerPostalCode FROM Sales.Customers`

Use this query:

`SELECT CAST(CustomerPostalCode as varchar(10)) FROM Sales.Customers`

By specifying the correct type at the data source, you eliminate many of these common data source errors.

You may encounter different types of errors in Power BI that are caused by the diverse data source systems where your data resides.

If you experience an error not covered, you can search [Microsoft documentation](https://learn.microsoft.com/en-us/power-query/dealing-with-errors) for the error message, and the resolution you need.

# Power Query Editor

## Applied Steps
### Recording Applied Steps

When you work in Power Query Editor, all steps that you take to shape your data are recorded. Then, each time the query connects to the data source (i.e., **scheduled data refresh**), it automatically applies your steps, so your data is always shaped the way that you specified. Power Query Editor only makes changes to a particular view of your data, so you can feel confident about changes that are being made to your original data source.
([Microsoft source](https://learn.microsoft.com/en-us/training/modules/clean-data-power-bi/2-shape-data#:~:text=When%20you%20work,original%20data%20source.))

### M Code

[Microsoft source](https://learn.microsoft.com/en-us/training/modules/clean-data-power-bi/7-advanced-editor)

Each cleaning step that you made was likely created by using the graphical interface, but Power Query uses the M language behind the scenes.
After creating steps to clean data, select the **View** ribbon of Power Query and then select **Advanced Editor**:
![[Pasted image 20230930120652.png]]
You should see something like this:
![[Pasted image 20230930120706.png]]

You might notice that M code is written top-down. Later steps in the process can refer to previous steps by the variable name to the left of the equal sign. Be careful about reordering these steps because it could ruin the statement dependencies. Write to a query formula step by using the **in** statement. Generally, the last query step is used as the **in final data set** result.


## Pivots

Pivot meaning: **Moving rows to columns or columns to rows** (or "pivoting") to see different summaries of the source data. Filtering, sorting, grouping, and conditionally formatting the most useful and interesting subset of data enabling you to focus on just the information you want. ([source](https://support.microsoft.com/en-gb/office/overview-of-pivottables-and-pivotcharts-527c8fa3-02c0-445a-a2db-7794676bce96#:~:text=Moving%20rows%20to%20columns%20or,just%20the%20information%20you%20want.))

pivot visualization:
![[Pasted image 20230930112405.png]]
([source](http://jalammar.github.io/visualizing-pandas-pivoting-and-reshaping/))

Regarding [Microsoft source](https://learn.microsoft.com/en-us/training/modules/clean-data-power-bi/2-shape-data):

### Unpivot Columns

If Pivot dataset is like this:

![[Pasted image 20230930112607.png]]

Then to unpivot it, select the **Transform** tab in Power Query, and then select **Unpivot**:
![[Pasted image 20230930112648.png]]

### Pivot Columns

To pivot a flat file (dataset):
first select column that you'd like to be aggregated, in the case below, "Subcategory Name":
![[Pasted image 20230930112845.png]]
then:
![[Pasted image 20230930112732.png]]
then:
![[Pasted image 20230930113000.png]]
then you'll see it transformed like so:
![[Pasted image 20230930113130.png]]


## Combining Tables

[Microsoft source](https://learn.microsoft.com/en-us/training/modules/clean-data-power-bi/5-combine-tables)

### Merge Queries

Similar to SQL JOIN operation.
Go to **Home** on the Power Query Editor ribbon and select the **Merge Queries** drop-down menu, where you can select **Merge Queries as New**.

### Append Queries

Case scenario: you have tables that contain certain columns that are common in all the tables, for example, (id, company, name, phone). If this is the case:
Before you begin combining queries, you can remove extraneous columns that you don't need for this task from your tables. To complete this task, format each table to have only four columns with your pertinent information, and rename them so they all have the same column headers. The following is visualization of the tables after they've been renamed to have the same 4 column names:
![[Pasted image 20230930114800.png]]

Then, on the **Home** tab on the Power Query Editor ribbon, select the drop-down list for **Append Queries**:
![[Pasted image 20230930114834.png]]

Then, the final appended table will look like this:
![[Pasted image 20230930114849.png]]

## Profiling Data to Find Data Anomalies and Data Statistics

[Microsoft source](https://learn.microsoft.com/en-us/training/modules/clean-data-power-bi/6-profile-data)

Power Query Editor determines data anomalies by using the **Column Distribution** feature.
![[Pasted image 20230930120218.png]]

By default, Power Query examines the first 1000 rows of your data set. To change this, <mark style="background: #D2B3FFA6;">select the profiling status in the status bar and select Column profiling based on entire data set</mark>.

Distinct values are all the different values in a column, including duplicates and null values, while unique values do not include duplicates or nulls. Therefore, **distinct** in this table tells you the total count of how many values are present, while **unique** tells you how many of those values only appear once.

Side note: before doing all of this, it is important to see the underlying data structures that data is organized in which can be done by clicking **Model** tab see something like this:
![[Pasted image 20230930115755.png]]

# Power BI Model Terms

[Microsoft source](https://learn.microsoft.com/en-us/training/modules/choose-power-bi-model-framework/2-describe-power-bi-model-fundamentals)

understand these terms in order to choose the appropriate model framework:

- Data model
- Power BI dataset
- Analytic query
- Tabular model
- Star schema design
- Table storage mode
- Model framework

## Data Model (i.e., Model or Semantic Model)

* A Power BI data model is a query-able data resource that’s optimized for analytics.
* Reports can query data models by using one of two analytic languages:
	* Data Analysis Expressions (DAX)
	* Multidimensional Expressions (MDX)
* Created in Power BI Desktop

## Power BI Dataset

* It is a data model, but when published to a workspace in the Power BI service.
	* Note: Not all datasets originate from data models developed in Power BI Desktop. Some datasets represent connections to external-hosted models
* It is a source of data for visualizations in Power BI reports and dashboards.

## Analytic Query

* To visualize data, Power BI sends an analytic query.
	* An analytic query produces a query result from a model that’s easy for a person to understand, especially when visualized.

An analytic query has three phases that are executed in this order:
1. Filter
2. Group
3. Summarize

### Filtering

* **Filtering** (sometimes known as slicing) narrows down on a subset of the model data.
* **When the model enforces row-level security (RLS), it applies filters to model tables to restrict access to specific data. Measures, which summarize model data, can also apply filters.

### Grouping

**Grouping** (sometimes known as dicing) divides query result into groups. Each group is also a filter, but unlike the filtering phase, filter values are visible in the query result. For example, grouping by customer filters each group by customer.

### Summarizing

**Summarization** produces a single value result. Typically, a report visual summarizes a numeric field by using an aggregate function. Aggregate functions include sum, count, minimum, maximum, and others. You can achieve simple summarization by aggregating a column, or you can achieve complex summarization by creating a measure using a DAX formula.

### Example

Consider an example: A Power BI report page includes a slicer to filter by a single year. There’s also a column chart visual that shows quarterly sales for the filtered year.

![Screenshot of the Power BI report described in the previous paragraph.](https://learn.microsoft.com/en-us/training/wwl-data-ai/choose-power-bi-model-framework/media/model-frameworks-analytic-query-example.png)

In this example, the slicer **filters** the visual by calendar year 2021. The column chart **groups** by quarters (of the filtered year). Each column is a group that represents a visible filter. The column heights represent the **summarized** sales values for each quarter of the filtered year.

## Tabular model

A Power BI model is a tabular model. A tabular model comprises one or more tables of columns. It can also include relationships, hierarchies, and calculations.

## Star schema design

* To produce an optimized and easy-to-use **tabular** model, we recommend you produce a star schema design.
* classify model tables as either dimension or fact.
	* Dimension tables describe business entities
		* Entities can include products, people, places, and concepts including time itself.
	* Fact tables store observations or events
		* for example, sales orders, stock balances, exchange rates, or temperature readings.
		* contains dimension key columns that relate to dimension tables, and numeric measure columns.
	* A fact table forms the center of a star, and the related dimension tables form the points of the star.
* In an analytic query, dimensions table columns filter or group. Fact table columns are summarized.

Visualized example:
![[Pasted image 20230930123719.png]]

## Table storage mode

Each Power BI model table (except calculated tables) has a storage mode property. The storage mode property can be either **Import**, **DirectQuery**, or <mark style="background: #D2B3FFA6;">Dual</mark>, and it determines whether table data is stored in the model.

### Model framework

<mark style="background: #FF5582A6;">Table storage mode settings determine the model framework</mark>, which can be either import, DirectQuery, or <mark style="background: #D2B3FFA6;">composite</mark>. The following units in this module describe each of these frameworks and provides guidance on their use.

- An import model comprises tables that have their storage mode property set to **Import**.
- A DirectQuery model comprises tables that have their storage mode property set to **DirectQuery**, and they belong to the same **source group**. Source group is described later.
- A composite model comprises more than one source group.

check [this](https://learn.microsoft.com/en-us/training/modules/choose-power-bi-model-framework/6-choose-model-framework), only after you finish the subsequent sections, to see the guidelines of choosing the right model framework.

#### Import Model

Benefits: almost everything in terms of performance and functionality.

Limitations:

* Model Size:
	* there’s a 1-GB limit per dataset.
		* This limit refers to the compressed size of the Power BI model, not the volume of data being collected from the source system.
	* When you publish the model to a dedicated capacity (also known as Premium capacities), it can grow beyond 10-GB, providing you enable the [Large dataset storage format setting](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-large-models) for the capacity.
	* To decrease dataset capacity, checkout tips [here](https://learn.microsoft.com/en-us/power-bi/guidance/import-modeling-data-reduction).
* Data Refresh:
* Daily refresh limits: up to eight times per day in a shared capacity, and up to 48 times per day in a dedicated capacity.
* to refresh a table, Power BI removes all data and reloads it again. These operations can place an unacceptable burden on source systems, especially for large fact tables. To reduce this burden, you can set up the incremental refresh feature. Incremental refresh automates the creation and management of time-period partitions, and intelligently update only those partitions that require refresh.
	* When your data source supports incremental refresh, it can result in faster and more reliable refreshes, and reduced resource consumption of Power BI and source systems.
	* Advanced data modelers can customize their own partitioning strategy. Automation scripts can create, manage, and refresh table partitions. For more information, see [Power BI usage scenarios: Advanced data model management](https://learn.microsoft.com/en-us/power-bi/guidance/powerbi-implementation-planning-usage-scenario-advanced-data-model-management). This usage scenario describes using the XMLA endpoint available with Power BI Premium.

#### DirectQuery Model

[M source](https://learn.microsoft.com/en-us/training/modules/choose-power-bi-model-framework/4-determine-when-to-develop-directquery-model)

* A DirectQuery model consists of DirectQuery storage mode tables that belong to the same source group. ^ngupkb
	* A source group is a set of tables that are related to a data source. It has two types:
	* Import source group: set of import storage mode tables related to a data source. ^v8cl9b
	* DirectQuery source group: set of DirectQuery storage mode tables related to a data source.
	* Side note: if we have more than one source group, then the model framework we're currently using is called a composite model.

![[Pasted image 20231007123300.png]]

Benefits:
* Model large or fast-changing data sources
* Enforce source RLS (row level security)
* Data sovereignty restrictions
	* If your organization has security policies that restrict data leaving their premises, then it isn’t possible to import data. A DirectQuery model that connects to an on-premises data source may be appropriate. (You can also consider installing [Power BI Report Server](https://learn.microsoft.com/en-us/power-bi/report-server/get-started) for on-premises reporting.)
* Create specialized datasets
	* Typically, DirectQuery mode supports relational database sources. That’s because Power BI must translate analytic queries to native queries understood by the data source.
	* However, there’s one powerful exception. You can connect to a Power BI dataset (or Azure Analysis Services model) and convert it to a DirectQuery local model. A local model is a relative term that describes a model’s relationship to another model. In this case, the original dataset is a remote model, and the new dataset is the local model. These models are chained, which is term used to describe related models. You can chain up to three models in this way.
	* This capability to chain models supports the potential to personalize and/or extend a remote model. The simplest thing you can do is rename objects, like tables or columns, or add measures to the local model. You can also extend the model with calculated columns or calculated tables, or add new import or DirectQuery tables. However, these extensions result in the creation of new source groups, which means the model becomes a [[Power BI#Composite Model|composite model]]. That scenario is described in [Unit 5](https://learn.microsoft.com/en-us/training/modules/choose-power-bi-model-framework/5-determine-when-to-develop-composite-model).
	* For more information, see [Using DirectQuery for Power BI datasets and Azure Analysis Services](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-datasets-azure-analysis-services).

Limitations:
- Not all data sources are supported. Typically, only major relational database systems are supported. Power BI datasets and Azure Analysis Services models are supported too.
- <mark style="background: #FF5582A6;">All Power Query (M) transformations are not possible</mark>, because these queries must translate to native queries that are understood by source systems. So, for example, <mark style="background: #FF5582A6;">it’s not possible to use pivot or unpivot transformations</mark>.
- Analytic query performance can be slow, especially if source systems aren’t optimized (with indexes or materialized views), or there are insufficient resources for the analytic workload.
- Analytic queries can impact on source system performance. It could result in a slower experience for all workloads, including OLTP operations.
- the number of users who are opening the reports at any one time will impact the load that is placed on the data source. For example, if your report has 20 visuals in it and 10 people are using the report, 200 queries or more will exist on the data source because each visual will issue one or more queries.

##### Behavior of DirectQuery Connections 

[M source](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/5-directquery-models#:~:text=Behavior%20of%20DirectQuery%20connections)

When you use DirectQuery to connect to data in Power BI Desktop, that connection behaves in the following way:

- When you initially use the **Get Data** feature in Power BI Desktop, you will select the source. If you connect to a relational source, you can select a set of tables and each one will define a query that logically returns a set of data. If you select a multidimensional source, such as SAP BW, you can only select the source.
- When you load the data, <mark style="background: #FF5582A6;">no data is imported into the Power BI Desktop, only the schema is loaded</mark>. 
	- When you build a visual within Power BI Desktop, queries are sent to the underlying source to retrieve the necessary data. 
	- The time it takes to refresh the visual depends on the performance of the underlying data source.
- If changes are made to the underlying data, they won't be immediately reflected in the existing visuals in Power BI due to caching. 
	- <mark style="background: #FF5582A6;">You need to carry out a refresh to see those changes.</mark> The necessary queries are present for each visual, and the visuals are updated accordingly.
	- Regarding refreshing in dashboards, similar logic applies: You can pin visuals, or entire report pages, as dashboard tiles. The tiles are automatically refreshed on a schedule, for example, every hour. You can control the frequency of this refresh to meet your requirements. When you open a dashboard, the tiles reflect the data at the time of the last refresh and might not include the latest changes that are made to the underlying data source. You can always refresh an open dashboard to ensure that it's up-to-date.
- When you publish the report to the Power BI service, it will result in a dataset in Power BI service, the same as for import. However, **no data is included with that dataset**.
- When you open an existing report in Power BI service, or build a new one, the underlying source is again queried to retrieve the necessary data. Depending on the location of the original source, you might have to configure an on-premises data gateway.
#### Composite Model

 [M source](https://learn.microsoft.com/en-us/training/modules/choose-power-bi-model-framework/5-determine-when-to-develop-composite-model)

A composite model comprises more than one [[Power BI#^ngupkb|source group]]. Typically, there’s always the import source group and a DirectQuery source group:
![[Pasted image 20230930134927.png]]

Benefits:
* design flexibility.
	* Commonly, enterprise models benefit from using DirectQuery tables on large data sources and by boosting query performance with imported tables.
* satisfy some analytic queries from imported data.
* when your model includes DirectQuery tables to a remote model, like a Power BI dataset, you can extend your model with new calculated columns and tables. It results in a specialized model based on a core model. For more information, see [Power BI usage scenarios: Customizable managed self-service BI](https://learn.microsoft.com/en-us/power-bi/guidance/powerbi-implementation-planning-usage-scenario-customizable-managed-self-service-bi).

Limitations:
* Import (or rather, dual) tables still require periodic refresh.
* Queries that require data from import and DirectQuery tables are slow. However, to avoid this:
	* add import aggregation tables to your model (or enable automatic aggregations)
	* set related dimension tables to use dual storage mode. 
	* This scenario is described later
* When chaining models, modifications made to upstream models can break downstream models. Be sure to assess the impact of modifications by performing [dataset impact analysis](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-dataset-impact-analysis) first.
* Relationships between tables from different source groups are known as limited relationships. A model relationship is limited when the Power BI can’t determine a “one” side of a relationship. Limited relationships may result in different evaluations of model queries and calculations. For more information, see [[Power BI#Relationship Evaluation Advanced|Relationship evaluation]] (its [M source](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-relationships-understand)).

##### Boost DirectQuery model performance with import data

When there’s a justification to develop a DirectQuery model, you can mitigate some limitations by using specific Power BI features that involve import tables.

###### Import aggregation tables

* Enable automatic aggregations to direct fact queries to a cached aggregation. 
* ensure that related dimension tables are set to use dual storage mode.
* Automatic aggregations are a Premium feature. For more information, see [Automatic aggregations](https://learn.microsoft.com/en-us/power-bi/enterprise/aggregations-auto).

###### Dual storage mode

A dual storage mode table is set to use both import and DirectQuery storage modes. At query time, Power BI determines the most efficient mode to use. Whenever possible, Power BI attempts to satisfy analytic queries by using cached data.

Dual storage mode tables work well with import aggregation tables.

Slicer visuals and filter card lists, which are often based on dimension table columns, render more quickly because they’re queried from cached data.

###### Deliver real-time data from an import model

When you set up an import table with incremental refresh, you can enable the **Get the latest data in real-time with DirectQuery** option.

![Animated diagram shows the incremental refresh and real-time data set up, and it highlights the Get the latest data in real-time with DirectQuery option.](https://learn.microsoft.com/en-us/training/wwl-data-ai/choose-power-bi-model-framework/media/model-framework-incremental-refresh.png)

By enabling this option, Power BI automatically creates a table partition that uses DirectQuery storage mode. In this case, the table becomes a hybrid table, meaning it has import partitions to store older data, and a single DirectQuery partition for current data.

When Power BI queries a hybrid table, the query uses the cache for older data, and passes through to the data source to retrieve current data.

This option is only available with a Premium license.

For more information, see [Configure incremental refresh and real-time data](https://learn.microsoft.com/en-us/power-bi/connect-data/incremental-refresh-configure).

### Load JSON Using Expander

when loading NoSQL data (from Cosmos DB for example), data will initially look like this:
![[Pasted image 20230930080619.png]]

So click load, then click on the expander button, then uncheck prefix option, then apply:
![[Pasted image 20230930080722.png]]


# Relationship Evaluation (Advanced)

[M source](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-relationships-understand#relationship-evaluation)

first of all, an example of a [[Power BI#Composite Model|composite model]]:
![[Pasted image 20230930140506.png]]
(side note: vertipaq is just a case scenario name for an [[Power BI#^v8cl9b|import source group]]).

Relationships can be evaluated into one of the following two types:
### Regular relationships
A model relationship is _regular_ when the query engine can determine the "one" side of relationship. It has confirmation that the "one" side column contains unique values.

Example (denoted by "R"):
![[Pasted image 20230930140913.png]]

Benefits:
* Upon refreshing the data of imported models, data structures (DSs) are created for each regular relationship 
	* These DSs consist of indexed mappings of all column-to-column values
	* their purpose is to accelerate joining tables at query time.
* At query time, table expansion happens, example:
![[Pasted image 20230930141221.png]]
	side note: the columns highlighted in red and green are the columns used to join Sales with Product and Product with Category respectively.
	The expanded table is effectively a denormalized perspective of the data contained in the three tables. This is beneficial for increasing performance of analytical queries. In the example above, a new row is added to the **Sales** table, and it has a production identifier value (9) that has no matching value in the **Product** table. It's a referential integrity violation. In the expanded table, the new row has (Blank) values for the **Category** and **Product** table columns.

### Limited relationships

A model relationship is _limited_ when there's no guaranteed "one" side. A limited relationship can happen for two reasons:

- The relationship uses a many-to-many cardinality type (even if one or both columns contain unique values).
- The relationship is cross source group (which can only ever be the case for composite models).

Example (limited relationships are indicated by "L"):
![[Pasted image 20230930141641.png]]

The benefits of regular relationships are now gone:
* data structures are never created for limited relationships. 
	* Well then what happens? Power BI resolves table joins at query time.
* Table expansion never occurs for limited relationships. 
	* Therefore blank virtual rows aren't added to compensate for referential integrity violations.
		* Why? because table joins are now achieved by using `INNER JOIN` semantics.

There are other restrictions related to limited relationships:

- The `RELATED` DAX function can't be used to retrieve the "one" side column values.
- Enforcing RLS has topology restrictions.

Note, Power BI indicates a limited relationship by the parentheses `( )` here:
![[Pasted image 20230930141911.png]]

# Working With Tables (Power BI Model View)

[M source](https://learn.microsoft.com/en-us/training/modules/design-model-power-bi/2-tables)
## Configuring Data Model and Building relationships between tables

click here:
![[Pasted image 20231002142905.png]]

then, to manage relationships, click here:
![[Pasted image 20231002143006.png]]

then press `auto detect` if the tables have common column names. Otherwise, press `new` to display this:
![[Pasted image 20231002143900.png]]
note 1: the configuration above will change depending on the scenario of your data.
note 2: read more about "Cross filter direction" [here](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-relationships-understand)

## Creating a Date Table

[M source](https://learn.microsoft.com/en-us/training/modules/design-model-power-bi/3-date-table)

use case example: suppose that you are developing reports for the Sales team at your organization. The database contains tables for sales, orders, products, and more. You notice that many of these tables, including Sales and Orders, contain their own date columns, as shown by the **ShipDate** and **OrderDate** columns in the Sales and Orders tables. You are tasked with developing a table of the total sales and orders by year and month. <mark style="background: #FFF3A3A6;">How can you build a visual with multiple tables, each referencing their own date columns?</mark>

To solve this problem, <mark style="background: #FF5582A6;">you can create a common date table that can be used by multiple tables.</mark>

Ways that you can build a common date table are:

- Source data    
- DAX
- Power Query

Then, you'll need to:
* mark your table as the official date table of your data model.
* establish relationships between your date table and the other tables containing dates (e.g., Sales and Order tables).

Side note: Date tables are required to apply special time filters known as _time intelligence_.

### Building The Table 

First, let's see the 3 ways to build a common date table.

#### Using Source Data

If the source databases already have their own date tables, then bring it into your data model and don't use any other methods that are outlined in this section.

Otherwise, use the other two methods.

#### Using DAX (Data Analysis Expression)

Use one one of the following DAX functions:
* CALENDAR
	* returns a contiguous range of dates based on a start and end date that are entered as arguments in the function.
* [CALENDARAUTO](https://learn.microsoft.com/en-us/dax/calendarauto-function-dax)
	* returns a contiguous, complete range of dates that are automatically determined from your dataset (using earliest and last dates of found in your dataset. However, ending date [can be even later than that](<https://learn.microsoft.com/en-us/training/modules/design-model-power-bi/3-date-table#:~:text=plus%20data%20that%20has%20been%20populated%20to%20the%20fiscal%20month%20that%20you%20can%20choose%20to%20include%20as%20an%20argument%20in%20the%20CALENDARAUTO()%20function.>))
	* Note ([M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-calculated-tables/1-introduction#:~:text=The%20CALENDARAUTO%20DAX%20function%20takes,would%20be%20June%2030%2C%202022.)): when passing an optional argument called `fiscal_year_end_month`, then the returned date values change. The following example illustrates this: Suppose the MinDate and MaxDate in the data model are July 1, 2010 and June 30, 2011. Then:
		* `CALENDARAUTO()` will return all dates between January 1, 2010 and December 31, 2011.
		* `CALENDARAUTO(3)` will return all dates between April 1, 2010 and March 31, 2012.

##### CALENDAR()

Follow these steps to create a date table called `Dates`:

![[Pasted image 20231002193841.png]]
the formula above creates `Dates` table from 2011-5-31 until 2022-12-31

Then, if you want to add other columns, select "New column" (next to "New table"), and execute the following DAX expressions:
```DAX
Year = YEAR(Dates[Date])
MonthNum = MONTH(Dates[Date])
WeekNum = WEEKNUM(Dates[Date])
DayoftheWeek = FORMAT(Dates[Date], "DDDD")
```

Pro tip ([source1](https://www.youtube.com/watch?v=-li7sxUxEqA), [source2](https://www.sqlbi.com/articles/creating-a-simple-date-table-in-dax/#:~:text=The%20code%20snippet,other%20column%20required), [source3](https://www.sqlbi.com/articles/reference-date-table-in-dax-and-power-bi/)):
just use this all-in-one DAX expression :] :

``` EXCEL
Date =
VAR MinYear = YEAR(MIN(Sales[Order Date]))
VAR MaxYear = YEAR(MAX(Sales[Order Date]))
RETURN
ADDCOLUMNS (
    FILTER (
        CALENDARAUTO( ),
        AND(YEAR([Date]) >= MinYear, YEAR([Date]) <= MaxYear)
    ),
    "Calendar Year", "CY " & YEAR([Date]),
    "Month Name", FORMAT([Date], "mmmm"),
    "Month Number", MONTH([Date]),
    "Weekday", FORMAT([Date], "dddd"),
    "Weekday number", WEEKDAY([Date]),
    "Quarter", "Q" & TRUNC((MONTH([Date]) - 1) / 3 ) + 1
)
```

the expression above can be used instead of just applying `CALENDARAUTO()` so that we get the relevant start/end dates only using `MinYear` and `MaxYear`.

Note: if you don't understand this syntax, refer to [[#Calculated Tables|Calculated Tables]] and [[#DAX Syntax|DAX Syntax]] headers.
#### Using Power Query's M Language

Open Power Query from here:
![[Pasted image 20231002194510.png]]

Then, in the left pane of the power query:
![[Pasted image 20231002194725.png]]

Then execute the following query:
![[Pasted image 20231002194828.png]]

Then, to convert to table:
![[Pasted image 20231002195914.png]]
Then select the delimiter as "none" and the extra columns to "show errors" (or other options if you find them useful :])

Then, to add columns from that date column (e.g., year):
![[Pasted image 20231002200143.png]]

### Marking as Official Date Table

Follow these steps:
![[Pasted image 20231002201213.png]]
then choose the date column.

Note 1 ([M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-calculated-tables/1-introduction#:~:text=The%20table%20must,have%20missing%20dates.)):
to mark a table as date table, the following requirements must  be met:
- The table must include a column of data type Date.
- The date column ([M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-time-intelligence/2-functions#:~:text=Date%20table%20requirement)): 
	- must span full years. A year isn't necessarily a calendar year (January-December).
	- must not have missing dates.
	- must contain unique values.
	- must not contain BLANKs.



Note 2:
Selecting **Mark as date table** <mark style="background: #D2B3FFA6;">will remove autogenerated hierarchies from the **Date** field in the table that you marked as a date table</mark>. For other date fields, the auto hierarchy will still be present until you establish a relationship between that field and the date table or until you turn off the **Auto Date/Time** feature. You can manually add a hierarchy to your common date table by right-clicking the year, month, week, or day columns in the **Fields** pane and then selecting **New hierarchy.** This process is further discussed later.

### Establishing Relationships

The final step to build your visuals is to establish a relationship between this new common date table and the other tables that contain dates (e.g., Sales and Orders tables).

To do this, access the `manage relationships` menu by following the steps previously described in "[[Power BI#Configure data model and build relationships between tables|Configure data model and build relationships between tables]]" header, such that the final menu configuration looks similar to this:
![[Pasted image 20231002204342.png]]

Alternatively, you can just drag and drop the date column into the other required tables from the model view as shown [here](https://youtu.be/-li7sxUxEqA?t=180) (at 3:00)

Finally, look at Microsoft's example [here](https://learn.microsoft.com/en-us/training/modules/design-model-power-bi/3-date-table#:~:text=After%20you%20have%20built,a%20common%20date%20table.) or [this](https://www.youtube.com/watch?v=-li7sxUxEqA) great YouTube video to see how to visualize the tables now that you've managed their relationships.

## Working With Dimensions

[M source](https://learn.microsoft.com/en-us/training/modules/design-model-power-bi/4-dimensions)

One can use use hierarchies as one source to help you find detail in dimension tables.

### Hierarchies

Power BI automatically enters values of the date type as a hierarchy (if the table has not been marked as a date table).

Follow these steps to create a hierarchy:
![[Pasted image 20231002221458.png]]

Then, add the sub-columns to the main hierarchy column by following these steps:
![[Pasted image 20231002222143.png]]

Then, you can do whatever you want with this hierarchy:
![[Pasted image 20231002222712.png]]
for example, use as x-axis of a visualization.

#### Flattening a Parent-Child Hierarchy

In the example below, `Manager ID` is logically a parent of `Employee ID`.
![[Pasted image 20231002222904.png|625]]
But the two columns above just show us the first level of the hierarchy (for example, they will show us that 1013 -> 1011, but they won't show us that 1013 -> 1011 -> 1010). Therefore, <mark style="background: #FF5582A6;">to visualize all the hierarchy levels, we have to flatten it</mark>.

To flatten the hierarchy, right click the table of interest, then click "new column", then execute the following DAX expression:
``` EXCEL
Path = PATH(Employee[Employee ID], Employee[Manager ID])
```
its output is the "Path" column in the table below:
![[Pasted image 20231002223748.png|550]]

then, create columns of all the possible levels of this path by executing the following DAX expressions:
```EXCEL
Level 1 = PATHITEM(Employee[Path],1)
Level 2 = PATHITEM(Employee[Path],2)
...
Level N = PATHITEM(Employee[Path],N)
```
where N is the last level between an employee and a manger. But how to know this number?:
```EXCEL
MaxLevel = MAXX(Employee, PATHLENGTH(Employee[Path])) - 1
```
so create any temporary column with `MaxLevel` just to see that number, and if the result is 2, then `N` will be 2, and so on.

Now, you can create a hierarchy with these columns.

### Role-Playing Dimensions

Previously, you've considered dimensions that have only one relationship with a fact table. However, situations do occur where your <mark style="background: #FFB8EBA6;">dimension table will have multiple relationships with a fact table</mark>.

Example 1 ([M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-write-formulas/1-introduction#:~:text=CALENDARAUTO%20DAX%20functions.-,Role%2Dplaying%20dimensions,-When%20two%20model)):
When two model tables have multiple relationships, it could be because your model has a role-playing dimension. For example, if you have a table named **Sales** that includes two date columns, **OrderDateKey** and **ShipDateKey**, both columns are related to the **Date** column in the **Date** table. In this case, the **Date** table is described as a role-playing dimension because it could play the role of _order date_ or _ship date_.
![[Pasted image 20231004100904.png]]

Now, Microsoft Power BI models only allow one active relationship between tables, which in the model diagram is indicated as a solid line. The active relationship is used by default to propagate filters, which in this case would be from the **Date** table to the **OrderDateKey** column in the **Sales** table. Any remaining relationships between the two tables are inactive. In a model diagram, the relationships are represented as dashed lines. Inactive relationships are only used when they're expressly requested in a calculated formula by using the [`USERELATIONSHIP`](https://learn.microsoft.com/en-us/dax/userelationship-function-dax/) DAX function.

Perhaps a better model design could have two date tables, each with an active relationship to the **Sales** table. Thus, report users can filter by order date or ship date, or both at the same time. A calculated table can duplicate the **Date** table data to create the **Ship Date** table.

Example 2:
![[Pasted image 20231002225012.png|450]]
The preceding visual shows the Calendar, Sales, and Order tables. Calendar is the dimension table, while Sales and Order are fact tables. The dimension table has two relationships: one with Sales and one with Order. This example is of a role-playing dimension because the Calendar table can be used to group data in both Sales and Order. 
If you wanted to build a visual in which the Calendar table references the Order and the Sales tables, the Calendar table would act as a role-playing dimension.

## Data Granularity

[M source](https://learn.microsoft.com/en-us/training/modules/design-model-power-bi/5-data-granularity)

Data granularity is the detail that is represented within your data, meaning that the more granularity your data has, the greater the level of detail within your data.

Consider a scenario where your company manages 1,000 refrigerated semi-trucks. Every few minutes, each truck uses a Microsoft Azure IoT application to record its current temperature. This temperature is important to your organization because, if the refrigeration were to malfunction, it could spoil the entire load, costing thousands of dollars. With so many trucks and so many sensors, extensive data is generated every day. Your report users don't want to sift through numerous records to find the ones that they are particularly interested in.

How can you change the granularity of the data to make the dataset more usable?

In this scenario, you might want to import the data by using a daily average for each truck. That approach would reduce the records in the database to one record for each truck for each day.

### Building Relationship Where Granularity Differs

consider that you're building reports for the Sales team at Tailwind Traders. You've been asked to build a matrix of total sales and budget over time by using the Calendar, Sales, and Budget tables. You notice that the lowest level of time-based detail that the Sales table goes into is by day, for instance 5/1/2020, 6/7/2020, and 6/18/2020. The Budget table only goes to the monthly level, for instance, the budget data is 5/2020 and 6/2020:

![[Pasted image 20231003183435.png]]

Therefore, we need to define same granularity level for both tables, which can be done by transforming the **Year** and **Month** columns in the Calendar table into a new column, and do the same transformation in the Budget table, you can match the format of the **Date** column in the Calendar table. Then, you can establish a relationship between the two columns. To complete this task, you'll concatenate the **Year** and **Month** columns and then change the format. This can be done like so:

Select **Transform Data** on the ribbon. On **Applied Steps**, on the right pane, right-click the last step and then select **Insert Step After**:
![[Pasted image 20231003190519.png|324]]

Under **Add Column** on the Home ribbon, select **Custom Column**. Enter the following equation, which will concatenate the **Year** and **Month** columns, and then add a dash in between the column names.

```M
Column = Table.AddColumn(#"Renamed Columns", "Custom", each [Year] & "-" &[Month])
```

Then, change the data type to **Date** and then rename the column. Your Budget table should resemble the following figure:
![[Pasted image 20231003225255.png|450]]

Now, you can create a relationship between the Budget and the Calendar tables like so (in the [M source](https://learn.microsoft.com/en-us/training/modules/design-model-power-bi/5-data-granularity#:~:text=create%20the%20relationship%20on%20the%20Date%20column), it is said that the relationship is on the `Date` column, however, I think they meant the `MonthYear` column?):
![[Pasted image 20231003225344.png|700]]

Now, check [this](https://learn.microsoft.com/en-us/training/modules/design-model-power-bi/5-data-granularity#:~:text=Now%2C%20you%20need,budgets%20over%20time.) to see how to build a matrix of the total sales and budgets over time.

## Relationship Cardinalities & Bi-Directional Cross-Filtering 

[M source](https://learn.microsoft.com/en-us/training/modules/design-model-power-bi/6-relationships-cardinality)

Data can be filtered on one or both sides of a relationship.

With a **single cross-filter direction**:

- Only one table in a relationship can be used to filter the data. For instance, Table 1 can be filtered by Table 2, but Table 2 cannot be filtered by Table 1.
- For a one-to-many or many-to-one relationship, the cross-filter direction will be from the "one" side, meaning that the filtering will occur in the table that has many values.

Tip:
<mark style="background: #D2B3FFA6;">Follow the direction of the arrow on the relationship between your tables to know which direction the filter will flow. You typically want these arrows to point to your fact table.</mark>

With **both cross-filter directions** or **bi-directional cross-filtering**:

- One table in a relationship can be used to filter the other. For instance, a dimension table can be filtered through the fact table, and the fact tables can be filtered through the dimension table.
- You might have lower performance when using bi-directional cross-filtering with many-to-many relationships.

You should not enable bi-directional cross-filtering relationships unless you fully understand the ramifications of doing so.

For many-to-many relationships, you can choose to filter in a single direction or in both directions by using bi-directional cross-filtering. The ambiguity that is associated with bi-directional cross-filtering is amplified in a many-to-many relationship because multiple paths will exist between different tables. If you create a measure, calculation, or filter, unintended consequences can occur where your data is being filtered and, depending on which relationship that the Power BI engine chooses when applying the filter, the final result might be different. This situation is also true for bi-directional relationships and why you should be cautious when using them.

Also, check out [this](https://learn.microsoft.com/en-us/training/modules/design-model-power-bi/6-relationships-cardinality#:~:text=Create%20many%2Dto%2Dmany%20relationships) example on creating a many to many relationship (even though I don't fully understand why it's a M:M relationship, since the customer ID is unique in the Customer table)

# Context Types (Row, Query, Filter Contexts)

[M source](https://support.microsoft.com/en-au/office/context-in-dax-formulas-2728fae0-8309-45b6-9d32-1d600440a7ad)

[TDS source](https://medium.com/analytics-vidhya/concept-of-context-in-dax-with-examples-in-power-bi-chapter-3-14fe6ab3ce32)

![[Pasted image 20231006100849.png]]
([source](https://thedatalabs.org/filter-context/))

* Context is what makes it possible to perform dynamic analysis.
* “Context is how DAX applies layers of filtering to tables used in your calculations so that they return results that are relevant for every value.”
* There are different types of context: row context, query context, and filter context.
	* Filter context is the set of values allowed in each column, based on filter constraints that were applied to the row or that are defined by filter expressions within the formula.
	* Row context can be thought of as "the current row.” 
		* If you have created a **[[#Calculated Columns|calculated column]]**, the row context consists of the values in each individual row and values in columns that are related to the current row. 
		* There are also some functions ([EARLIER](https://docs.microsoft.com/dax/earlier-function-dax) and [EARLIEST](https://docs.microsoft.com/en-us/dax/earliest-function-dax)) that get a value from the current row and then use that value while performing an operation over an entire table.
	* Query context refers to the subset of data that is implicitly created for each cell in a PivotTable, depending on the row and column headers.

## Filter Context

Filter context means when you are applying **filters** on the set of **values** of **columns** or **tables** using **DAX calculations**.

There are some items on which filter context applied. For example,

1. attributes in rows or columns
2. by slicer
3. through filter pane
4. to the calculated measure
	1. This is done using [`CALCULATE`](https://learn.microsoft.com/en-us/dax/calculate-function-dax/) and [`FILTER`](https://learn.microsoft.com/en-us/dax/filter-function-dax/) DAX functions, as explained in [this](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-modify-filter/2-modify-filter-context) Microsoft source, which is referenced later in the [[#Filter Context Functions|Filter Context Functions]] section.

> “Filter context applies on top of other contexts, such as row context or query context.”

* Filter context is the context that is applied to a whole table or column when a formula is evaluated ([source](https://www.linkedin.com/pulse/row-context-filter-dax-essentials-ayush-mittal/)).
	* Filter context is usually created by slicers, visuals, or filters that limit the data that is available for calculation.
		* For example, if you have a slicer that lets you select a product category, and you want to calculate the average sales for each product category, you can use a formula like this: `Average Sales = AVERAGE(Total Sales)`, then it will calculate the average of the total sales column for each product category. **The filter context in this case could be determined by the slicer that filters the sales table by product category**.

Visualized example of filter context ([source](https://www.statslab-bi.co.nz/project/row-filter-context-dax/)):
![[Pasted image 20231006101604.png]]

You can learn more about filter contexts from [this](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-modify-filter/1-introduction) Microsoft source.

### Filter Behavior When Adding Filter Expressions

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-modify-filter/2-modify-filter-context#:~:text=Two%20possible%20standard%20outcomes%20occur%20when%20you%20add%20filter%20expressions%20to%20the%20CALCULATE%20function)

Two possible standard outcomes occur when you add filter expressions to the `CALCULATE` function:

- If the columns (or tables) aren't in filter context, then new filters will be added to the filter context to evaluate the `CALCULATE` expression.
- If the columns (or tables) are already in filter context, the existing filters will be overwritten by the new filters to evaluate the `CALCULATE` expression.

Example to illustrate this:
Given this DAX formula (mentioned in a later sub-section in [[#Filter Context Functions|Filter Context Functions]]):
```EXCEL
Revenue Red = CALCULATE([Revenue], 'Product'[Color] = "Red")
```
and given that we add that measure to a table to get this:
![[Pasted image 20231006112010.png|417]]
If we now change the table's first column `Region` to the column `Color` (of `Product` table), then we'll get something like this:
![[Pasted image 20231006112247.png|433]]

The following bullet points are explanation of the two cases above:
* Case 1: Because no filter is applied on the **Color** column in the **Product** table, the evaluation of the measure adds a new filter to filter context. 
	* In the first row, the value of $2,681,324.79 is for red products that were sold in the Australian region.
* Case 2: Because we switched the first column of the table visual from **Region** to **Color**, the **Color** column will now be in filter context. 
	* Consequently, in this visual that groups by color, the measure formula overwrites the filter context with a new filter.
	* This result might or might not be what you want. Thus [`KEEPFILTERS`](https://learn.microsoft.com/en-us/dax/keepfilters-function-dax/) DAX function is introduced later, 
		* KEEPFILTERS is a filter modification function that you can use to preserve filters rather than overwrite them.





## Row Context

* **Row Context** is related to **current rows.**
	* If you create a calculation using the **[[#Calculated Columns|calculated column]]**, the row context involves the **values of all** columns from the **current** row.
		* If that table [[Power BI#^128yfb|has a relationship with the other table]], then it includes all the **related** values from the other table for that row.
	* There are some [[#Iterator Functions|iterative functions]] in **DAX** over a table. Those functions involve **multiple** rows during calculation and each with its own **row context**.

Visualized example of row context in a calculated column ([source](https://powerbidocs.com/2021/01/07/filter-context-and-row-context-in-power-bi/)):
![[Pasted image 20231006101527.png]]

A visualized example of row context in an iterator function is shown later in the [[#Iterator Functions|Iterator Functions]] section.

## Query Context

The combination of row and filters create the final query for DAX. You can define this is as query context. Users explicitly mention row and filter context for DAX, and DAX implicitly creates the query context from that filter and row context.

# DAX (Data Analysis Expression)

## DAX Calculation Types

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-write-formulas/1-introduction)

By using Data Analysis Expressions (DAX), you can add three types of calculations to your data model:
- Measures
- Calculated columns
- Calculated tables

Note:
DAX can also be used to define row-level security (RLS) rules, which are expressions that enforce filters over model tables. However, rules aren't considered to be model calculations so they're out of scope for this module. More information will be shown later, but for now, see [Row-level security (RLS) with Power BI](https://learn.microsoft.com/en-us/power-bi/admin/service-admin-rls/).

### Measures

* DAX formula achieves summarization over model data (unlike calculated columns, which operate row by row).
* DAX formula must return a single value (like calculated columns)
* Results are never stored in the model (unlike calculated columns)
* Measures are evaluated at query time (unlike calculated columns, which are evaluated at refresh time)
* Measures can't reference a table or column directly;
	* <mark style="background: #FFB8EBA6;">they must pass the table or column into a function to produce a summarization</mark>.

Its appearance is like this:
![[Pasted image 20231004131654.png]]

#### Implicit Measures

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-measures/1-introduction)

Non-numeric columns can be summarized. However, the sigma symbol does not show next to non-numeric columns in the **Fields** pane because they don't summarize by default.

Text columns allow the following aggregations:
- <mark style="background: #D2B3FFA6;">First (alphabetically)</mark>
- <mark style="background: #D2B3FFA6;">Last (alphabetically)</mark>
- Count (Distinct)
- Count

Date columns allow the following aggregations:
- Earliest
- Latest
- Count (Distinct)
- Count

Implicit measures aren't suitable for the following case:
* When you need to make sophisticated calculations.
* When the model is queried by using Multidimensional Expressions (MDX). Note that MDX: 
	* expects explicit measures 
	* can't summarize column data. 
	* is used when a Power BI dataset is queried by using [Analyze in Excel](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-analyze-in-excel/) 
	* is used when a [Power BI paginated report](https://learn.microsoft.com/en-us/power-bi/paginated-reports/paginated-reports-report-builder-power-bi/) uses a query that is generated by the MDX graphical query designer.

#### Explicit Measures (Simple, Compound, and Quick)

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-measures/2-simple-measures)

* Are called "simple measures" if they aggregate a **single** column or **single** table ([M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-measures/2-simple-measures#:~:text=All%20measures%20that%20you%27ve%20created%20are%20considered%20simple%20measures%20because%20they%20aggregate%20a%20single%20column%20or%20single%20table.)).
* Are called "compound measures" if they reference one or more measures ([M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-measures/3-compound-measures)).
	* Example: `Profit = [Revenue] - [Cost]`
* Are called "quick measures" if you create the measure from Table tools -> calculations -> quick measure as seen below ([M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-measures/4-quick-measures)):
![[Pasted image 20231004205818.png]]
(for more info on the rest of the steps of creating the quick measure, check [this](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-measures/4-quick-measures#:~:text=In%20the%20Fields,the%20measure%20definition.))

Note that all these measure types are not mutually exclusive.
#### Explicit vs Implicit Measures

"Measures" can be the following:

* Explicit measures:
	* Usually a synonym for the word "measures".
	* Created by writing them with DAX.
	* Are calculations that you can add to your model.
* Implicit measures:
	* created by clicking inside Power BI's interface; where we click simple summarization methods like sum, count, etc.
	* Are identified in the Fields pane because they're shown with the sigma symbol.
		* Note: Any column can be summarized when added to a visual. Therefore, whether they're shown with the sigma symbol or not, when they're added to a visual, they can be set up as implicit measures.
	* Are automatic behaviors that allow visuals to summarize model column data.

#### "Calculated Measure" is a Non-Existent Term

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-measures/2-simple-measures#:~:text=In%20tabular%20modeling%2C%20no%20such%20concept%20as%20a%20calculated%20measure%20exists.%20The%20word%20calculated%20is%20used%20to%20describe%20calculated%20tables%20and%20calculated%20columns.%20It%20distinguishes%20them%20from%20tables%20and%20columns%20that%20originate%20from%20Power%20Query%2C%20which%20doesn%27t%20have%20the%20concept%20of%20an%20explicit%20measure)

Regarding the word "calculated":
* It describes calculated tables and calculated columns
	* These are created from DAX while normal tables and columns are created from Power Query
* Therefore, it doesn't apply to measures.

TLDR; Power Query doesn't have the concept of a measure.

### Calculated Columns

* write a DAX formula to add a calculated column to any table in your model. 
	* The formula is evaluated for each table row and it returns a single value.
* Increases the storage size of your model.

Its appearance is like this:
![[Pasted image 20231004131317.png]]

Note 1: Check out DAX examples of calculated columns and how to deal with fiscal years [here](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-calculated-tables/2-calculated-columns).

Note 2 (M source): If your DAX formula needs to reference columns **in other tables**, you have two options:  ^128yfb
* If the tables are related, directly or indirectly, you can use the [`RELATED`](https://learn.microsoft.com/en-us/dax/related-function-dax/) or [`RELATEDTABLE`](https://learn.microsoft.com/en-us/dax/relatedtable-function-dax/) DAX function. The `RELATED` function retrieves the value at the one-side of the relationship, while the `RELATEDTABLE` retrieves values on the many-side. The `RELATEDTABLE` function returns a table object.
- When the tables aren't related, you can use the [`LOOKUPVALUE`](https://learn.microsoft.com/en-us/dax/lookupvalue-function-dax/) DAX function.

Generally, try to use the `RELATED` function whenever possible. It will usually perform better than the `LOOKUPVALUE` function due to the ways that relationship and column data is stored and indexed.

Example: suppose you have the following 2 tables:
![[Pasted image 20231005184103.png|550]]
(source: [Adventure Works DW 2020 M03.pbix](https://github.com/MicrosoftDocs/mslearn-dax-power-bi/raw/main/activities/Adventure%20Works%20DW%202020%20M03.pbix) file)

and now the calculated column definition below adds the **Discount Amount** column to the **Sales** table:
```EXCEL
Discount Amount =
(
    Sales[Order Quantity]
        * RELATED('Product'[List Price])
) - Sales[Sales Amount]
```
Power BI evaluates the calculated column formula for each row of the **Sales** table. The values for the **Order Quantity** and **Sales Amount** columns are retrieved within row context. However, because the **List Price** column belongs to the **Product** table, the `RELATED` function is required to retrieve the list price value _for the sale product_.

Note: as you can see: Per row, Power BI knows the corresponding row in the `Product` table, as they are joined using the `ProductKey`.
### Calculated Tables

* DAX formula can duplicate or transform _existing model data_, or create a series of data, to produce a new table.
* Calculated table data is always imported into your model, so it increases the model storage size and can prolong data refresh time.

Note
A calculated table can't connect to external data; you need to use Power Query to accomplish that task.

Calculated tables can be useful in various scenarios:
- [[#Creating a Date Table|Date tables]]
- [[#Role-Playing Dimensions|Role-playing dimensions]]
- [[#What-If Analysis (Disconnected Tables)|What-if analysis]]

#### Avoiding Multi-Relationships by Using Calculated Tables

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-calculated-tables/1-introduction)

Consider the following scenario:
![[Pasted image 20231005134733.png]]
Notice that the **Sales** table has three relationships to the **Date** table.
**In this case**, the active relationship filters the **OrderDateKey** column in the **Sales** table. **Thus**, filters that are applied to the Date table will propagate to the Sales table to **filter by order date; they'll never filter by ship date or due date**. 

Therefore, we can enhance the current model structure by doing the following steps:
* Delete the inactive relationships;
	* `Date['Date']` -> `Sales['ShipDateKey']`
	* `Date['Date']` -> `Sales['DueDateKey']`
* Create Calculated tables that will act like "mirrors" of `Date` table, so we'll have at the end something like this:
	* `Ship Date['Ship Date']` -> `Sales['ShipDateKey']`
	* `Due Date['Due Date']` -> `Sales['DueDateKey']`
	* Side note: "Mirror" is a term I personally came up with, which refers to the following:
		* when the **Date** table data refreshes, the **Ship Date** & **Due Date** tables recalculate, so they'll always be in sync ([M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-calculated-tables/1-introduction#:~:text=When%20the%20Date%20table%20data%20refreshes%2C%20the%20Ship%C2%A0Date%20table%20recalculates%2C%20so%20they%27ll%20always%20be%20in%20sync.)). So for example, <mark style="background: #FF5582A6;">The Due Date calculated table will recalculate each time a table (Sales or Date tables) that contains a date column refreshes.</mark> In other words, when a row is loaded into the **Sales** table with an order date of July 1, 2022, the **Due Date** table will automatically extend to include dates through to the end of the next year: June 30, 2023 ([M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-calculated-tables/1-introduction#:~:text=The%20Due%C2%A0Date%20calculated%20table%20will,the%20next%20year%3A%20June%2030%2C%202023.)).

check [this](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-calculated-tables/1-introduction#:~:text=to%20refreshed%20tables.-,Duplicate%20a%20table,-The%20following%20section) and [this](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-calculated-tables/1-introduction#:~:text=time%20intelligence.-,Create%20a%20date%20table,-In%20the%20next) to see the full steps of how to create `Ship Date` and `Due Date` tables respectively.

But to summarize, either duplicate the `Date` table by clicking here:
![[Pasted image 20231005135916.png]]
then executing this: `Ship Date = 'Date'`
then organizing the columns to be meaningful like this:
![[Pasted image 20231005140033.png|375]]
then marking table as date table on `Ship Date` column.

Or, you can create new table using `CALENDARAUTO` DAX function like this: `Due Date = CALENDARAUTO(6)` (assuming that the financial year for your company ends on June 30 of each year).
Then follow similar organizing steps as previously mentioned.
#### What-If Analysis

You can use _what-if_ parameters to run scenarios and scenario-type analysis on your data. What-if parameters are powerful additions to your Power BI data models and reports because they enable you to look at historical data to analyze potential outcomes if a different scenario had occurred. Additionally, what-if parameters can help you look forward, to predict or forecast what could happen in the future ([M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/8-what-if-parameters)).

When you create a [What-if parameter](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-what-if/), a calculated table is automatically added to your model. Example ([source](https://www.youtube.com/watch?v=6a_5uderwAg)):
![[Pasted image 20231004113636.png]]

What-if parameters allow report users to select or filter by values that are stored in the calculated table. Measure formulas can use selected value(s) in a meaningful way. In the example above, the what-if parameter is the chosen numeric range in `Pct Sales Forecast`, and the measure formula is to multiply this numeric value by the `Total Sales` column to get the `Total Sales Forecast` bars in the bar chart above.

Notably, what-if calculated tables aren't related to other model tables because they're not used to propagate filters. For this reason, they're sometimes called _disconnected tables_. Side note: Every what-if table is a *disconnected table*, but the reverse is not true.

### Comparisons
#### Calculated Columns vs Measures

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-measures/5-compare-calculated-columns-measures)

Calculated columns and measures differ in the following points:
- **Purpose** - Calculated columns extend a table with a new column, while measures define how to summarize model data.
- **Evaluation** - Calculated columns are evaluated by using <mark style="background: #D2B3FFA6;">row context</mark> at data refresh time, while measures are evaluated by using <mark style="background: #D2B3FFA6;">filter context</mark> at query time. Filter context is introduced in a later module; it's an important topic to understand and master so that you can achieve complex summarizations.
	- Side note ([source](https://endjin.com/blog/2022/04/measures-vs-calculated-columns-in-dax#:~:text=When%20you%20write%20a%20calculated%20column%2C%20you,wrap%20the%20column%20in%20an%20aggregation%20function.)): <mark style="background: #FF5582A6;">because measures don't see row context, you can't refer to columns directly</mark>, and instead you must wrap the columns in aggregation functions first. For example, the `SUM` in `Quantity = SUM(Sales[Order Quantity])`.
- **Storage** - Calculated columns (in Import storage mode tables) store a value for each row in the table, but a measure never stores values in the model.
- **Visual use** - Calculated columns (like any column) can be used to filter, group, or summarize (as an implicit measure), whereas measures are designed to summarize.

#### Calculated Columns vs Custom Columns

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-calculated-tables/4-technique)

There are three techniques that you can use to add columns to a model table:
- Add columns to a view or table (as a persisted column), and then source them in Power Query. This option only makes sense when your data source is a relational database and if you have the skills and permissions to do so. However, it's a good option because it supports ease of maintenance and allows reuse of the column logic in other models or reports.
- Add custom columns (using M) to Power Query queries.
- Add calculated columns (using DAX) to model tables.

Best practices:
* Use calculated columns only when:
	* You need to create a column for a **calculated table** 
	* The calculated column's DAX formula:
		* Depends on summarized model data.
		* Needs to use specialized modeling functions that are only available in DAX, such as the `RELATED` and `RELATEDTABLE` functions. 
			* Side note: Specialized functions can also include the [DAX parent and child hierarchies](https://learn.microsoft.com/en-us/dax/understanding-functions-for-parent-child-hierarchies-in-dax/), which are designed to naturalize a recursive relationship into columns.
				* For example, in an employee table where each row stores a reference to the row of the manager (who is also an employee).
* Otherwise, try to always use custom columns, as they load to the model in a more compact and optimal way.

## DAX Basic Syntax

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-write-formulas/2-formulas)

Basic syntax:
`<Calculation name> = <DAX formula>`

where `<Calculation name>` can be:
* calculated table
	* Example: `Ship Date = 'Date'` will duplicate `Date` table's data into `Ship Date` table.
* calculated column
	* Example: if the column used in the `<DAX formula>` is a fully qualified column (i.e., its name is unique across all other tables in the data model), then `Revenue = SUM([Sales Amount])`. Otherwise, we have to mention the table name, which is the best practice in both cases, like this: `Revenue = SUM(Sales[Sales Amount])`
* measure
	* Example: `Profit = [Revenue] - [Cost]`. Note: Unlike calculated columns, it is best practice not to add table name before measures.
		* why? measures are a model-level object. While they're assigned to a home table, it's only a cosmetic relationship to logically organize measures in the **Fields** pane.

So, the result of this expression can be:
* table object (calc. table)
* scalar value (calc. column & measure)

Tip: use [this](https://www.daxformatter.com/) DAX formatter to properly format DAX code.

Note 1: check out logical operators [here](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-write-formulas/5-operators#:~:text=%26%20%27Product%27%5BColor%5D-,Logical%20operators,-Use%20logical%20operators). Moreover, here's an example of `IN` operator:
Side note: the `IN` operator creates a logical OR condition between each row that is being compared to a table. Note: The table constructor syntax uses braces.
```EXCEL
ANZ Revenue =
CALCULATE(
    [Revenue],
    Customer[Country-Region] IN {
        "Australia",
        "New Zealand"
    }
)
```

Note 2 ([M source](<https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-calculated-tables/2-calculated-columns#:~:text=The%20addition%20operator%20(%2B)%20is%20evaluated%20before%20the%20text%20concatenation%20operator%20(%26).>)): <mark style="background: #FFB8EBA6;">The addition operator (+) is evaluated before the text concatenation operator (&).</mark>

Note 3: check out info about `FORMAT`'s date/time strings [here](https://learn.microsoft.com/en-us/dax/format-function-dax#custom-datetime-formats).
## DAX BLANK Data Type

* DAX uses BLANK for both database NULL and for blank cells in Excel. 
* BLANK doesn't mean zero.
* Think of it as the _absence of a value_.
* [`BLANK`](https://learn.microsoft.com/en-us/dax/blank-function-dax/) DAX function returns BLANK, while the [`ISBLANK`](https://learn.microsoft.com/en-us/dax/isblank-function-dax/) DAX function tests whether an expression evaluates to BLANK.
* Regarding how BLANK is dealt with in [implicit conversions](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-write-formulas/5-operators#:~:text=DAX%20operators.-,Implicit%20conversion,-When%20writing%20a):
	* It's handled similar to how Excel treats BLANK
	* It's different to how databases (SQL) treat NULL.
	* <mark style="background: #D2B3FFA6;">BLANK is treated as zero when acted on by arithmetic operators and as an empty string when concatenated to a string.</mark>

## DAX Variables

When creating one or more variables (using `VAR`), a `RETURN` clause is used to define the expression, which then refers to the variables.

Example of using variables: suppose you have this DAX formula to create a measure called `Revenue YOY %`:
``` EXCEL
Revenue YoY % =
DIVIDE(
    [Revenue]
        - CALCULATE(
            [Revenue],
            SAMEPERIODLASTYEAR('Date'[Date])
    ),
    CALCULATE(
        [Revenue],
        SAMEPERIODLASTYEAR('Date'[Date])
    )
)
```

Notice how the `CALCULATE(...)` part is repeated twice. So, to run this definition formula in at least half the time, let's define this part as a variable like so: ^4lu9ab
```EXCEL
Revenue YoY % =
VAR RevenuePriorYear =
    CALCULATE(
        [Revenue],
        SAMEPERIODLASTYEAR('Date'[Date])
    )
RETURN
    DIVIDE(
        [Revenue] - RevenuePriorYear,
        RevenuePriorYear
    )
```

## DAX Functions

### COUNT Related Functions

* [Count](https://learn.microsoft.com/en-us/dax/count-function-dax): Counts the number of rows **in** the specified **column** that contain **non-blank** values.
* [COUNTROWS](https://learn.microsoft.com/en-us/dax/countrows-function-dax): counts the number of rows **in** the specified **table**, or in a table defined by an expression.
* [DISTINCTCOUNT](https://www.reddit.com/r/PowerBI/comments/d2prhw/comment/ezwdpay/?utm_source=share&utm_medium=web2x&context=3): Counts the number of distinct rows of a table, **including blank**. 
* [DISTINCTCOUNTNOBLANK](https://www.reddit.com/r/PowerBI/comments/d2prhw/comment/ezwdpay/?utm_source=share&utm_medium=web2x&context=3): Counts the number of distinct rows from a column, **ignoring blanks**.

Example to differentiate between COUNT & COUNTROWS:
imagine you have a table called `Customer` that looks like this:
| cust_id | cust_name |
| ------- | --------- |
| 1       | 'ash'     |
| 2       | 'adam'    |
| 3       | ''        |
| 4   | BLANK     |
| BLANK   | BLANK          |

Then, `COUNT(Customer['cust_name'])` will be 3, while `COUNTROWS(Customer)` will be 5
(I think)

### Iterator Functions

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-iterator-functions/1-introduction)

* Iterator functions enumerate all rows of a given table and evaluate a given expression for each row.
* For any iterator function, you must pass in a table and an expression.
	* The table can be a model table reference or an expression that returns a table object.
	* The expression must evaluate to a scalar (single) value.
* Side note: Single-column summarization functions (e.g., SUM) are implicitly converted to their iterator counterpart (e.g., SUMX)

The following example illustrates different aspects of an iterator function (filter and row contexts) (M source: the video found [here](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-iterator-functions/1-introduction)):
![[Pasted image 20231006082949.png]]
Side note: In Power BI's UI, if we didn't add the InventoryKey -> 5,6 filter, then the returned sales table would've contained all the table.

Important note: pleas understand the filter context part (1) in the image above. Consider this other example for illustrating this concept ([M source 1](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/2-statistical-summary#:~:text=Start%20by%20creating%20a%20new%20measure%20called%20Top%2010%20Products.%20Then%2C%20use%20the%20TOPN%20function%2C%20along%20with%20the%20SUMX%20function%2C%20to%20calculate%20your%20top%2010%20products%20by%20total%20sales%2C%20as%20follows), [M source 2](https://learn.microsoft.com/en-us/dax/topn-function-dax)):
```EXCEL
Top 10 Products =
SUMX(TOPN(10, Product, Product[Total Sales]), [Total Sales])
```
The DAX expression above is useful if we want to present the top 10 in a different context, such as how much of the top 10 best-selling products contributed toward the overall total sales:
![[Pasted image 20231014122341.png]]
So in the image above, notice that because the selected visual filters the `Product` table by country, the `Product` part of the DAX expression above will change depending on the current country filter applied. For example, to visualize the first bar, the expression above was evaluated such that the `Product` table only contains rows related to `United States` value in the `Country` column. 

#### Changing AVERAGEX Count of Values to Get Higher Grain Summarizations

Suppose we have the following tables:
![[Pasted image 20231006085044.png]]
Such that `Sales Order`:
![[Pasted image 20231006085717.png]]
and `Sales`:
![[Pasted image 20231006085743.png]]

Now, suppose the required task is the following: "get the average revenue".
We know that the average means the sum of values divided by the count of values. However, that theory raises a question: What does the count of values represent?

If we'd like the "count of values" to be the count of sales order lines, then we'll get the following measure using DAX:
```EXCEL
Revenue Avg =
AVERAGEX(
    Sales,
    Sales[Order Quantity] * Sales[Unit Price] * (1 - Sales[Unit Price Discount Pct])
)
```
because each row in the **Sales** table records a sales order line, it can be more precisely described as _revenue per order line_. Accordingly, you should rename the **Revenue Avg** measure as **Revenue Avg Order Line** so that it's clear to report users about what's being used as the average base.
The result (if visualized in a table matrix) will be something like this:
![[Pasted image 20231006090256.png]]

Moreover, if we'd like to raise the granularity to the sales order level (a sales order consists of one or more order lines), then we'll add the following measure:
```EXCEL
Revenue Avg Order =
AVERAGEX(
    VALUES('Sales Order'[Sales Order]),
    [Revenue]
)
```
Result:
![[Pasted image 20231006090308.png]]

As expected, the average revenue for an order is always higher than the average revenue for a single order line.

Notes:
* Regarding how iterator functions count values: 
	* the count of values is the number of expressions that doesn't evaluate to BLANK.
* Regarding the [`VALUES`](https://learn.microsoft.com/en-us/dax/values-function-dax/) DAX function:
	* When the input parameter is a column name, returns a one-column table that contains the distinct values from the specified column. Duplicate values are removed and only unique values are returned. A BLANK value can be added.
		* So in our example above, the passed argument is a column name, so the table returned contains the distinct `Sales Order` values (e.g., `SO43659`, `SO43660`, `SO43661`), so the average's denominator in that case is 3 instead of 8 (the count of the sales order lines)
	* When the input parameter is a table name, returns the rows from the specified table. Duplicate rows are preserved. A BLANK row can be added.
	* Remark: When you use the VALUES function in a context that has been filtered, the unique values returned by VALUES are affected by the filter.
		* To disregard existing filters, use [ALL](https://learn.microsoft.com/en-us/dax/all-function-dax) function instead.


#### RANKX Function

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-iterator-functions/3-calculate-ranks)

Syntax:
```EXCEL
RANKX(<table>, <expression>[, <value>[, <order>[, <ties>]]])
```
read it's [documentation](https://learn.microsoft.com/en-us/dax/rankx-function-dax) to understand each of its arguments.

Example: to rank products by their quantity, add the following measure to a table:
```EXCEL
Product Quantity Rank =
RANKX(
    ALL('Product'[Product]),
    [Quantity]
)
```
Result:
![[Pasted image 20231006092316.png]]
Couple of things to notice:
* We use [`ALL`](https://learn.microsoft.com/en-us/dax/all-function-dax/), not [`VALUES`](https://learn.microsoft.com/en-us/dax/values-function-dax/), in RANKX, because the table visual will group by product (which is a filter on the **Product** table).
* In the screenshot above, notice that we have the following ranks: `10, 10, 12`. This is because we didn't pass a `<ties>` argument, so it defaulted to `'Skip'`.
	* If we don't want this, then execute this instead: `Product Quantity Rank = RANKX( ALL('Product'[Product]), [Quantity], , , DENSE )`.
		* The result in that case will be `10, 10, 11`.

Now, at the end of the screenshot above, we'll have something like this:
![[Pasted image 20231006092701.png]]
The reason is because the total for all products is ranked. 
It's not appropriate to rank total products, so you will now use the following logic to modify the measure definition to return BLANK, unless a single product is filtered:
```EXCEL
Product Quantity Rank =
IF(
    HASONEVALUE('Product'[Product]),
    RANKX(
        ALL('Product'[Product]),
        [Quantity],
        ,
        ,
        DENSE
    )
)
```

Filter context and the `HASONEVALUE` function will be introduced later when talking about filter context.

### Filter Context Functions

#### CALCULATE and FILTER Functions

You can use the [`CALCULATE`](https://learn.microsoft.com/en-us/dax/calculate-function-dax/) DAX function to modify filter context in your formulas.
Syntax:
```EXCEL
CALCULATE(<expression>, [[<filter1>], <filter2>]…)
```
Filters can be:
* Boolean expressions, which must have the following rules:
	* They can reference only a single column.
	- They cannot reference measures.
	- They cannot use functions that scan or return a table that includes aggregation functions like `SUM`.
	- Example: `Revenue Red = CALCULATE([Revenue], 'Product'[Color] = "Red")`
* table expressions
	* A table expression filter applies a table object as a filter.
		* it's likely a DAX function that returns a table object.
		* Its rows are a subset of those rows that were passed in, meaning the rows where the expression evaluated as `TRUE`.
	* Commonly, you'll use the [`FILTER`](https://learn.microsoft.com/en-us/dax/filter-function-dax/) DAX function to apply complex filter conditions, including those that can't be defined by a Boolean filter expression. The `FILTER` function is classed as an [[#Iterator Functions|iterator function]], and so you would pass in a table, or table expression, and an expression to evaluate for each row of that table.
	* Example: the use of `FILTER` here:
```EXCEL
Revenue Red =
CALCULATE(
	[Revenue],
	FILTER(
		'Product',
		'Product'[Color] = "Red"
	)
)
```

Note 1: from the two `Revenue Red` DAX formula examples above, we can see that All filter expressions that are passed in to the `CALCULATE` function are table filter expressions. A Boolean filter expression is a shorthand notation to improve the writing and reading experience. Internally, <mark style="background: #FFB8EBA6;">Microsoft Power BI translates Boolean filter expressions to table filter expressions</mark>, which is how it translates your **Revenue Red** measure definition.

Other side notes:
* When you have multiple filters, they're evaluated by using the `AND` logical operator
* The [`CALCULATETABLE`](https://learn.microsoft.com/en-us/dax/calculatetable-function-dax/) DAX function is similar to `CALCULATE`, however, its return value is the value that is the result of the expression **but wrapped in a table**.

#### Using CALCULATE for Context Transitions

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-modify-filter/5-context-transition)

Case scenario: 
Suppose you're writing a calculated column formula or an iterator function (where both use row context). Now, in the middle of this formula, you realize that you need to evaluate a measure expression, but since measures are using filter context, you'll need to make a context transition from filter context to row context.

Illustration:
In the following example, you will add a calculated column to the **Customer** table to classify customers into a loyalty class. The scenario is simple: When the revenue that is produced by the customer is less than $2500, the customer is classified as **Low**; otherwise they're classified as **High**. We'll write all possible DAX expressions, and then explain the results of each one

```EXCEL
Customer Segment Broken =
VAR CustomerRevenue = SUM(Sales[Sales Amount])
RETURN
    IF(CustomerRevenue < 2500, "Low", "High")

Customer Segment With Calculate =
VAR CustomerRevenue = CALCULATE(SUM(Sales[Sales Amount])) // [*]
RETURN
    IF(CustomerRevenue < 2500, "Low", "High")

Customer Segment With Measure = 
VAR CustomerRevenue = [Revenue] // where Revenue is a previously made measure of [*]
RETURN
    IF(CustomerRevenue < 2500, "Low", "High")

```

Result of `Customer Segment Broken`:
![[Pasted image 20231006161034.png]]
Result of `Customer Segment With Calculate` or `Customer Segment With Measure`:
![[Pasted image 20231006161412.png]]

Explanations:
* Case 1: the calculated column formula produces an incorrect result: Each customer is assigned the value of **High** because the expression `SUM(Sales[Sales Amount])` isn't evaluated in a filter context. Instead, it's evaluated in a row context, so each customer is assessed on the sum of _every_ **Sales Amount** column value in the **Sales** table.
*  Case 2: Fixes case 1 by forcing the evaluation of the `SUM(Sales[Sales Amount])` expression _for each customer_ using `CALCULATE` to make a context transition that applies the row context column values to filter context. Alternatively, if you've a previously defined measure (e.g., `Revenue`) and evaluate that in row context, context transition will happen automatically. Thus, you don't need to pass measure references to the `CALCULATE` function.

Now, recall in the example of sales commission mentioned in the [[#VALUES, HASONEVALUE, and SELECTEDVALUE Functions (to Examine Filter Context)|VALUES-HASONEVALUE-SELECTEDVALUE section]], we can now modify this example to display the total sales commission like so:
![[Pasted image 20231006162041.png]]

Using iterator function `SUMX` in this DAX expression:
```EXCEL
Sales Commission =
SUMX(
    VALUES('Sales Territory'[Region]),
    CALCULATE(
        [Revenue]
        * IF(
            VALUES('Sales Territory'[Country]) = "United States",
            0.15,
            0.1
        )
    )
)
```
Note: it is meaningless to replace the inner `VALUES` with `SELECTEDVALUE` in this case, as it is no longer needed to test whether a single Country column value in the Sales Territory table is in filter context because it's known to be filtering by a single country (because it's iterating over the regions in filter context and a region belongs to only one country).

#### REMOVEFILTERS Function

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-modify-filter/3-filter-modifier-functions)

* Use the [`REMOVEFILTERS`](https://learn.microsoft.com/en-us/dax/removefilters-function-dax/) DAX function as a `CALCULATE` filter expression to remove filters from filter context. It can remove filters from one or more columns or from all columns of a single table.
	* Side note: The `REMOVEFILTERS` function is relatively new. In previous versions of DAX, you removed filters by using the [`ALL`](https://learn.microsoft.com/en-us/dax/all-function-dax/) DAX function or variants including the [`ALLEXCEPT`](https://learn.microsoft.com/en-us/dax/allexcept-function-dax/) and the [`ALLNOBLANKROW`](https://learn.microsoft.com/en-us/dax/allnoblankrow-function-dax/) DAX functions.

Example to illustrate:
Suppose we have this table:
![[Pasted image 20231006145032.png]]
When looking at the `Revenue` measure, we notice that the `SUM` of this measure is filtered based on the `Group`, `Country`, and `Region` columns of the `Sales Territory` table. Now, what if we want to get the total `SUM` that is not filtered by any of these columns? Answer: we remove all filters related to `Sales Territory` like so:
```EXCEL
Revenue Total Region = CALCULATE([Revenue], REMOVEFILTERS('Sales Territory'))
```
The result of this DAX expression can be seen in the `Revenue Total Region` measure in the screenshot above.  Now, while this result on its own isn't useful, when it's used as a denominator in a ratio, it calculates a percent of grand total. Therefore, you will now overwrite the **Revenue Total Region** measure definition with the following definition:
```EXCEL
Revenue % Total Region =
VAR CurrentRegionRevenue = [Revenue]
VAR TotalRegionRevenue =
    CALCULATE(
        [Revenue],
        REMOVEFILTERS('Sales Territory')
    )
RETURN
    DIVIDE(
        CurrentRegionRevenue,
        TotalRegionRevenue
    )
```
Result is shown in the `Revenue % Total Region` measure above.

Now, what if we want to calculate the ratio of revenue for a region divided by its country's revenue? Answer: Remove `Region` filter only in `Sales Territory` table like so:
```EXCEL
Revenue % Total Country =
VAR CurrentRegionRevenue = [Revenue]
VAR TotalCountryRevenue =
    CALCULATE(
        [Revenue],
        REMOVEFILTERS('Sales Territory'[Region])
    )
RETURN
    DIVIDE(
        CurrentRegionRevenue,
        TotalCountryRevenue
    )
```
The result can be seen in the `Revenue % Total Country` measure above.

Similarly, we can calculate the region revenue as a ratio of its group's revenue by adding `'Sales Territory'[Country]` as a second REMOVEFILTERS argument to the code above, where the result can be seen in the `Revenue % Total Group` measure above.

#### KEEPFILTERS Function

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-modify-filter/3-filter-modifier-functions#:~:text=its%20group%27s%20revenue.-,Preserve%20filters,-You%20can%20use)

You can use the [`KEEPFILTERS`](https://learn.microsoft.com/en-us/dax/keepfilters-function-dax/) DAX function as a filter expression in the `CALCULATE` function to preserve filters.

The following example illustrates KEEPFILTERS vs FILTER vs CALCULATE functions:
Suppose you have this table (source: a personally modified version of [this](https://github.com/MicrosoftDocs/mslearn-dax-power-bi/raw/main/activities/Adventure%20Works%20DW%202020%20M06.pbix) file ):
![[Pasted image 20231006145313.png]]
Lets' see how each of the 3 measures are calculated:
```EXCEL
Revenue Red With CALCULATE Only = 
CALCULATE ( 
 [Revenue], 
 Product[Color] = "Red"
)

Revenue Red With KEEPFILTERS = 
CALCULATE(
    [Revenue],
    KEEPFILTERS(Product[Color] = "Red")
)

Revenue Red With FILTERS = 
CALCULATE(
    [Revenue],
    FILTER(
        'Product',
        Product[Color] = "Red"
    )
)
```

Now, [this](https://community.fabric.microsoft.com/t5/Desktop/Conceptual-Question-FILTER-vs-KEEPFILTERS-vs-neither-What-is-the/m-p/1444071/highlight/true#M606196) great article explains in depth the inner-workings of each of these functions (which also talks about using [VALUES](https://learn.microsoft.com/en-us/dax/values-function-dax) function), but to summarize, let's see how Power BI internally transforms these expressions:
```EXCEL
INTERNAL Revenue Red With CALCULATE Only = 
CALCULATE ( 
 [Revenue], 
 FILTER(
  ALL(Product[Color]),
  Product[Color] = "Red"
 )
)

INTERNAL Revenue Red With KEEPFILTERS = 
CALCULATE(
    [Revenue],
    KEEPFILTERS(
     FILTER(
      ALL(Product[Color]),
      Product[Color] = "Red"
     )
    )
)

INTERNAL Revenue Red With FILTERS = 
CALCULATE(
    [Revenue],
    FILTER(
        'Product', // note: VALUES(Product[Color]) can be used here as well
        Product[Color] = "Red"
    )
)
```

Now, we notice the following:
* `Revenue Red With CALCULATE Only` is the only measure that spans the result over all rows.
	* This is because internally, Power BI uses [ALL](https://learn.microsoft.com/en-us/dax/all-function-dax) function which ignores any filters that might have been applied (so in our case, the filter applied by the `Color` column is ignored).
* `KEEPFILTERS` and `FILTER` return the same result with the same appearance in the table above, however:
	* The **FILTER()** uses two queries as opposed to the **KEEPFILTERS()** which uses only one query. Therefore, KEEPFILTERS is faster, and is therefore preferable ([source](<https://michalmolka.medium.com/dax-keepfilters-vs-filter-8f3fb519ccaf#:~:text=The%20FILTER()%20uses%20two,values%20from%20the%20function's%20arguments.>)). ^a8h0ge

#### USRELATIONSHIP Function (for Inactive Relationships)

An inactive model relationship can only propagate filters when the [`USERELATIONSHIP`](https://learn.microsoft.com/en-us/dax/userelationship-function-dax/) DAX function is passed as a filter expression to the `CALCULATE` function. When you use this function to engage an inactive relationship, the active relationship will automatically become inactive.

Review an example of a measure definition that uses an inactive relationship to calculate the **Revenue** measure by shipped dates:
```EXCEL
Revenue Shipped =
CALCULATE (
    [Revenue],
    USERELATIONSHIP('Date'[DateKey], Sales[ShipDateKey])
)
Mod
```

Side note: 
* You can modify the model relationship behavior when an expression is evaluated by passing the [`CROSSFILTER`](https://learn.microsoft.com/en-us/dax/crossfilter-function/) DAX function as a filter expression to the `CALCULATE` function. It's an advanced capability.
	* The `CROSSFILTER` function can modify filter directions (from both to single or from single to both) and even disable a relationship.

#### VALUES, HASONEVALUE, and SELECTEDVALUE Functions (to Examine Filter Context)

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-modify-filter/4-examine-filter-context)

The [`VALUES`](https://learn.microsoft.com/en-us/dax/values-function-dax/) DAX function lets your formulas determine what values are in filter context. Syntax: `VALUES(<TableNameOrColumnName>)`

* The `VALUES` function always returns a table object
	* When a returned table contains multiple rows, we won't be able to test if a specific value is in the filter context.
		* To fix this, our formula must first test that the `VALUES` function returns a single row. Two functions can help us with this: the [`HASONEVALUE`](https://learn.microsoft.com/en-us/dax/hasonevalue-function-dax/) and the [`SELECTEDVALUE`](https://learn.microsoft.com/en-us/dax/selectedvalue-function/) DAX functions.

The following measure example illustrates how to HASONEVALUE:
```EXCEL
Sales Commission =
[Revenue]
    * IF(
        HASONEVALUE('Sales Territory'[Country]),
        IF(
            VALUES('Sales Territory'[Country]) = "United States",
            0.15,
            0.1
        )
    )
```

Note: it is preferable to replace `VALUES` with `SELECTEDVALUE` whenever applicable ([M source](https://learn.microsoft.com/en-us/dax/best-practices/dax-selectedvalue)), so the code above could be updated to be the following:
```EXCEL
Sales Commission =
[Revenue]
    * IF(
		SELECTEDVALUE('Sales Territory'[Country]) = "United States"),
		0.15,
		0.1
    )
```
Result:
![[Pasted image 20231006153817.png]]
Notice that the total Sales Commission result is BLANK. The reason is because multiple values are in filter context for the Country column in the Sales Territory table. In this case, the HASONEVALUE function returns FALSE, which results in the Revenue measure being multiplied by BLANK (a value multiplied by BLANK is BLANK). Side note: to produce a total, you will need to use an iterator function, which is explained later in this module.

Note: Three other functions that you can use to test filter state are:
- [`ISFILTERED`](https://learn.microsoft.com/en-us/dax/isfiltered-function-dax/) - Returns `TRUE` when a passed-in column reference is _directly_ filtered.
- [`ISCROSSFILTERED`](https://learn.microsoft.com/en-us/dax/iscrossfiltered-function-dax/) - Returns `TRUE` when a passed-in column reference is _indirectly_ filtered. A column is cross-filtered when a filter that is applied to another column in the same table, or in a related table, affects the reference column by filtering it.
- [`ISINSCOPE`](https://learn.microsoft.com/en-us/dax/isinscope-function-dax/) - Returns `TRUE` when a passed-in column reference is the level in a hierarchy of levels.

Example that uses `ISINSCOPE`: 
```EXCEL
Revenue % Total Country =
VAR CurrentRegionRevenue = [Revenue]
VAR TotalCountryRevenue =
    CALCULATE(
        [Revenue],
        REMOVEFILTERS('Sales Territory'[Region])
    )
RETURN
    IF(
        ISINSCOPE('Sales Territory'[Region]),
        DIVIDE(
            CurrentRegionRevenue,
            TotalCountryRevenue
        )
    )
```
Result:
![[Pasted image 20231006154002.png]]
In the matrix visual, notice that Revenue % Total Country values are now only displayed when a region is in scope.

### Time Intelligence Functions

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-time-intelligence/1-introduction)

* Time intelligence relates to calculations over time <mark style="background: #FFB86CA6;">using measures, not calculated columns</mark>.
* In DAX, time intelligence means **_modifying the filter context for date filters_**.
* They can help you answer these time-related questions like:
	* What's the accumulation of revenue for the year, quarter, or month?
	- What revenue was produced for the same period last year?
	- What growth in revenue has been achieved over the same period last year?
	- How many new customers made their first order in each month?
	- What's the inventory stock on-hand value for the company's products?
* Important note: Many DAX time intelligence functions are ***concerned with standard date periods***, specifically years, quarters, and months. <mark style="background: #FFB8EBA6;">If you have "irregular time periods", or you need to work with weeks or time periods, then you'll need to use the `CALCULATE` function and pass in hand-crafted date or time filters.</mark> More about CALCULATE function [[#CALCULATE and FILTER Functions|here]].
	*  Side note: An Example of an "irregular time period" are financial months that begin mid-way through the calendar month.

#### Summarizations Over Time Functions

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-time-intelligence/2-functions)

One group of DAX time intelligence functions is concerned with summarizations over time:

- [`DATESYTD`](https://learn.microsoft.com/en-us/dax/datesytd-function-dax/) - Returns a single-column table that contains dates for the year-to-date (YTD) in the current filter context. This group also includes the [`DATESMTD`](https://learn.microsoft.com/en-us/dax/datesmtd-function-dax/) and [`DATESQTD`](https://learn.microsoft.com/en-us/dax/datesqtd-function-dax/) DAX functions for month-to-date (MTD) and quarter-to-date (QTD). You can pass these functions as filters into the [`CALCULATE`](https://learn.microsoft.com/en-us/dax/calculate-function-dax/) DAX function.
- [`TOTALYTD`](https://learn.microsoft.com/en-us/dax/totalytd-function-dax/) - Evaluates an expression for YTD in the current filter context.
- [`DATESBETWEEN`](https://learn.microsoft.com/en-us/dax/datesbetween-function-dax/) - Returns a table that contains a column of dates that begins with a given start date and continues until a given end date.
- [`DATESINPERIOD`](https://learn.microsoft.com/en-us/dax/datesinperiod-function-dax/) - Returns a table that contains a column of dates that begins with a given start date and continues for the specified number of intervals.

Important note:
While the `TOTALYTD` function is simple to use, you are limited to passing in one filter expression. If you need to apply multiple filter expressions, use the `CALCULATE` function and then pass the `DATESYTD` function in as one of the filter expressions.

##### Using TOTALYTD

Example syntax:
```EXCEL
TOTALYTD(<expression>, <dates>, [, <filter>][, <year_end_date>])
```
Example with values:
```EXCEL
Revenue YTD = TOTALYTD([Revenue], 'Date'[Date], "6-30")
```
note: The year-end date value of `"6-30"` represents June 30.
Result when adding `Revenue YTD` column to the table in the screenshot below:
![[Pasted image 20231005220605.png]]
Notice that it produces a summarization (i.e., accumulation) of the revenue amounts from the beginning of the year through to the filtered month.

##### Using DATESBETWEEN

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-time-intelligence/3-calculations)

* We need to calculate the number of new customers for a time period.
	* A new customer is counted in the time period in which they **made their first purchase**.
		* silly example for illustration: suppose that in each of the following days, we had these customer ids of purchases:
			* day 1 -> 1, 2, 3
			* day 2 -> 1, 4, 5
			* day 3 -> 1, 6, 7
		* Then:
			* DISTINCTCOUNT of day 1 -> 3
			* DISTINCTCOUNT of days 1 and 2 -> 5
			* DISTINCTCOUNT of days 1, 2, and 3 -> 7
		* Then, to get the number of customers who made **their very first purchases** on the third day, we do: 7 - 5 = 2 (which are ids 6 and 7)
		* side note: we can't just get the DISTINCTCOUNT of day 3 alone, because that will give us 3, but customer id 1 has already made a purchase before
* Now, to get that, we need to first get the number of distinct customers life-to-date (`CustomersLTD`)
	* Life-to-date means from the beginning of time until the last date in filter context.
* Then, we subtract the count of distinct customers before the time period in filter context (`CustomersPrior`) from `CustomersLTD`.

DAX expression for this:
```EXCEL
New Customers By Sub From Prior =
VAR CustomersLTD =
    CALCULATE(
        DISTINCTCOUNT(Sales[CustomerKey]),
        DATESBETWEEN(
            'Date'[Date],
            BLANK(),
            MAX('Date'[Date])
        ),
    'Sales Order'[Channel] = "Internet"
    )
VAR CustomersPrior =
    CALCULATE(
        DISTINCTCOUNT(Sales[CustomerKey]),
        DATESBETWEEN(
            'Date'[Date],
            BLANK(),
            MIN('Date'[Date]) - 1
        ),
        'Sales Order'[Channel] = "Internet"
    )
RETURN
    CustomersLTD - CustomersPrior
```
Result:
![[Pasted image 20231006181644.png]]
Notes: 
* `Customers LTD` measure is a DAX formula of just the `CustomersLTD` DAX variable
* (In the purple highlight) Notice how Power BI is intelligent enough to add the values when we're not accumulating, and to display the last value when we're accumulating (in both cases, `2459` is returned)
* The `New Customers By Using MIN and MAX` measure was a fault attempt by me to replicate the DAX formula of `NEW Customers By Sub From Prior`, where I tried to use `MIN` and `MAX` instead. This logically won't work, and you can check the reason [here](https://community.fabric.microsoft.com/t5/DAX-Commands-and-Tips/Question-About-Behavior-of-DATESBETWEEN/m-p/3464080/thread-id/132158#M132162).

#### Using `LASTDATE` Function for Snapshot Calculations

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-time-intelligence/3-calculations#:~:text=Snapshot%20calculations)

* Occasionally, fact data is stored as snapshots in time. Common examples include inventory stock levels or account balances. A snapshot of values is loaded into the table on a periodic basis.
* Since each date has its own values which could be overlapping with previous dates' values, it doesn't logically make sense to summarize valuues across date.
	* Example: Adding stock level counts across product categories produces a meaningful summary, but adding stock level counts across dates does not.
		* In other words, Adding yesterday's stock level to today's stock level isn't a useful operation to perform

Example: add a measure to the Inventory table that sums the UnitsBalance value for a single date. The date will be the last date of each time period:
```EXCEL
Stock on Hand =
CALCULATE(
    SUM(Inventory[UnitsBalance]),
    LASTDATE('Date'[Date])
)
```
<mark style="background: #FFB8EBA6;">Technical note</mark>: recall that `LASTDATE` returns a single row of the last date in the current filter context. However, we still have to "aggregate" that row using `SUM`, since measures don't allow direct references to columns.
Result:
![[Pasted image 20231006182745.png]]
The measure returns BLANKs for June 2020 because no record exists for the last date in June. According to the data, it hasn't happened yet. To solve this, use the [`LASTNONBLANK`](https://learn.microsoft.com/en-us/dax/lastnonblank-function-dax/) DAX function:
```EXCEL
Stock on Hand =
CALCULATE(
    SUM(Inventory[UnitsBalance]),
    LASTNONBLANK(
        'Date'[Date],
        CALCULATE(SUM(Inventory[UnitsBalance]))
    )
)
```
Result:
![[Pasted image 20231006182825.png]]
Note:
* The `LASTNONBLANK` function is an iterator function:
	* It returns the last date that produces a non-BLANK result. 
		* It achieves this result by iterating through all dates in filter context _in descending chronological order_.
			* When it encounters a non-BLANK result, the function returns the date. That date is then used to filter the `CALCULATE` function.
	* <mark style="background: #FF5582A6;">Technical note</mark>: The LASTNONBLANK function evaluates its expression in row context. The CALCULATE function must be used to [[#Using CALCULATE for Context Transitions|transition the row context to filter context]] to correctly evaluate the expression.



#### Comparions Over Time Functions

Another group of DAX time intelligence functions is concerned with shifting time periods:
- [`DATEADD`](https://learn.microsoft.com/en-us/dax/dateadd-function-dax/) - Returns a table that contains a column of dates, shifted either forward or backward in time by the specified number of intervals from the dates in the current filter context.
- [`PARALLELPERIOD`](https://learn.microsoft.com/en-us/dax/parallelperiod-function-dax/) - Returns a table that contains a column of dates that represents a period that is parallel to the dates in the specified dates column, in the current filter context, with the dates shifted a number of intervals either forward in time or back in time.
- [`SAMEPERIODLASTYEAR`](https://learn.microsoft.com/en-us/dax/sameperiodlastyear-function-dax/) - Returns a table that contains a column of dates that are shifted one year back in time from the dates in the specified dates column, in the current filter context.
- Many helper DAX functions for navigating backward or forward for specific time periods, all of which returns a table of dates. These helper functions include [`NEXTDAY`](https://learn.microsoft.com/en-us/dax/nextday-function-dax/), [`NEXTMONTH`](https://learn.microsoft.com/en-us/dax/nextmonth-function-dax/), [`NEXTQUARTER`](https://learn.microsoft.com/en-us/dax/nextquarter-function-dax/), [`NEXTYEAR`](https://learn.microsoft.com/en-us/dax/nextyear-function-dax/), and [`PREVIOUSDAY`](https://learn.microsoft.com/en-us/dax/previousday-function-dax/), [`PREVIOUSMONTH`](https://learn.microsoft.com/en-us/dax/previousmonth-function-dax/), [`PREVIOUSQUARTER`](https://learn.microsoft.com/en-us/dax/previousquarter-function-dax/), and [`PREVIOUSYEAR`](https://learn.microsoft.com/en-us/dax/previousyear-function-dax/).

Example: add a measure to the **Sales** table that calculates revenue for the prior year by using the `SAMEPERIODLASTYEAR` function:
```EXCEL
Revenue PY =
VAR RevenuePriorYear = CALCULATE([Revenue], SAMEPERIODLASTYEAR('Date'[Date]))
RETURN
    RevenuePriorYear
```
When adding to table:
![[Pasted image 20231005220808.png|380]]
Notice that it produces results that are similar to the previous year's revenue amounts.

Another example of calculating the yearly change ratio is shown [here](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-time-intelligence/2-functions#:~:text=to%20calculate%20the-,change%20ratio,-.%20Be%20sure%20to).

# Fixing Performance Issues

[M source](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/1-introduction)

## Using Performance analyzer to Find Bottlenecks

[M source](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/2-performance)

You can use Performance analyzer in Power BI Desktop to help you find out how each of your report elements are performing when users interact with them. To use this tool, we have to follow these prerequisites:
* Create a new empty page and focus on it.
* Close Power BI desktop, then reopen it (done to clear [visual cache](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/2-performance#:~:text=data%20engine%20cache.-,Visual%20cache,-%2D%20When%20you%20load))
* If we just want to clear the [data engine cache](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/2-performance#:~:text=the%20blank%20page.-,Data%20engine%20cache,-%2D%20When%20a%20query), then we can connect DAX Studio to the data model and then call Clear Cache.

Then:
![[Pasted image 20231007112753.png]]
Then we select the page of the report that we want to analyze, and interact with the elements of the report that we want to measure. We will see the results of your interactions display in the Performance analyzer pane as we work. When we are finished, we'll select the Stop button.

For more detailed information, see [Use Performance Analyzer to examine report element performance](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-performance-analyzer/).

To review the tasks in order of duration, longest to shortest, right-click the **Sort** icon next to the **Duration (ms)** column header, and then select **Total time** in **Descending** order:
![[Pasted image 20231007112954.png]]

The log information for each visual shows how much time it took (duration) to complete the following categories of tasks:
![[Pasted image 20231007113032.png]]
- **DAX query** - The time it took for the visual to send the query, along with the time it took Analysis Services to return the results.
	- To analyze your queries in more detail, you can use DAX Studio, which is a free, open-source tool that is provided by another service.
- **Visual display** - The time it took for the visual to render on the screen, including the time required to retrieve web images or geocoding.
- **Other** - The time it took the visual to prepare queries, wait for other visuals to complete, or perform other background processing tasks. 
	- If this category displays a long duration, the only real way to reduce this duration is to **optimize DAX queries for other visuals, or reduce the number of visuals in the report**.



## General Tips

[M source 1](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/2-performance), [M source 2](https://learn.microsoft.com/en-us/training/modules/get-data/8-performance-issues)

Tips on how to optimize Power BI performance (i.e., decrease the time it takes to render report pages and update visuals): 
* Regarding original data source:
	* **Process as much data as possible in the original data source.** Power Query and Power Query Editor allow you to process the data; however, the processing power that is required to complete this task might lower performance in other areas of your reports. Generally, a good practice is to process, as much as possible, in the native data source. For example, if you have large data models, or data that is anticipated to quickly grow over time, you can follow one of these options:
		* use a summary (i.e., aggregation) table from the data source ([M source](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/6-aggregations)).
			* Example: a detail table might contain every transaction, a summary table would contain one record per day, per week, or per month. It might be an average of all of the transactions per day, for instance.
			* You can create aggregations in different ways and each method will yield the same results, for example:
				* If you have access to the database, you could either create a table or a view with the aggregation and then import that into Power BI
				* If not, you can use Power Query Editor to create the aggregations step-by-step (example is found [here](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/6-aggregations#:~:text=step%2Dby%2Dstep.-,In%20this%20example,-%2C%20you%20open%20a), and in-depth info is found [here](https://learn.microsoft.com/en-us/power-bi/enterprise/aggregations-auto)).
		* Use a Mixed mode design (to produce a composite model).
			* set the **Storage Mode** property to **DirectQuery** for larger fact-type tables.
			* This is done when we want to mitigate the disadvantage of losing the ability to drill into data because the detail no longer exists when we fully rely on summary tables ([M source](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/4-reduce-cardinality#:~:text=disadvantage%20is%20that,or%20DirectQuery.)).
		* Instead of performing complex column calculations in Power BI, perform them in the original data source ([M source](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/5-directquery-models#:~:text=Avoid%20the%20use%20of%20complex%20calculated%20columns%20because%20the%20calculation%20expression%20will%20be%20embedded%20into%20the%20source%20queries.%20It%20is%20more%20efficient%20to%20push%20the%20expression%20back%20to%20the%20source%20because%20it%20avoids%20the%20push%20down)).
		* Add surrogate key columns to dimension-type tables when applicable.
		* In the original data source, review the indexes and verify that the current indexing is correct. If you need to create new indexes, ensure that they are appropriate ([M source](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/5-directquery-models#:~:text=Review%20the%20indexes%20and%20verify%20that%20the%20current%20indexing%20is%20correct.%20If%20you%20need%20to%20create%20new%20indexes%2C%20ensure%20that%20they%20are%20appropriate.)).
* Regarding options from Power BI UI itself:
	* It is generally recommended to keep the auto date/time feature, however, if the schema already has a table which is marked as date table, then you can disable this feature by going to File > Options and settings > Options, and then select "Current File" page, and unchecking the option.
	* When using **DirectQuery** storage mode, we can apply one of the following **query reduction options**:
		* *Reduce number of queries sent by* - By default, every visual interacts with every other visual. Selecting this check box disables that default interaction. You can then optionally choose which visuals interact with each other by using the **Edit interactions** feature.
		* *Slicers* - By default, the Instantly apply slicer changes option is selected. To force the report users to manually apply slicer changes, select the **Add an apply button to each slicer to apply changes when you're ready** option. ^e1vpye
		* *Filters* - By default, the Instantly apply basic filter changes option is selected. To force the report users to manually apply filter changes, select one of the alternative options:
			* Add an apply button to all basic filters to apply changes when you're ready
			* Add a single apply button to the filter pane to apply changes at once (preview)
			  ![[Pasted image 20231007122635.png]]
* Regarding visuals:
	* Per report page, try to limit the number of visuals to the important ones only.
		* If all the information is important, see if you can present that info as drill-through pages and/or report page tooltips.
	* Per visual, limit the number of fields (measures or columns) to 100 or less.
* Regarding DAX
	* Optimize the DAX code by using more efficient functions.
		* Example: [[Power BI#^a8h0ge|replacing FILTER with KEEPFILTERS whenever possible]]. Other examples are found [here](https://medium.com/@technologIT/optimizing-dax-code-for-directquery-tips-and-tricks-ab1b5e6fd91f) and [here](https://towardsdatascience.com/analyze-performance-when-aggregating-data-in-power-bi-and-dax-queries-fc00027950a3).
	* Try to use variables [[Power BI#^4lu9ab|when repeated code is found]] to decrease run time.
* Regarding the data model
	* Do not import columns that you don't need in any visuals or relationships.
	* make sure the columns' data types are correct.
	* Remove any useless rows found at the top/bottom of a table.
	* Make sure that each column is 100% valid and has 0% errors.
		* To make sure that this scan is done properly, at the bottom left status bar of Power Query, click on `Column profiling based on top 1000 rows` and change it to be for the whole table.
	* In columns, **Separate date and time, if bound together.** 
		* If any of your tables have columns that combine date and time, make sure that you separate them into distinct columns before importing them into Power BI. This approach will increase compression abilities ([Microsoft source](https://learn.microsoft.com/en-us/training/modules/get-data/8-performance-issues)).
	* Check that relationship cardinality properties are correctly configured. 
		* For example, a one-side column that contains unique values might be incorrectly configured as a many-side column.
		* Side note: Cardinality is also used in the context of the relationships between two tables, where it describes the direction of the relationship.
	*  Reduce the number of high cardinally columns (i.e., high unique column values) in your dataset, as lower cardinality leads to more optimized performance. ([M source](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/4-reduce-cardinality)).
	* ensure that both of the columns that you are using to participate in any relationship **are sharing the same data type** ([M source](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/4-reduce-cardinality#:~:text=ensure%20that%20both%20of%20the%20columns%20that%20you%20are%20using%20to%20participate%20in%20a%20relationship%20are%20sharing%20the%20same%20data%20type.)).

### Aggregations

In regards to optimizing the performance issues for **DirectQuery** storage mode:
we can use **DirectQuery user-defined aggregation tables** by adding user-defined aggregation tables to a DirectQuery model. 
User-defined aggregation tables are special model tables that are hidden (from users, calculations, and RLS). They work best when they satisfy higher-grain analytic queries over large fact tables. When you set the aggregation table to use DirectQuery storage mode, it can query a materialized view in the data source. You can also set an aggregation table to use import storage mode or enable automatic aggregations, and these options are described in Unit 4.

For more information, see [DirectQuery model guidance in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/guidance/directquery-model-guidance).

## Query Folding

ChatGPT:
Query Folding is a performance optimization feature in Power BI that allows the Power Query engine to push data transformation operations back to the data source, such as a database or web service, instead of performing them locally within Power BI. This can significantly improve query performance by reducing the amount of data transferred over the network and processed locally.

Example: Let's say you have a Power BI report that connects to a SQL database. You want to filter the data to only include records where the sales amount is greater than $1,000 and then aggregate the results. Without query folding, Power BI might first retrieve all the data from the database and then apply the filter and aggregation operations locally. With query folding, Power BI sends a SQL query to the database that includes the filter and aggregation operations, and the database performs these operations. This results in faster and more efficient data processing.


# Enforcing Security

[M source](https://learn.microsoft.com/en-us/training/modules/enforce-power-bi-model-security/1-introduction)

* We can enforce model security by restricting access to subset of data, and by restricting access to specific model tables and columns.
* Achieving this requirement commonly involves setting up row-level security (RLS), which involves defining roles and rules in that filter data model. We can also set up object-level security (OLS), to restrict access to entire tables or columns.

## Row-Level Security (RLS)

[M source](https://learn.microsoft.com/en-us/training/modules/enforce-power-bi-model-security/2-restrict-access-to-power-bi-model-data)

* set up RLS by creating one or more roles.
	* A role has a unique name in the model.
	* A role can include 0 or more rules.
		* Rules enforce filters on model tables by using Data Analysis Expressions (DAX) filter expressions.
		* 0 rules mean that the role has access to all model data.
		* Rule expressions are evaluated within [[#Row Context|row context]].
			* When the expression returns TRUE, the user can “see” the row.
		* Rules can be static or dynamic
			* Static rules use DAX expressions that refer to constants. 
				* Example 1: `'Region'[Region] = "Midwest"`. This has the following cascading effect ([M source](https://learn.microsoft.com/en-us/training/modules/enforce-power-bi-model-security/2-restrict-access-to-power-bi-model-data#:~:text=The%20following%20steps%20explain%20how%20Power%20BI%20enforces%20the%20rule)): `Region` table is filtered -> the `Region` table filter is propagated to `State` table -> same thing but from `State` to `Sales`. This propagation happen automatically due to the model relationships between these tables.
				* Example 2: To restrict access to all table rows, apply the following rule to a table: `FALSE()`
			* Dynamic rules use special DAX functions that return environmental values. Example functions include:
			* [USERNAME](https://learn.microsoft.com/en-us/dax/username-function-dax) or [USERPRINCIPALNAME](https://learn.microsoft.com/en-us/dax/userprincipalname-function-dax) – Returns the Power BI authenticated user as a text value.
				* <mark style="background: #FF5582A6;">Important note</mark> ([M source](https://learn.microsoft.com/en-us/training/modules/enforce-power-bi-model-security/2-restrict-access-to-power-bi-model-data#:~:text=Be%20aware%20that,principal%20name%20format.)): it is preferable to use the latter function, as the former returns `DOMAIN\username` in Power BI Desktop and `username@adventureworks.com` (i.e., User Principal Name (UPN)) in Power BI service. However, the latter function always return UPN.
			* [CUSTOMDATA](https://learn.microsoft.com/en-us/dax/customdata-function-dax) - Returns the **CustomData** property passed in the connection string. Non-Power BI reporting tools that connect to the dataset by using a connection string can set this property, like Microsoft Excel.
			* Example rule that restricts data access to the region(s) of the authenticated user: `'AppUser'[UserName] = USERPRINCIPALNAME()`. Thiss will compare the current user's UPN with the ones in the `AppUser` table which will map that user to a specific region, as can be seen by the image below:
			  ![[Pasted image 20231007170636.png]]
			* Another example ([M source](https://learn.microsoft.com/en-us/training/modules/row-level-security-power-bi/3-dynamic-method)):
			  ![[Pasted image 20231017150459.png]]
			  then:
			  ![[Pasted image 20231017150411.png]] 
	* Role management (creation, validation, etc.) can be done in the following environments:
		* SQL Server Data Tools (SSDT), if the models are from the Analysis Services of Azure or SQL Server
		* SQL Server Management Studio (SSMS) or third-party tools like [Tabular Editor](https://tabulareditor.com/) otherwise.
* It is better to apply a [[#Star schema design|start schema design]] to enforce rules that filter dimension tables, allowing [model relationships](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-relationships-understand) to efficiently propagate those filters to fact tables.
* Validate roles to ensure they apply the correct filters.
  ![[Pasted image 20231007171243.png]]
* To add members to the role in Power BI service ([M source](https://learn.microsoft.com/en-us/training/modules/row-level-security-power-bi/2-static-method)):
	* go to our workspace in Power BI service. 
	* Find the dataset that we created with the same name as our report
	* Click here:
	  ![[Pasted image 20231017150849.png]]
	* Then add Microsoft Entra ID users and security groups to the security role. 
		* When members are added to this role, the DAX filter that you previously defined will be applied to them.
	* To test the roles in Power BI service, click on (...) icon next to the role that you want to test, then select "Test as role".

### Set up Role Mappings

* Role mappings must be set up in advance of users accessing Power BI content. 
* Role mapping involves assigning Azure Active Directory (Azure AD) security objects to roles. 
	* Security objects can be user accounts or security groups.
	* Note: it’s a good practice to map roles to security groups. That way, there will be fewer mappings, and you can delegate the group membership management to the network administrators.
* Use Power BI service for role mapping if the models were developed in Power BI Desktop.
* Use SSMS for role mapping if the models were developed in Azure Analysis Services or SQL Server Analysis Services.
* More information can be found here: [Row-level security (RLS) guidance in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/guidance/rls-guidance)

### Use Single Sign-On (SSO) for DirectQuery Sources

<mark style="background: #FF5582A6;">Important note</mark>: ***Calculated tables and calculated columns*** that reference a DirectQuery table from a data source with SSO authentication ***aren’t supported in the Power BI service***.

When your data model has DirectQuery tables and their data source supports SSO, the data source can enforce data permissions.

Example scenario:
Consider that Adventure Works has an Azure SQL Database for their sales operations that resides in the same tenant as Power BI. The database enforces RLS to control access to rows in various database tables. You can create a DirectQuery model that connects to this database without roles and publish it to the Power BI service. ***When you set the data source credentials in the Power BI service, you [enable SSO](https://learn.microsoft.com/en-us/power-bi/connect-data/service-azure-sql-database-with-direct-connect).*** When report consumers open Power BI reports, Power BI passes their identity to the data source. The data source then enforces RLS based on the identity of the report consumer. To enable this option:
![[Pasted image 20231007171725.png]]
For information about Azure SQL Database RLS, see [Row-level security](https://learn.microsoft.com/en-us/sql/relational-databases/security/row-level-security).
For more information about data sources that support SSO, see [Single sign-on (SSO) for DirectQuery sources](https://learn.microsoft.com/en-us/power-bi/connect-data/power-bi-data-sources).

## Object-Level Security (OLS)

[M source](https://learn.microsoft.com/en-us/training/modules/enforce-power-bi-model-security/3-restrict-access-to-power-bi-model-objects)

* <mark style="background: #FF5582A6;">OLS is available in Power BI Premium, and is not available in Power BI Desktop</mark> (read more about this [here](<https://learn.microsoft.com/en-us/training/modules/enforce-power-bi-model-security/3-restrict-access-to-power-bi-model-objects#:~:text=OLS%20is%20a%20feature%20inherited%20from%20Azure%20Analysis%20Services%20(AAS)%20and%20SQL%20Server%20Analysis%20Services%20(SSAS).%20The%20feature%20is%20available%20in%20Power%20BI%20Premium%20to%20provide%20backward%20compatibility%20for%20models%20migrated%20to%20Power%20BI.%20For%20this%20reason%2C%20it%E2%80%99s%20not%20possible%20to%20completely%20set%20up%20OLS%20in%20Power%20BI%20Desktop.>))
* Object-level security (OLS) can restrict access to specific tables and columns, and their metadata.
	* When you secure metadata, it’s not possible to retrieve information about secured tables and columns by using [Dynamic Management Views (DMVs)](https://learn.microsoft.com/en-us/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services).
		* Tabular models can hide tables and columns (and other objects) by using a [perspective](https://learn.microsoft.com/en-us/analysis-services/tabular-models/perspectives-ssas-tabular). A perspective defines viewable subsets of model objects to help provide a specific focus for report authors. However, a user can still query a table or column even when it’s not visible to them.

To set up OLS:
* Create roles like what we did in RLS.
* Next, add OLS rules to the roles.
	* This capability isn’t supported by Power BI Desktop, so we will circumvent this issue by using [XML for Analysis (XMLA) endpoint](https://learn.microsoft.com/en-us/power-bi/enterprise/service-premium-connect-tools).
		* XMLA provides access to the Analysis Services engine in the Power BI service (read more about it [here](https://learn.microsoft.com/en-us/training/modules/enforce-power-bi-model-security/3-restrict-access-to-power-bi-model-objects#:~:text=You%20add%20OLS,and%20managing%20models.)).
* Once you’ve added the OLS rules, you can publish the model to the Power BI service. Use the same process for RLS to map accounts and security groups to the roles.

Notes:
* when a user doesn’t have permission to access a table or column, they get this:
  ![[Pasted image 20231007181745.png]]
* Instead of using OLS, a better approach might be to create a ***separate set of models or reports*** for the different report consumer requirements.
* We can’t mix RLS and OLS in the same role.
	* If we need to apply RLS and OLS in the same model, we'll need to create separate roles dedicated to each type.
* We can’t set table-level security if it breaks a relationship chain:
  ![[Pasted image 20231007181924.png]]
	* However, model relationships that reference a secured column will work, providing that the column’s table isn’t secured.
* While it isn’t possible to secure measures, a measure that references secured objects is automatically restricted.

For more information, see [Object-level security](https://learn.microsoft.com/en-us/analysis-services/tabular-models/object-level-security).

## Good Modeling Practices

[M source](https://learn.microsoft.com/en-us/training/modules/enforce-power-bi-model-security/4-apply-good-modeling-practices)

Some of good development practices to apply include:

- Define fewer datasets (data models) with well-designed roles.
- Create fewer roles by using dynamic rules. A data-driven solution is easier to maintain because you don’t need to add new roles.
- When possible, create rules that filter dimension tables instead of fact tables. It will help to deliver faster query performance.
- Validate that the model design, including its relationships and relationship properties, are correctly set up.
- Use the `USERPRINCIPALNAME` function instead of `USERNAME` function. It provides consistency when validating the roles in Power BI Desktop and the Power BI service.
- Rigorously validate RLS and OLS by testing all roles.
- Ensure that the Power BI Desktop data source connection uses the same credentials that will be applied when set up in the Power BI service.


# Report Design

## Report Design Requirements

[M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-requirements/1-introduction)

The three broad report consumer audiences are ([M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-requirements/2-identify)):
- Executive
	- C-levels like CEO, CTO, etc.
	- Charged with making plans and decisions that often involve a medium or long-term focus.
- Analyst
	- Provides guidance to the organization.
	- Determines the effectiveness of business strategies.
	- Improves processes.
- Information worker
	- Uses data to help make decisions or take actions that are operational in that they are done on a daily basis.

Audience needs can be met by one, or possibly a combination, of four report types ([M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-requirements/3-determine)):
- Dashboard
	- interpret the story as quickly as possible.
	- UX is limited by insights that are highly curated toward the audience.
	- focused, self-explanatory, and clearly labeled.
	- Dashboards help answer questions such as "How are we doing?" or "Are we there yet?" (recall [[Data Analytics Notes#Types of Analytics|descriptive analysis]]).
- Analytical
	- High level of UX to discover answers to a broad array of questions.
	- help answer questions such as "Why did that happen?" or "What might happen next?" (recall [[Data Analytics Notes#Types of Analytics|diagnostic analysis]]).
	- More info on how to design this report type is shown in a [[#Report Design Principles|later section]].
- Operational
	- monitor current or real-time data, make decisions, and act on those decisions.
	- include buttons that allow the report consumer to navigate within the report and also beyond the report to perform actions in external systems.
	- minimize the number of analytical features to ensure that focus remains on the operation that it's designed to serve.
- Educational
	- provide clear narrative detail and guidance to help with understanding the data.
Each of these types has a different approach to UI and UX requirements.

![[Pasted image 20231008112343.png|550]]

Recommendation: check out different report designs in the embedded Power BI report [here](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-requirements/6-explore-designs).

Don't forget to design reports with built-in assistance ([M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-user-experience/7-design-built-in-assistance)). In other words, provide a "no training required" experience. Relevant design techniques for this:
* Information page
	* Dedicate an entire report page that includes instructions and definitions.
	* Consider adding a back button to the page. Then, add a button in a consistent location on each page that navigates to the information page. Configure these buttons to use the **Information** or **Help** icon.
* [[Power BI#^fupz9h|Visual header tooltip icon]]
* [[Power BI#^0zoeia|Button with overlay]]

Don't forget to design a mobile report layout ([M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-user-experience/9-reports-mobile)). Check out the illustration below:
![[Pasted image 20231014115252.png]]
Note that to publish a mobile-optimized version of your report, we can publish the main report as you did previously; the web and mobile versions are published at the same time.
## Report Structure

[M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-reports/1-introduction)

A Power BI report:
*  Connects to a single dataset (data model)
* has at least one report page.
	* On each page, _report objects_ are laid out. Report objects include:
		*  **Visuals** - Visualizations of dataset data.
		*  **Elements -** Provide visual interest but don't use dataset data. Elements include text boxes, buttons, shapes, and images.
![[Pasted image 20231008144830.png]]

### Report Design Principles

[M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-reports/2-design-layout)

* Avoid combining subjects or opposing objectives on the same page.
* consider design principles of:
	* placement
	  ![[Pasted image 20231008145104.png|425]]
	  ![[Pasted image 20231008145113.png|425]]
	* balance
		* Symmetrical: achieved by distributing the weight evenly on both halves of the page.
		* Asymmetrical: achieved through contrast. Example of this is done using the golden ratio:
		  ![[Pasted image 20231008145315.png|425]]
	* contrast
	* proximity
	* repition

Important aspects to be aware of ([M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-reports/3-design-reports)):
* Space: Spacing applies to the report page margins and the spacing between report objects.
	* Margins
	  ![[Pasted image 20231008145553.png]]
	* Object spacing: 
		* Ensure that you provide sufficient space surrounding, or within, report objects.
		* Consider using different space depth to visually separate sections of related objects.
* Size: related to the page size and visual size.
	* Page size:
		* you can set custom dimensions that are larger than the available screen size so that the report consumer will need to interact with scrollbars to view the entire page.
		* However, a large page size that is filled with visuals might take time to render, and visuals might not render in a top-to-bottom order.
	* Visual size: 
		* the more important the visual, the larger its size.
		* Focus mode can help consumers better interpret the data or more easily interact with the visual, such as expanding into levels of a matrix or decomposition tree visual.
* Alignment:
	* <mark style="background: #FF5582A6;">Important tip</mark>: Use the alignment commands on the Format tab, which will help you quickly and accurately align visuals.
	* Consider laying out the report page with different sections and aligning visuals appropriately within the sections. Sections can be _implied_ or _explicit_:
		* Implied sections: Define implied sections by aligning groups of visuals in close proximity:
		  ![[Pasted image 20231008145940.png]]
		* Explicit sections: define explicit sections by using colored shapes and overlaying aligned visuals on those shapes:
		  ![[Pasted image 20231008150013.png]]
* Color: Ensure that colors are sufficiently contrasting. Color contrast is especially important to create accessible reports for report consumers who have low vision.
* Consistency:
	* The quickest way to enforce consistency is to use a report theme. A report theme applies format settings to your entire report, ensuring consistent application of colors, fonts, pages, and visual format options, including the Filters pane styles.
	* Tip: You can use an external site like [powerbi.tips](https://powerbi.tips/) to generate a theme. The site will guide you through building a color palette and setting property values for all core visual types.
	* For more information, see [Use report themes in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-report-themes/).

### Report Objects

Report objects are laid out on each report page and include:
- **Visuals** - Visualizations of dataset data (check the steps to create visuals [here](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-reports/4-report-objects#:~:text=You%20can%20use,a%20report%20visual.)).
- **Elements** - Provide visual interest but don't use dataset data.
	- The text box deserves a special mention because it's capable of embedding _dynamic values_ that are sourced from the report dataset into paragraphs of text. When the page is filtered, dynamic values are filtered. Technically, the text box isn't a visual. However, in this instance, it behaves like one. It's also available as the _smart narrative_ visual, which automatically summarizes data by using text descriptions and insights.
	  ![[Pasted image 20231008171105.png]]
	  At design time, you can start with a text box, or you can add the smart narrative visual from the **Visualizations** pane. However you start, the end result will be the same. Then, you can add a dynamic value by using Q&A to ask a question. Additionally, you can format the values.

### Selecting Report Visuals

[M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-reports/5-report-visuals)

Visual types:
* Categorical visuals
	* bar or column charts are good choices when you need to show data across multiple categories.
* Time Series Visuals
	* Visuals that you can use for time series data include:
		* Stacked column chart
		* Area chart
		* Line and stacked column chart
		* Ribbon chart, which has the added benefit of showing rank changes over time
	* Line charts work well with a consistent flow of data, such as when sales are recorded for every period. If no sales are recorded for some periods, the line chart visual will fill such gaps with a straight line that connects the values of the previous and next periods.
		* If missing values are a possibility, a column chart might be a better visual choice because it will help to avoid the interpretation of a non-existent trend:
		  ![[Pasted image 20231008172013.png]]
* Proportional visuals
	* Proportional visuals show data as part of a whole. They effectively communicate how a value is distributed across a dimension. 
	* Visuals that you can use for proportionality:
		* 100% Stacked Column chart
		* Funnel chart
		* Treemap
		* Pie chart
		* Doughnut chart
	* Proportional visuals can't plot a mix of positive and negative values. They should be used when all values are positive or all values are negative
	* In the following example, a 100% Stacked Bar chart visual shows proportional sales across four stores:
	  ![[Pasted image 20231008190221.png]]
	  Notice that the actual sales value isn't shown. Instead, the proportion of sales is shown.
* Numeric visuals
	* Example:
	  ![[Pasted image 20231008190500.png]]
* Grid visuals
	* tables and matrices can effectively convey a lot of detailed information.
		* Tables have a fixed number of columns, and each column can express grouped or summarized data.
		* Matrices can have groups on columns and rows.
			* matrices provide one of the best experiences for hierarchical navigation. They allow users to drill down, on the columns or rows, to discover detailed data points of interest.
			* In the following example, a table visual shows sales and units sold by product. Showing these metrics together in a single visual can be a challenge because ***the scale of values for sales and units is so different***. But by applying conditional formatting, data bars help report consumers quickly ***understand the distribution of values***:
			  ![[Pasted image 20231008214400.png]]
			  In the next example, a matrix visual displays inventory by product and by store. It uses conditional formatting to show indicators, which provide visual cues to understanding the data:
			  ![[Pasted image 20231008214442.png]]
	* Note 1: Adding conditional formatting options, such as background colors, font colors, or icons, can enhance values with visual indicators.
	* Note 2: Check [this](https://medium.com/@raghu.949/power-bi-table-vs-matrix-9512c2da90ab) article to see difference between tables and matrices.
* Geospatial visuals
	* Tip: Depending on the granularity level, choose either map or filled map (more info [here](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-reports/5-report-visuals#:~:text=In%20the%20following%20example%2C%20sales,by%20interpreting%20the%20color%20graduations.))
* Performance visuals
	* Visuals that can be used to show performance include:
		* Gauge
		* KPI (Key Performance Indicators)
		* Table, with conditional formatting
		* Matrix, with conditional formatting
	* To use a KPI, we need three pieces of information ([M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-reports/8-kpi)):
		* A unit of measurement that we want to track (e.g., total sales).
		* A goal for the measurement as a comparison with current progress.
		* A time series.
	* Now, to select a KPI:
		* Click this visual:
		  ![[Pasted image 20231008215633.png]]
		* Enter fields for said visual like this:
		  ![[Pasted image 20231008215703.png]]
		* Result will look something like this (changes based on value of `Trend axis`):
		  ![[Pasted image 20231008215718.png]]
* AI visuals
	* Mentioned in the [[#Power BI Analytic Capabilities]] section.

### Visual Headers

[M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-user-experience/6-visual-headers)

* All report objects, including visuals and elements (like buttons), have a visual header. 
* The visual header appears when you hover the cursor over the report object, and they can launch actions like focus mode, drill up, or drill down. 
	* You can also access the **More options** menu by selecting the ellipsis (**...**) button. This menu includes sorting options, export, spotlight, and many others.
* Illustration of visual headers:
  ![[Pasted image 20231014113536.png]]
	* Side note: Always leave sufficient space for the visual headers to appear in the upper-right section of objects, like the image above.
* Regarding visual header tooltip icons ([M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-user-experience/7-design-built-in-assistance#:~:text=or%20Help%20icon.-,Visual%20header%20tooltip%20icon,-Within%20the%20visual)) ^fupz9h
	* we can enable the visual header tooltip. This adds the **Help** (**?**) icon to the visual header. Illustration:
	  ![[Pasted image 20231014114158.png]]
* Best practices on when to hide visual headers:
	* when the report consumer isn't familiar with Power BI and you don't intend on teaching them
		* hide all visual headers
	*  when a report object doesn't need it
		* hide visual header for that report object
* For more information, see [Using improved visual headers in Power BI reports](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-visual-elements-for-reports#using-improved-visual-headers-in-power-bi-reports).


## Applying Filters to Reports

[M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-filters/1-introduction)

* Filtering can occur at five different levels of a Microsoft Power BI report:
	- Dataset (RLS)
	- Report
	- Page
	- Visual
	- Measure
		- Implementation note: At report design time in Microsoft Power BI Desktop, **you can create measures except when the model is a live connection to SQL Server Analysis Services multidimensional model**. These measures belong to the report, and so **they're called report-level measures**.
- Report, page, and visual level filters apply to the structure of the report:
  ![[Pasted image 20231011072601.png]]

### Filters Pane

[M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-filters/2-report-structure)

Use the **Filters** pane to apply filters to the report structure:
![[Pasted image 20231011072831.png|202]]

The Filters pane has three **sections**:
- Filters on all pages
	- defines _report-level filters_ (i.e., global filters).
- Filters on this page
	- defines _page-level filters_.
- Filters on this visual
	- defines _visual-level filters_.
	- is the only one that can be defined using measures.
		- When a measure filters a visual, it's used to eliminate groups. 
		- For example, consider a column chart visual that groups by store. A measure filter could eliminate groups (stores) where the total store sales are less than a certain amount.

Filters apply to a single field and use **one of following filter types**:
* Basic
	* select items from a list of distinct values that are found in the field.
- Advanced
	- create more complex conditions by using data type-specific operators:
		- **Text field operators** - Test for conditions such as "contains," "starts with," "is blank," "is empty," and others.
		- **Numeric field operators** - Test for conditions such as "is less than," "is less than or equal to," and others.
		- **Date field operators** - Test for conditions such as "is after," "is on or after," and others.
	- combine multiple tests by using a logical AND/OR operator.
- Top N
	- only in visual-level filters.
	- applies to text and date fields.
	- must pass in a field that's summarized, like sales revenue.
	- example: top five products by revenue.
- Relative date and Relative time
	- allow the report consumer to filter by past, present, or future time periods based on the current date and time.

Filter visibility notes:
* You can lock filters to ensure that report consumers can't remove or modify them.
* You can hide filters. A hidden filter isn't visible to report consumers:
  ![[Pasted image 20231011073529.png]]
* You can hide the entire **Filters** pane to ensure that report consumers can't open it:
  ![[Pasted image 20231011073553.png]]

For more information, see [Format filters in Power BI reports](https://learn.microsoft.com/en-us/power-bi/create-reports/power-bi-report-filter/).

### Slicers

[M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-filters/3-slicers)

The [slicer](https://learn.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-slicers) is a core visual with one purpose: <mark style="background: #FF5582A6;">filter other visuals</mark>.

Regarding the slicer's scope of filtering visuals, that scope can be:
* between chosen visuals of a single page.
* on an an entire page (default).
* synced across multiple pages.
	* For more information, see [Sync slicers across pages in Power BI reports](https://learn.microsoft.com/en-us/power-bi/developer/visuals/enable-sync-slicers).

You can configure a slicer by using one or more fields from the same table or a hierarchy. <mark style="background: #FFB8EBA6;">When configured to use multiple fields or a hierarchy, the slicer presents an expandable tree structure of items.</mark>

The following section mentions different field data types, and possible slicer layouts for each of them:
* Text field
	* List (default)
	* Dropdown
* Numeric field
	* Between (default)
	* Less than or equal to
	* Greater than or equal to
	* List
	* Dropdown
* Date field
	* Between (default)
	* Before
	* After
	* Relative date
	* Relative time
	* List
	* Dropdown

Slicer layout notes:
* List and dropdown
	* support format options to control the selection of items (e.g., **single select**).
* Dropdown
	* use much less space on the report page.
	* <mark style="background: #D2B3FFA6;">only query the dataset when expanded open. Therefore, they can also help expedite report page rendering.</mark>
		* Note: other slicer types can have this advantage as well based on [[Power BI#^e1vpye|how you configure Power BI settings to gain performance boost]].
* Numeric and date ranges (between, after, less than, etc.)
	* support format options to select a single value that acts as the lower or upper boundary of the filter.
	* The reason why numeric and date slicers have additional layouts is because these data types represent continuous values. Therefore, the slicer layouts allow filtering by ranges of continuous values.


Note: To change the slicer style, select Format your visual > Slicer settings > Visual > Options > Style:
![[Pasted image 20231011075824.png]]

Check different slicer layouts by watching the video in [this](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-filters/3-slicers#:~:text=Other%20configuration%20options%20are%20available%20for%20you%20to%20modify%20slicer%20behavior%20and%20its%20look.%20To%20learn%20more%2C%20watch%20the%20following%20video%20that%20demonstrates%20how%20to%20configure%20and%20style%20slicers.) Microsoft source.

### Visual Interactions

[M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-filters/4-advanced-filtering)

* when report consumers interact with visuals, filters are propagated to other visuals on the report page. This way, visuals behave like slicers.
	* For example, a report consumer can select a column of a column chart visual to filter other visuals on the page.
	* To remove the cross filters, they can either select the column again or select a different visual.
	* To add cross filters from same or other visuals, press the **ctrl** key.
* Example of disabling cross filters for a certain visual (from video found [here](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-filters/4-advanced-filtering#:~:text=To%20gain%20a%20better%20understanding%20of%20visual%20interactions%2C%20watch%20the%20following%20video%20that%20describes%20a%20use%20case%20and%20shows%20how%20to%20configure%20it.)):
  ![[Pasted image 20231011092414.png]]
  To find filters currently a visual:
  ![[Pasted image 20231011092518.png]]

For more information, see [Filters and highlighting in Power BI reports](https://learn.microsoft.com/en-us/power-bi/create-reports/power-bi-reports-filters-and-highlighting/).

### Drillthrough

Allow report consumers to drill from visuals to other pages which are called drillthrough pages.

For more information, see [Set up drillthrough in Power BI reports](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-drillthrough/).

Example: right clicking a bar value then choosing the drillthrough page like here:
![[Pasted image 20231011092806.png]]

Steps include:
* create a _target report page_ that has the visuals you want for the type of entity that you're going to provide drillthrough for.
* on that created page, drag the field for which you want to enable drillthrough here:
  ![[Pasted image 20231011093048.png]]
* Now users can right-click a data point on the other source pages in your report, and get a context menu that supports drillthrough to that target page.

Note 1: we can pass all applied filters to the drillthrough target page by going to the destination page then clicking here:
![[Pasted image 20231011104446.png]]
Side note: the filters shown in *italic* above are filters applied from the source page.

Note 2: we can also add a measure or a summarized numeric column to the drillthrough area:
![[Pasted image 20231011104607.png]]
When you add a measure or summarized numeric column, you can drill through to the page when the field is used in the _Value_ area of a visual.

### Tooltips

[M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-reports/7-format)

One of the options for customizing how your selected visualizations look is to use *tooltip* feature of Power BI:

* When you add a visual, the default tooltip displays the data point's value and category, but you can customize this information to suit your needs.
* One way to use tooltips is to display ***graphical information***. To do so, follow the steps [here](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-reports/7-format#:~:text=Another%20way%20to,tooltip%20will%20display.).
	* Note: the final output could look like this (when hovering over the doughnut visual):
	  ![[Pasted image 20231008215346.png]]

For more information, see [Create tooltips based on report pages in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-tooltips/).

By default, the report tooltip receives all filters that apply to the visual ([M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-filters/4-advanced-filtering#:~:text=By%20default%2C%20the%20report%20tooltip%20receives%20all%20filters%20that%20apply%20to%20the%20visual.)).

### Bookmarks

- Bookmarks capture a specific view of a report, including filters, slicers, the page selection, and the state of visuals.
	- Bookmarks that are created by a report consumer are known as _personal bookmarks_.
- You can invoke bookmarks directly from the **Bookmarks** pane, or you can invoke them indirectly by selecting a button, image, or shape.
- Illustration on how to create a bookmark ([M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-user-experience/4-bookmarks#:~:text=watch%20the%20following%20video.)):
  ![[Pasted image 20231014110924.png]]
	- Bookmark State: captures different state, relating to data, display, and the current page
		- The **Data** state captures anything that impacts the queries that Power BI sends to the dataset. (e.g., slicer, sort order, drill depth, etc.)
		- The **Display** state is related to the visibility of a report object.
		- The **Current page** state determines whether the bookmark will direct the report consumer to the bookmarked page or apply the current page.
	- Bookmark Scope: makes a bookmark apply to all page visuals or specific visuals that you select.
		- The **All visuals** scope is turned on by default, meaning that the bookmark applies to all report objects, even if hidden.
		- The **Selected visuals** scope will target only those visuals that are selected when the bookmark was updated.
			- Side note: visuals can be selected by pressing **ctrl** and left clicking the needed visuals, or using the **selection pane**.
- Bookmark examples ([M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-user-experience/4-bookmarks#:~:text=the%20following%20video.-,Bookmark%20examples,-By%20combining%20different)):
	-  Reset slicers. Steps:
		- Capture the **Data** state.
		- **Ctrl** click the slicer visual(s) to select them.
		- Use the **Selected visuals** scope on the selected visuals.
		- Set the slicers to the default values.
		- Update the bookmark.
		- Assign the bookmark to a button action.
	- Swap visuals. Steps for the two required bookmarks:
		- Capture the **Display** state but not the **Data** state.
		- **Ctrl** click the initially visible visual and the hidden visual to select them.
		- Use the **Selected visuals** scope on the selected visuals.
		- Update the first bookmark, with one visual as visible and the other as hidden.
		- Update the second bookmark by using the inverse visibility state.
		- Assign the bookmarks to button actions.
		- Side note: No performance is impacted by having hidden visuals on a page. Hidden visuals don't run queries.
	- Drill down multiple visuals and direct depth navigation. Steps shown [here](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-user-experience/4-bookmarks#:~:text=Configure%20each%20bookmark%20to%20capture%20the%20Data,Assign%20the%20bookmarks%20to%20button%20actions.).
	- Pop-up overlays. Illustration:
	  ![[Pasted image 20231014112341.png]]
	  Steps for the two required bookmarks: ^0zoeia
		- Configure the first bookmark to capture the **Display** state.
		- Ensure that the overlay object is visible, and then update the bookmark.
		- Assign the bookmark to a **Help** button action.
		- Configure the second bookmark to capture the **Display** state.
		- Ensure that the overlay object is hidden, and then update the bookmark.
		- Assign the bookmark to the overlay object.
- For more information on bookmarks, see [Bookmarks in Power BI service](https://learn.microsoft.com/en-us/power-bi/consumer/end-user-bookmarks/).
### Report Options

With report options, you can:
- Disable persistent filters. (covered in a later section).
- Hide visual headers for all visuals or for a specific visual.
	- This will prevent report consumers from determining the filters that are applied to a visual by using the filter icon (covered in a later section).
- Hide the **Filter** icon for a specific visual.
- Restrict report consumers from changing filter types (for example, basic to advanced) in the **Filters** pane.
- Remove the search box in the **Filters** pane.

#### Query Reduction Options

Reduce the number of queries that are sent to the dataset by doing one of the following:
* Disable cross highlighting/filtering by default.
* Add an **Apply** button to (mentioned in [[#General Tips|general performance tips section]]):
	* Slicers.
	* All basic filters in the filters pane.
	* The filters pane.

### Consumption-Time Filtering

[M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-filters/5-consumption-time)

In reading view, report consumers can use many different filter techniques when viewing a Power BI report, such as:
- Using slicers.
- [[#Consumer Uses Filters|Using filters]].
- [[#Interactive Filtering Actions|Applying interactive filtering actions]].
- Determining applied filters.
- Working with persistent filters.

As a report author, use these filter techniques to design reports that take advantage of these capabilities, and at times, disable them (when you have good reason to do so).

#### Consumer Uses Filters

- consumer capabilities:
	- Select the eraser icon to **clear** the filter
		- but they **can't remove** that filter.
	- Apply a new ***filter selection***
		- but they can't add a new **filter**.
			- However, a filter can be added/removed using [query string parameters in the URL](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-url-filters)
		- also can't enforce or disable single selection
	- Change the filter type, such as from basic to advanced (unless disabled for the report)
		- but they can't change it to **Top N**, or **relative date or time** 
	- Use the search box to search for values to filter by (unless disabled for the report).

#### Interactive Filtering Actions

Many report consumer interactions apply filters. These interactions can:
- Slice to propagate filters to other visuals.
- Include/exclude filters.
	- These filters appear in the Filters pane as filter cards titled **Included** or **Excluded**. The report consumer can use the **Filters** pane to view, modify, or remove them.
- Cross filter.
	- Note ([M source](https://learn.microsoft.com/en-us/power-bi/consumer/end-user-interactions#cross-filter-and-cross-highlight)): **Cross-filtering** removes data that doesn't apply. **Cross-highlighting** retains all the original data points but dims the portion that doesn't apply to your selection.
- Drill through to a report page.
- Apply bookmarks.

#### Determine Applied Filters

Occasionally, report consumers want to know (or verify) what filters apply to a specific visual. To do so: Hover the cursor over the Filter icon in the visual header, a pop-up window will then appear, describing the filters that affect the visual:
![[Pasted image 20231011125447.png]]

Note 1: Hidden filters aren't visible in the pop-up window.

Note 2: If the **Filter** icon isn't available for a visual, it could be because one of the reasons mentioned in the [[#Report Options|report options section]].

For more information, see [Take a tour of the report Filters pane](https://learn.microsoft.com/en-us/power-bi/consumer/end-user-report-filter#view-only-those-filters-applied-to-a-visual).

#### Persistent Filters

_Persistent filters_ is a feature that saves report consumer's slicer and filter settings. It automatically applies the settings when the report consumer reopens the report. It can be reset from here:
![[Pasted image 20231011135812.png]]

### Design Choices: Filters vs Slicers vs Visual Interactions

[M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-filters/6-filter-techniques)

Check the link above for full list of advantages and disadvantages of both. Here, we'll mention brief points:
* Filters allow us to configure advanced filter types, like **Top N**, or allow us to use more complex expressions, like "contains," "does not contain," "is blank," and others.
	* However, we can filter slicers as you would any visual. For example, we can apply a filter to a slicer to remove the BLANK item.
* Filters result in faster report rendering because no visual rendering is required, unlike slicers.
* We can create hierarchical slicers (based on a hierarchy or by using multiple fields that are sourced from the same table).
* Synced slicers can filter other pages in the report.

Alternatively, we can enable filtering by using visuals. However, a downside to this approach is that some report consumers might not be aware that visuals can cross filter other visuals. 
Example: In the following bar chart, the report page is filtered by the product Excel:
![[Pasted image 20231011141228.png]]

Tips when designing a report: 
* Consistency: use either filters or slicers.
* In the **Filters** pane, consider locking or hiding visual-level filters to avoid confusing report consumers. (Often, report consumer shouldn't modify or see visual-level filters.)
* Create a bookmark to reset all slicers to default values. Then, add a button to the page to invoke the bookmark. For example, the button could be captioned as **Reset slicers**.
* When a requirement is in place to lay out many slicers, consider creating a page that is dedicated to showing all slicers. For example, the page could be named **Slicers**. Sync the slicers to other pages and then set the slicers as hidden on those pages.
* Consider using other visuals in place of slicers. Be sure to teach report consumers how to cross filter by using these visuals.

For more information, see [Create buttons in Power BI reports](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-buttons/) and [Create page navigation](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-buttons#create-page-navigation).


# Power BI Analytic Capabilities

[M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/1-introduction)

## Statistical Summaries

[M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/2-statistical-summary)

* To create statistical functions, you have the following options:
	* create **quick statistics** from the Visualizations pane:
	  ![[Pasted image 20231014134042.png]]
	* create statistics using DAX: `Average Qty = AVERAGE(Sales[Order Qty])`
		* Side note: apparently, using DAX is better in terms of performance ([M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/2-statistical-summary#:~:text=However%2C%20to%20avoid%20performance%20issues%2C%20it%27s%20better%20to%20create%20the%20statistical%20measures%20yourself%20by%20using%20DAX%20functions%20to%20calculate%20average%2C%20sum%2C%20min%2C%20max%2C%20and%20so%20on.))
* Using histograms is the most common way to display statistics about your datasets.
	* Histograms are created using the **bar (column) chart** or the **area chart** visuals:
	  ![[Pasted image 20231014134529.png]]
	* A typical bar or column chart visual in Power BI **relates two data points: a measure and a dimension.** A **histogram** differs slightly from a standard bar chart in that it **only visualizes a single data point**.
	* you can use grouping/binning techniques to create a clustered column chart. This is mentioned in a later section called [[#Group and Bin Data]].
* Performing Top N analysis is a great way to present data that might be important, such as the top 10 selling products. This can be done in 3 ways:
	* Q&A Visual
	  ![[Pasted image 20231014134808.png]]
	  ![[Pasted image 20231014134811.png]]
	  Side note: Q&A is explained later in the [[#Q&A|Q&A section]]. ^uhio1l
	* Top N filter type
	  ![[Pasted image 20231014134858.png]]
	* TOPN DAX function
		* Example of this is mentioned in the [[#Iterator Functions|Iterator Functions section]]

For more information about the statistical capabilities of Power BI, see [Statistical Functions - DAX](https://learn.microsoft.com/en-us/dax/statistical-functions-dax/).

## Outliers Detection

[M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/3-visuals)

* The best visual to use for identifying outliers is the scatter chart;
	* It shows the relationship between two numerical values. 
	* It displays patterns in large sets of data and is, therefore, ideal for displaying outliers.
	* Basic way of identifying outliers:
		* choose scatter chart from visualizations pane
		* add fields of interests:
		  ![[Pasted image 20231014135443.png]]
		* Identify the outliers by yourself:
		  ![[Pasted image 20231014135503.png]]
	* Advanced way of identifying outliers (on a different example than the one above) ([source](https://www.youtube.com/watch?v=kc3ztxkj0Tc)):
		* Suppose you want to see the outliers here:
		  ![[Pasted image 20231014140104.png]]
		  and suppose the business logic dictates that outliers are considered to be customers with `Profit Margins` above 35% **and** with `Total Sales` above 55,000. ^kmz928
		* Therefore, if we want to manually see where the outliers are, we'll have to look at the x and y axes to see them:
		  ![[Pasted image 20231014140513.png]]
		* But what if we want to automate this process by separating the y axis (i.e., `Total Sales`) into two groups (i.e., outliers, and non outliers)? Illustration:
		  ![[Pasted image 20231014140700.png]]
		* Solution: follow these steps: 
			* Create a *detached table* called `Outlier Detection Logic` (at minute 3:50, 5:00):
			  ![[Pasted image 20231014135610.png]]
			  ![[Pasted image 20231014135709.png]]
		* create DAX measure called `Outlier Sales` that will follow the business logic discussed [[Power BI#^kmz928|above]] in order to sum the `Total Sales` of the outlier customers only (explained at [6:00](https://youtu.be/kc3ztxkj0Tc?t=362)):
		  ![[Pasted image 20231014141124.png]]
		* create complimentary logic for `Non Outlier Sales` measure:
		  ![[Pasted image 20231014142039.png]]
		* As you can see, these are two DAX formulas. However, we need to use only one DAX formula called `Sales Grouping` to display in the y-axis of the scatter chart. To do so, we use this DAX formula (explained at [8:25](https://youtu.be/kc3ztxkj0Tc?t=503)):
		  ![[Pasted image 20231014143127.png]]
		* Finally, we add the created measures as fields to the scatter chart:
		  ![[Pasted image 20231014144229.png]]
		  Note that `Customer Name` and `Grouping` are from `Customers` and `Outlier Detection Logic` tables respectively, while `Profit Margins` (not explicitly explained in [the video](https://www.youtube.com/watch?v=kc3ztxkj0Tc)) and `Sales Grouping` are measures created and stored in its own logical folder:
		  ![[Pasted image 20231014144750.png]]

## Group and Bin Data

[M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/4-group-data)

Grouping vs binning ([M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/4-group-data#:~:text=Grouping%20is%20used%20for%20categories%20of%20data.%20Binning%20is%20similar%20to%20grouping%2C%20but%20it%20is%20used%20for%20grouping%20continuous%20fields%2C%20such%20as%20numbers%20and%20dates.)):
* Grouping is for discrete values
* Binning is for continuous values


General steps to create groups/bins ([source](https://www.youtube.com/watch?v=D1LO8syugMA)):
* Prepare your visual. For example:
  ![[Pasted image 20231014145625.png]]
* Add the <mark style="background: #FF5582A6;">group field</mark> to the `Axis` well like so:
  ![[Pasted image 20231014145456.png]]
* You'll now see the visual properly grouped/binned on the chosen axis like so:
  ![[Pasted image 20231014145542.png]]

Now, regarding the ***group field***, it can be created as a:
* Measure (using DAX)
	* Create measure using this DAX expression (at minute 1:07)
	  ![[Pasted image 20231014150002.png]]
* Group (using Power BI's UI) (at 2:02)
	* click on any of these two options:
	  ![[Pasted image 20231014150205.png]]
	* now, in the new window that opens, you have 2 group types to choose from:
		* List (at 2:21):
		  ![[Pasted image 20231014150331.png]]
		*  Bins (screenshot is from another [video](https://youtu.be/BRvdZSfO0DY?t=257)):
		  ![[Pasted image 20231014150805.png]]
* Column (using Power Query) (at [3:12](https://youtu.be/D1LO8syugMA?t=192))
	* Open Power Query
		* This can be done in multiple ways, when of them is to right click the table of interest and clicking "Edit Query"
	* Highlight the column that you want to bin, then click "Column from examples":
	  ![[Pasted image 20231014151033.png]]
	* At the first row, type a bin size like "20-40":
	  ![[Pasted image 20231014151111.png]]
	* Result:
	  ![[Pasted image 20231014151129.png]]


## Clustering

[M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/5-clustering-techniques)

Clustering allows you to identify a segment (cluster) of data that is similar to each other but dissimilar to the rest of the data. The process of clustering is different to that of grouping, which you accomplished previously.

[This video](https://www.youtube.com/watch?v=NjdZjozKboA) summarizes how to use clustering feature of Power BI, so check it out for details. However, one important thing to note (at minute [1:10](https://youtu.be/NjdZjozKboA?t=70)) is that the fields of the visual (e.g., scatter chart) have to adhere through a certain setup as shown in the image below:
![[Pasted image 20231014152650.png]]

## Time Series Analysis

[M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/6-time-series-analysis)

* Time series analysis involves:
	* analyzing a series of data in time order to identify meaningful information and trends and make predictions. 
	* the use of visuals such as line chart, area chart, or scatter chart.
		* These let us view how your data is progressing over time, which can be helpful in making observations like major events disrupting our data.
* The result of time series analysis is the best data that you can use for forecasting activities.
* We can also import a time series custom visual into Power BI Desktop from Microsoft AppSource. Example ([M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/6-time-series-analysis#:~:text=When%20you%20have%20set%20up%20the%20Play%20Axis%20visual%20to%20meet%20your%20requirements%2C%20you%20are%20ready%20to%20use%20it%20with%20your%20other%20visuals.%20Select%20the%20Play%20button%20and%20then%20watch%20how%20the%20data%20in%20each%20visual%20on%20the%20page%20evolves%20over%20the%20time.%20You%20can%20use%20the%20control%20buttons%20to%20pause%20the%20animation%2C%20restart%20it%2C%20and%20so%20on.)):
	  ![[line chart auto play.gif]]
	* Steps for using **Play Axis (Dynamic Slicer)** visual can be found [here](https://www.youtube.com/watch?v=8G8y5H-MMnQ) or [here](https://www.youtube.com/watch?v=0K-6rKN_xnY).

## Analyze Feature

[M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/7-analyze-feature)

* The **Analyze** feature provides additional analysis that is generated by Power BI for a selected data point. 
* Determines if Power BI has found something that we haven't seen before, or if we want Power BI to give you a different insight into your data. 
* This feature is particularly useful for <mark style="background: #FFB8EBA6;">explaining the increase and analyzing why the data distribution looks the way that it does</mark>.
* Example:
  ![[Pasted image 20231014161057.png]]
  ![[Pasted image 20231014161105.png]]
  If you find this analysis useful, you can add the new visual to your report so that other users can view it. Select the plus (**+**) icon in the upper-right corner of the visual to add it to your report.
* For more information about the Analyze feature, see [Apply insights in Power BI Desktop to discover where distributions vary (preview)](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-insights-find-where-different/).


## Specialized AI Visuals

[M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/9-use-specialized-visuals)

Tip: When adding an AI visual to your report, make sure that you size it to become as large as possible. That way, report consumers can fully interact with and explore the data in the visual.

### Key Influencers

* The **Key influencers** visual helps report consumers understand the factors that drive a particular metric, like sales revenue. 
* By using AI, Power BI will analyze the data, rank the factors that matter, and then present them as key influencers.
* Example ([M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/9-use-specialized-visuals#:~:text=The%20capabilities%20of%20the%20Key%20influencers%20visual%20are%20best%20described%20by%20following%20an%20example.%20For%20a%20demonstration%20of%20the%20Key%20influencers%20visual%2C%20watch%20the%20following%20video.)): 
  ![[Pasted image 20231014172359.png]]
* Essentially, the **Key influencers** visual is many visuals inside one frame. When you select a key influencer, an adjacent visual will show a representation of the influencer as a comparison against the remainder of the data. 
	* Additionally, the **Key influencers** visual includes the **Top segments** view, which shows the highest-ranking segments that contribute to a particular metric.
* For more information, see [Create key influencers visualizations](https://learn.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-influencers).

### Decomposition Tree

* The **Decomposition Tree** visual helps report consumers visualize data across multiple dimensions. 
* It automatically aggregates data and enables consumers to drill down into dimensions in any order. 
	* As a result, it's a valuable tool for ad hoc exploration and conducting root cause analysis. 
* As an AI visual, a decomposition tree provides a guided exploration experience that helps by finding the next dimension for consumers to drill down into.
* Example ([M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/9-use-specialized-visuals#:~:text=The%20capabilities%20of%20the%20Decomposition%20Tree%20visual%20are%20best%20described%20by%20following%20an%20example.%20For%20a%20demonstration%20of%20the%20Decomposition%20Tree%20visual%2C%20watch%20the%20following%20video.)):
  ![[Pasted image 20231014172809.png]]
* For more information, see [Create and view decomposition tree visuals in Power BI](https://learn.microsoft.com/en-us/power-bi/visuals/power-bi-visualization-decomposition-tree).

### Q&A

Side note: Q&A can be used in top N analysis as mentioned in the [[Power BI#^uhio1l|Statistical Summaries section]]

* To optimize the Q&A experience:
	* ensure that the data field names are user-friendly. 
	* enhance the data model with synonyms and terms. 
	* hide fields, such as fields that are used in model relationships, to restrict their use in Q&A. 
	* add suggested questions that become prompts in the **Q&A** visual. 
	* These optimizations can be done by clicking at the cog icon of the Q&A visual ([M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/9-use-specialized-visuals#:~:text=For%20a%20demonstration%20of%20the%20Q%26A%20visual%2C%20watch%20the%20following%20video.)):
	  ![[Pasted image 20231014173326.png]]
* For more information, see [Use Power BI Q&A to explore your data and create visuals](https://learn.microsoft.com/en-us/power-bi/create-reports/power-bi-tutorial-q-and-a).

Note: The Q&A visual consists of three main elements ([M source](https://learn.microsoft.com/en-us/training/modules/create-dashboards-power-bi/3-explore-data#:~:text=The%20Q%26A%20visual%20consists%20of%20three%20main%20elements%3A)):
* Question box
* Pre-populated suggestion tiles
* Pin visual icon
	* appears in Power BI service in order to pin the visual to a [[#Dashboards|dashboard]].
# Paginated Reports

[M source](https://learn.microsoft.com/en-us/training/modules/create-paginated-reports-power-bi/1-introduction)

Paginated reports are:
* used for operational reports with tables of details and optional headers and footers.
* used when we want to print the report on paper or when we want an e-receipt, a purchase order, or an invoice.
* used to render tabular data exceedingly well.
	* Therefore, ideal for creating sales invoices, receipts, purchase orders, and tabular data.
* descendants of SQL Server Reporting Services (SSRS), which was first introduced in 2004. 
	* Power BI paginated reports and SSRS have a lot in common. 
	* <mark style="background: #BBFABBA6;">If you're looking for information on paginated reports and can't find it, search the internet and Microsoft documentation on SSRS.</mark>
* shared with either a Power BI Pro or a Power BI premium license.
	* To publish your report, select **File >** **Save as** and then select **Power BI Service**. Your report will now appear in Power BI service ([M source](https://learn.microsoft.com/en-us/training/modules/create-paginated-reports-power-bi/5-publish)). For more information, go to [Publish datasets and reports from Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-upload-desktop-files/).
* not created in Power BI Desktop; they are built by using [Power BI Report Builder](https://www.microsoft.com/en-us/download/details.aspx?id=58158).

Illustrative example:
  ![[Pasted image 20231014174719.png]]

Best practices ([M source](https://learn.microsoft.com/en-us/training/modules/create-paginated-reports-power-bi/5-publish)):
* provide guidance to the user by documenting why this report was created.
	* Adding a report implementation date and time is an excellent practice.
	* People who are looking at a report won't know that they're looking at an older version unless that fact is highlighted in a footer.
* Put important information, like totals, at the top of the report.
* The way people read dates varies across different countries/regions. Localize data formats to the appropriate target user.
* test the appropriate delivery format and ensure that the report is rendering correctly in that format. Does the user want the report:
	* sent to them in an email message?
	* in a printable format?
	* in a web browser?
* Pay attention to the height and width of the report page. Verify that the report isn't running off the page when the report renders for the user.
* Create reports that are easy on the data source. Neglecting this overburden the data source and affect performance.

### Getting Data to Paginated Reports

[M source](https://learn.microsoft.com/en-us/training/modules/create-paginated-reports-power-bi/2-get-data)

Paginated reports:
* do not use Power Query when connecting to data sources.
* do not involve data cleaning steps.
* do not store a Power BI paginated report dataset.
	* When data is refreshed on the report, it is retrieved in an unaltered form from the data source, according to the query that was used to retrieve it.
* can be collected from multiple data sources, including Microsoft Excel, Oracle, SQL Server, and many more.
	* However, after the data has been collected, the different data sources cannot be merged into a single data model.
	* Each source must be used for a different purpose. 
		* For instance, data from an Excel source can be used for a chart, while data from SQL Server can be used for a table on a single report.
* have an expression language that can be used to look up data in different datasets, but it is nothing like Power Query.
* can use a dataset from Power BI service. 
	* These datasets have used Power Query to clean and alter the data. 
	* The difference is that this work was done in Power BI Desktop or SQL Server Data Tools prior to using Power BI Report Builder.

#### Create and Configure a Data Source

To create and configure a **data source**:
* From **Getting Started** screen -> "New Report" -> "blank report"
* Then:
  ![[Pasted image 20231014175857.png]]
* Then:
  ![[Pasted image 20231014175930.png]]
* Regarding (3), the **Connection Properties** screen will appear, so follow these steps:
  ![[Pasted image 20231014180013.png]]

#### Create and Configure a Dataset

<mark style="background: #FFF3A3A6;">data source vs dataset</mark> definitions in paginated reports (and probably in [[#DirectQuery Model]]):
* A data source is the **connection information to a particular resource**, like SQL Server.
* A dataset is the **saved information of the query against the data source**, not the data. 
	* The data always resides in its original location.

Now, to create and configure a **dataset**:
* Right-click **Datasets** in the **Report View** window and select **Add Dataset**.
* Follow these steps:
  ![[Pasted image 20231014180346.png]]

### Creating a Paginated Table/Matrix and Adding Parameters

[M source](https://learn.microsoft.com/en-us/training/modules/create-paginated-reports-power-bi/3-paginated-report)

* Follow the Microsoft source above to see the steps of creating a table
* Follow the video [here](https://youtu.be/hEGDJ6SxJEk?t=461) (starting from 7:40) to see the steps of creating a matrix:
  ![[Pasted image 20231014211345.png]]

To create a parameter:
* Follow the steps [here](https://learn.microsoft.com/en-us/training/modules/create-paginated-reports-power-bi/3-paginated-report#:~:text=add%20a%20parameter.-,Add%20parameters,-To%20add%20a).
* Or follow the steps in the same video referenced above starting from [10:00](https://youtu.be/hEGDJ6SxJEk?t=604):
  ![[Pasted image 20231014211141.png]]
  when clicking "Run":
  ![[Pasted image 20231014211221.png]]


### Creating Charts in a Paginated Report

[M source](https://learn.microsoft.com/en-us/training/modules/create-paginated-reports-power-bi/4-charts)

* First method of adding charts:
  ![[Pasted image 20231014211618.png]]
* Second method of adding charts:
  ![[Pasted image 20231014211625.png]]

Next, choose the type and style of your chart, then, it the chart will be added to the design surface.

When you select the chart, a new window appears to the right. The **Chart Data** screen allows you to format the chart according to the values and axis properties.

Select the plus (**+**) sign beside each section to select the required columns:
![[Pasted image 20231014211720.png]]

For more information on working with charts, you can search Microsoft documentation regarding SSRS reports. All of the material in the SSRS documentation will apply to Power BI paginated reports.

# Managing Workspaces

[M source](https://learn.microsoft.com/en-us/training/modules/create-manage-workspaces-power-bi/1-introduction)

Workspaces offer the following benefits:
- Focused collaboration efforts. 
	- You can use workspaces to house reports and dashboards for use by multiple teams.
- Ability to share and present reports and dashboards in a single environment.
- Assurance that the highest level of security is maintained by controlling who can access datasets, reports, and dashboards.

## Creating a Workspace and Workspace Roles

[M source](https://learn.microsoft.com/en-us/training/modules/create-manage-workspaces-power-bi/2-distribute-report-dashboard)

Most of the details are in the Microsoft source above. Therefore, we'll mention a few notes here.

When creating a workspace:
* A **contact list** refers to users who will receive notifications if issues with the workspace occur.
	* By default, these users are the workspace admins, but we can also add specific users.
* We can add optionally add the workspace to a specific OneDrive and then choose whether this workspace will be a part of a dedicated capacity or not.
	* Dedicated capacities are Power BI Premium features that ensure that your workspace will have its own computational resources as opposed to sharing resources with other users.

Regarding workspace roles:
* **Admin**
    - Workspaces: Update and delete them ^68di4d
    - People: Add or remove them, including other admins
    - Change [[Power BI#^u7k3wc|data classifications]] that could be applied to a dashboard.
- **Member**
    - People: Add members or others with lower permissions
    - <mark style="background: #D2B3FFA6;">Apps: Publish, unpublish, and change permissions</mark>
- **Contributor**
    - Workspace content: Create, edit, and delete
        - E.g., reports, dashboards, datasets
    - <mark style="background: #D2B3FFA6;">Reports: Publish them to the workspace</mark>
    - See **[[#Usage Metric Reports|usage metric reports]]**
    - See **lineage view**
- **Viewer**
    - View and interact with an item
    - Read data that's stored in workspace dataflows
- Note:  full permissions, review the [Roles in workspaces documentation](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-roles-new-workspaces#workspace-roles). It is mentioned here also:
  ![[Pasted image 20231015072419.png]]

To assign these roles to users, go to the workspace that you've created and, in the upper-left corner of the ribbon, select **Access**:
![[Pasted image 20231015072458.png]]

Notes regarding [building your app section in the Microsoft source](https://learn.microsoft.com/en-us/training/modules/create-manage-workspaces-power-bi/2-distribute-report-dashboard#:~:text=Create%20and%20configure%20an%20app): 
* We need a Power BI Pro license to publish an App.
* Use the **Contact Information** and **Support Site** fields to help users contact the appropriate person(s) and how to find help for the app.
* Regarding the **Manage Audience Access** section:
	* We can **Grant access to** the _Entire organization_ or _Specific users or groups_. 
		* For Specific users or groups, we can enter any mail-enabled account accessible within our Power BI tenant.
	* We can allow people to share the datasets in the app audience.
	* We can allow people to build content with the datasets in the app audience
	* Lastly, notice that **Workspace users** are already included in the audience by default. This goes back to the roles we covered earlier.


## Usage Metric Reports

[M source](https://learn.microsoft.com/en-us/training/modules/create-manage-workspaces-power-bi/3-monitor-usage-performance)

In the **Report usage** tab, you can view such details as:
* **Viewers per day**, **Unique viewers per day** (which doesn't include users who returned to the same reports multiple times), and **Shares per day** charts
- **Total Views**, **Total Viewers**, and **Total Shares** KPI cards
- **Total views and shares ranking** 
	- (compares how your report is doing in comparison to other reports in the app)
- **Views by Users** 
	- (details about each specific user that viewed the dashboard)

We can also filter by the distribution method of the report (for example, through sharing or from the workspace directly) and platform type (for example, mobile or web).

We can also view performance metrics on the **Report performance** tab, as shown in the following screenshot:
![[Pasted image 20231015080346.png]]

On the **Report performance** tab, we can view metrics such as:
- **Typical opening time**
	- How long it takes, at the fiftieth percentile, to open the report.
- **Opening time trend**
	- How the typical opening time changes over time. This metric can tell you how the report is performing as the number of users starts to grow.
- **Daily/7-Day Performance** charts
	- Highlight the performance for 10, 50, and 90 percent of the open-report actions every day and over a seven-day period.
- Filters for date
	- so you can see how the performance changes according to the day.

For more information, see [Monitor Usage Metrics](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-modern-usage-metrics/).

## Development Life Cycle Strategy

[M source](https://learn.microsoft.com/en-us/training/modules/create-manage-workspaces-power-bi/4-development-lifecycle-strategy)

The **deployment pipeline feature**:
* manages content (dashboards, etc.) between different environments in the development life cycle.
* lets us develop and test Power BI content in one centralized location and streamline the process before deploying the final content to users.
* requires that we're a Power BI premium user, and that we're a capacity admin.
* has the following advantages:
	* Increased productivity
		* reuse previous deployment pipelines, ensuring that efforts aren't duplicated.
	* Faster delivery of content
		* Report development becomes more streamlined
	* Lower human intervention required
		* decreased human error when moving content from one environment to another.
* consists of 3 stages/environments:
	* Development
		* The location in which dashboard developers or data modelers can build new content with other developers.
	* Test
		* Where a small group of users and user acceptance testers can see and review new reports, provide feedback, and test the reports with larger datasets for bugs and data inconsistencies before it goes into production.
	* Production
		* Where an expansive user audience can use tested reports that are reliable and accurate.
	* Side note: if business needs dictate so, the development stage can be omitted.

Steps to create a deployment pipeline:
* click here:
  ![[Pasted image 20231015140500.png]]
* After creating the pipeline, you'll see this page:
  ![[Pasted image 20231015140528.png]]
* assign workspaces to each of these stages using the "Assign a workspace" button. Notes:
	* Only workspaces that are assigned to a Premium capacity will appear. 
	* we can only assign a single workspace to each pipeline. Power BI will auto generate the two other workspaces that are used in the pipeline.
* At every stage, you have the option to publish the associated workspace as an app by selecting **Publish app**.

Testing phase:
* After finishing the development workspace, Select **Deploy to test**, which will create a new workspace. 
	* This workspace, by default, has the same name as the initial workspace but includes the **Test** suffix.
	* Testing should emulate conditions that objects will experience after they've been deployed for users. 
		* Therefore, Power BI allows you to change the source of data that is used during testing by clicking here:
		  ![[Pasted image 20231015140908.png]]
		  In this example, <mark style="background: #FFB8EBA6;">we want our dataset to be used for testing but with a different data source. To do so we have the following 2 options</mark>:
			* Create parameters in Power Query Parameters (mentioned in a later section)
			* Add a new rule:
			  ![[Pasted image 20231015141111.png]]
			  Then:
			  ![[Pasted image 20231015141133.png]]
			* Note: we do the steps above again, but this time to transition from the **Test** phase to the **Production** phase.

Notes about additional operations in development phase (logically similar to "git pull"):
* Suppose we receive a notification that one of the other developers has modified a report. To see the changes to this report:
  ![[Pasted image 20231015141555.png]]
  Result:
  ![[Pasted image 20231015141612.png]]
* The difference is typically registered as added or removed objects. If we decide that the changes shouldn't be deployed to the next phase, we can choose to ignore the changes. by selecting a specific report and then selecting **Deploy to test**.
	* Exercise caution with this tool. Reports are dependent on their datasets. If a dataset has changed, but you don't deploy it with an associated report, the report will not behave correctly.

For more information, see [Deployment Pipelines Best Practices](https://learn.microsoft.com/en-us/power-bi/create-reports/deployment-pipelines-best-practices/).

## Data Lineage View

[M source](https://learn.microsoft.com/en-us/training/modules/create-manage-workspaces-power-bi/5-troubleshoot-data)

Data lineage view:
* requires a Power BI Pro license and is only available for app workspaces.
* accessible to **Admin**, **Contributor**, and **Member** roles only.
* Refers to the path that data takes from the data source to the destination.
	* Example:
	  ![[Pasted image 20231015143231.png]] ^zfkx72
	* Typically, the flow would be **data sources > datasets/dataflows > reports > dashboards**.
* Simplifies the troubleshooting process
	* By seeing how data flows from source to destination and determining pain points and bottlenecks.
* Allows us to observe the impact of a single change in one dataset to reports and dashboards.
* Easily identifies reports/dashboards that haven't been refreshed.


To use lineage view:
* Go to a workspace, then:
  ![[Pasted image 20231015143628.png]]
  This will show the graph that is shown [[Power BI#^zfkx72|above]].

Now, regarding each card in the lineage view:
* Data source card
	* Example:
	  ![[Pasted image 20231015143854.png]]
	* The card tells us the type and the gateway of the data source.
		* If you are connected to the data through an on-premises data gateway, this card will tell you more information about the gateway. 
			* Additionally, if you double-click the card, you will get more details about the data source, such as the file path and the connection status.
	* Selecting the lower-right icon on the card will highlight the path from the data source to the destination:
	  ![[Pasted image 20231015144005.png]]


Dataset/Dataflow cards:
* Example:
  ![[Pasted image 20231015144348.png]]
* The impact analysis window displays how many workspaces, reports, and dashboards that this dataset is a part of and how many views that this dataset has gathered. We can select **Notify contacts**, which allows you to notify dataset owners (or any other user) of changes in the dataset:
  ![[Pasted image 20231015144514.png]]
* When double clicking this card, we see the following metadata:
  ![[Pasted image 20231015144251.png]]
	* <mark style="background: #FFB8EBA6;">Impact analysis is useful because it allows you to pinpoint datasets that aren't being used or looked at.</mark>

Reports and Dashboards cards:
* When double clicking:
  ![[Pasted image 20231015144649.png]]
* when clicking on the ellipsis (...) icon:
  ![[Pasted image 20231015144706.png]]

For more information, see [Data Lineage](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-data-lineage/).

## Data Protection Using Sensitivity (Security) Labels

[M source](https://learn.microsoft.com/en-us/training/modules/create-manage-workspaces-power-bi/6-data-protection)

To ensure that sensitive data is secure, do one of the following:
* Use Microsoft sensitivity labels on assets (dashboards, reports, datasets, and dataflows).
	* Labels are configured externally to Power BI
* Add encryption and watermarks when exporting the data.
* Use Microsoft Cloud App Security to monitor and investigate activities in Power BI.

Before we begin, we should ensure that we have the appropriate licensing, as shown [here](https://learn.microsoft.com/en-us/power-bi/admin/service-security-data-protection-overview/).

Regarding sensitivity labels:
* Specifies which data can be exported.
* Protects content even outside of Power BI
* To enable it:
  ![[Pasted image 20231016213638.png]]
  then:
  ![[Pasted image 20231016213647.png]]
* Possible labels:
	* None
	* Personal
	* General
	* Confidential
	* Highly confidential
	* User defined labels from [Microsoft 365 Security Center](https://security.microsoft.com/homepage/)
* When exporting a labeled dataset:
	* it could appear like this if we're an authorized user:
	  ![[Pasted image 20231016213819.png]]
	* Otherwise, we would be denied access to see the data.
* For more information, see [Apply Data Sensitivity Labels in Power BI](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-security-apply-data-sensitivity-labels).


# Managing Datasets

[M source](https://learn.microsoft.com/en-us/training/modules/manage-datasets-power-bi/1-introduction)

Managing datasets is important when we want to:
* make the reports more dynamic so that they can filter the data themselves.
* run what-if scenarios.
* guarantee the coherency and integrity of our datasets.
* make the datasets available in one place.
* automate the refresh process to ensure that the data is kept up to date.

## Power BI Gateways

[M source](https://learn.microsoft.com/en-us/training/modules/manage-datasets-power-bi/4-power-bi-gateway)

Gateway software allows us to:
* retain databases/data-sources on-premise, then access them in cloud services.
* flow from a user in the cloud, to the on-premise data, then back to the cloud:
  ![[Pasted image 20231016214604.png]]
	* Behind the scenes, the following actions occur:
	  ![[Pasted image 20231016215420.png]]
		* <mark style="background: #FFB8EBA6;">The cloud service</mark> :
			* creates a query and the encrypted credentials for the on-premises data source. 
			* sends them to the gateway queue for processing.
		* <mark style="background: #FFB8EBA6;">The gateway cloud service</mark>:
			* analyzes the query.
			* pushes the request to Microsoft Azure Service Bus.
		* The Service Bus:
			* sends the pending requests to the gateway.
		* <mark style="background: #FFB8EBA6;">The on-premises data gateway</mark>:
			* decrypts the credentials.
			* connects to the data source(s) with those credentials.
			* sends the query to the data source to be run.
		* The data source:
			* sends the results back to the on-premises gateway and then back to the gateway cloud service, which shows these results to the user.
	* Note ([M source](https://learn.microsoft.com/en-us/training/modules/manage-datasets-power-bi/8-troubleshoot-connectivity)): All of the above applies if we want to connect a user to an on-premise data source. However, if the user is solely dealing with cloud services, like SharePoint, then they do not require a gateway because the data is already in the cloud; they only need to provide authorization credentials to set up a data source connection. So, if a report fails to refresh, they should ensure that the data source credentials are up to date. For more information, see [Troubleshooting refresh scenarios](https://learn.microsoft.com/en-us/power-bi/connect-data/refresh-troubleshooting-refresh-scenarios/).


There are two types of on-premises data gateways:
* Organization mode
	* multiple users -> multiple on-premises data sources
* Personal mode
	* one user -> multiple on-premises data sources.
	* suitable in situations where you're the only one in your organization who creates reports;
		* You will install the gateway on your local computer, which needs to stay online for the gateway to work.

To use an on-premises gateway:
* [Install the on-premises data gateway](https://learn.microsoft.com/en-us/data-integration/gateway/service-gateway-install/)
* Make an admin configure it based on organizational needs.
* sign in by using your Microsoft 365 organization account.

To troubleshoot an on-premises data gateway:
* Run a network port test, see [Adjust communication settings for the on-premises data gateway](https://learn.microsoft.com/en-us/data-integration/gateway/service-gateway-communication#network-ports-test/?azure-portal=true).
* Provide proxy information for your gateway, see [Configure proxy settings for the on-premises data gateway](https://learn.microsoft.com/en-us/data-integration/gateway/service-gateway-proxy/).
* Find the current data center region that you're in, see [Set the data center region](https://learn.microsoft.com/en-us/data-integration/gateway/service-gateway-data-region/).

## Dataset Scheduled Refresh

[M source](https://learn.microsoft.com/en-us/training/modules/manage-datasets-power-bi/5-dataset-refresh)

The **Scheduled refresh** feature allows us to:
* define the frequency and time slots to refresh a particular dataset.

Scheduled refresh creation steps:
* create a gateway connection.
* select the **Schedule refresh** icon:
  ![[Pasted image 20231016220639.png]]
	* Side note: the on-demand refresh doesn't affect the next scheduled refresh time.
* Do the following:
  ![[Pasted image 20231016220543.png]]

Limitations:
* Maximum numbers of daily scheduled refreshes:
	* Dataset is on a shared capacity -> **8**
	* Power BI Premium -> **48**
* Refresh might not take place at that exact time
	* The goal is to initiate the refresh within **15** minutes of the scheduled time slot
	* A delay of up to **one hour** can occur if the service can't allocate the required resources sooner.

To check the refresh status you can either:
* Check it from here:
  ![[Pasted image 20231016221038.png]]
* Or from the refresh history page of the dataset's settings window:
  ![[Pasted image 20231016221105.png]]

## Dataset Incremental Refresh

[M source](https://learn.microsoft.com/en-us/training/modules/manage-datasets-power-bi/6-incremental-refresh)

Incremental refresh benefits:
* refresh large datasets quickly and often, without having to reload historical data each time.
* Quicker refreshes
	* Only data that needs to be changed gets refreshed. For example, if you have five years' worth of data, and you only need to refresh the last 10 days because that is the only data that has changed, the incremental refresh will refresh only those 10 days of data.
* More reliable refreshes
	* no need to keep your long-running data connections open to schedule a refresh.
* Reduced resource consumption
	* only need to refresh the smaller the amount of data, the overall consumption of memory and other resources is reduced.

Use case scenario:
* It isn't feasible for to manually refresh the data by adding a new file because:
	* the refreshes need to happen regularly to match the frequency of the live transactions that are occurring. 
	* the manual refresh task is becoming more difficult because the datasets have millions of rows. 
	* the PBIX file is limited by the memory resources that are available on the desktop computer, so importing large datasets is not an option.
* Consequently, you need to implement a better data refresh solution; incremental data refresh.

To define an incremental refresh policy, follow these steps:
* Define the filter parameters.
	* These are built-in (keyword) parameters called <mark style="background: #FFB8EBA6;">RangeStart and RangeEnd. These are used as</mark>:
		* a <mark style="background: #FFB8EBA6;">filtering window</mark> because they restrict the used data pulled into Power BI desktop to the specified range.
		* a <mark style="background: #FFB8EBA6;">sliding window</mark> to determine what data to pull into Power BI service.
	* Definition steps:
	  ![[Pasted image 20231016222315.png]]
* Use the parameters to apply a filter.
	* Steps:
		* Right click a chosen column, then select **custom filter**:
		  ![[Pasted image 20231016222446.png]]
		* Then, in the **Filter Rows** window that displays:
		  ![[Pasted image 20231016222531.png]]
		* We should now see a subset of the dataset in Power BI Desktop.
* Define the incremental refresh policy.
* Publish changes to Power BI service.

To define the incremental refresh policy, follow these steps:
* Right click the chosen table which you've applied the filter for, then:
  ![[Pasted image 20231016222655.png]]
* Then, configure the refresh as required. In this example, you will define a refresh policy to store data for five full calendar years, plus data for the current year up to the current date, and incrementally refresh 10 days of data:
  ![[Pasted image 20231016222734.png]]
* The two refresh operations above will apply the following logic (from top to bottom):
	* <mark style="background: #FFB8EBA6;">load the historical data</mark> for the last five years.
	* <mark style="background: #FFB8EBA6;">incrementally refresh the data</mark> that was changed in the last 10 days up to the current date <mark style="background: #FFB8EBA6;">and remove calendar years that are older than five years prior to the current date</mark>.
* Then, to apply that refresh policy, you need to publish the report to Power BI service.

For more information, see [Incremental refresh on Power BI](https://learn.microsoft.com/en-us/power-bi/service-premium-incremental-refresh/).


## Dataset Promotion and Certification

[M source](https://learn.microsoft.com/en-us/training/modules/manage-datasets-power-bi/7-manage-datasets)

Use case scenario: 
* the organization has many datasets that can be accessed by many users.
* We should direct users to the most up-to-date and highest-quality datasets in our workspaces.
* This is done by endorsing those optimized datasets as the ***one source of truth***. Endorsement can be done using promotion or certification:
	* Promotion
		* Promote your datasets when they're **ready for broad usage**.
		* Requirements:
			* write permissions on the workspace containing the content to be promoted. I.e., an [[Power BI#^68di4d|Admin]].
		* Steps:
			* In Power BI Service:
			  ![[Pasted image 20231017073316.png]]
			* Then:
			  ![[Pasted image 20231017073336.png]]
			* Result:
			  ![[Pasted image 20231017073421.png]]
			  This indicates that the dataset ready for viewing by all users.
	* Certification
		* Use case scenario: 
			* users expected to see a sales report and are now looking at a product report instead. We should direct users users to the datasets that they should be accessing
		* ***Certification will require users to have special access*** before they can view the Sales dashboards, so no confusion will occur when sharing multiple reports.
		* Requirements:
			* Request certification for a promoted dataset from the dataset's owner.
				* Only authorized users (i.e., content owners) can certify content. Other users can request content certification.
			* Certification can be a highly selective process, so only the truly reliable and authoritative datasets are used across the organization.
		* Steps:
			* To request certification:
			  ![[Pasted image 20231017073558.png]]
			  If it is greyed out, the organization's admins will provide details in a link titled, _"How do I get my dataset certified?"_ in the **Certified** section.

For more information, see [Promote your dataset](https://learn.microsoft.com/en-us/power-bi/service-datasets-promote/) or [Certify datasets](https://learn.microsoft.com/en-us/power-bi/service-datasets-certify/).

## Query Caching

[M source](https://learn.microsoft.com/en-us/training/modules/manage-datasets-power-bi/9-query-caching)

Use case scenario:
* Normally, we rely on the dataset to calculate queries, which when overloaded can reduce performance. This can lead to long loading times of reports and dashboards. To solve this, one might use query caching.

Regarding query caching:
* It is only available to users with Power BI Premium or Power BI Embedded.
* It can only be used on a specific page of a report at a time.
* Benefits:
	* It reduces loading time and increases query speed especially for datasets that are not refreshed often and are accessed frequently.
	* It respects bookmarks and default filters, so even if we enable query caching, any bookmarks that we have created still exist.
	* It caches query results to a specific user at a time.
	* It follows [[#Data Protection Using Sensitivity (Security) Labels|security labels]].
	* It reduces the load on your dedicated capacity by using cloud resources on your premium capacities on Power BI service to load the report.
* Steps:
	* Click here:
	  ![[Pasted image 20231017075030.png]]
	* ThenSelect the **Datasets** tab and expand the **Query Caching** options to see this:
	  ![[Pasted image 20231017075100.png]]
	* choose one of the available options. The default option is that query caching is turned off; however, we can also select **Off**, which turns off query caching for the specific dataset in question. If we select **On**, <mark style="background: #FFB8EBA6;">query caching will be turned on for this specific dataset only</mark>.
	* Side notes:
		* Switching from **On** to **Off** will clear all previously saved query results.
		* When turning off query caching, a small delay will occur in query loading because the report queries are running against the dataset and it does not have saved queries to fall back on.
		* If many datasets have query caching enabled, and a refresh occurs, a reduction in performance might occur because a large number of queries are being processed at once.

For more information, see [Query Caching in Power BI](https://learn.microsoft.com/en-us/power-bi/connect-data/power-bi-query-caching/).

# Dashboards

[M source](https://learn.microsoft.com/en-us/training/modules/create-dashboards-power-bi/1-introduction)

Dashboard characteristics:
* Can be created from multiple datasets or reports.
* Can't make edits on the dashboard tiles.
	* Dashboards do not have the **Filter**, **Visualization**, and **Fields** panes, so we can't add new filters and slicers.
* Can only be a single page (canvas).
* Can't see the underlying dataset directly in a dashboard.
* Both dashboards and reports can be refreshed to show the latest data.
* Its tiles can be sourced from a multitude of places including reports, datasets, other dashboards, Microsoft Excel, SQL Server Reporting Services, and more.
	* A report element pinned in the dashboard acts as a direct connection between the dashboard and the report that the snapshot came from.
		* To pin a report to a dashboard, go to the report visual that you want to pin, then:
		  ![[Pasted image 20231017110035.png]]
		  then:
		  ![[Pasted image 20231017110044.png]]
	* Dashboard tiles can also be created from ***custom streaming data*** like so ([M source](https://learn.microsoft.com/en-us/training/modules/create-dashboards-power-bi/7-configure-real-time-dashboard)):
	  ![[Pasted image 20231017133847.png]]
	  this is useful for the following use case scenario: sensors on machines constantly send a stream of data to "IoT hub", where they'll be housed in their native, messy format. From there, we can use a stream insight job to aggregate the data, meaning that it will clean the data and quiet the noisy messages. Then, we can retrieve the data into Power BI as a streaming dataset, where we can consume the information and build the required visuals. This process can be illustrated like this:
	  ![[Pasted image 20231017134036.png]]
	  For more information, see [Real-time streaming in Power BI](https://learn.microsoft.com/en-us/power-bi/connect-data/service-real-time-streaming).
* Can pin an entire page of a report (i.e., live page)
	* Any changes that we make to the report will automatically show on the dashboard when the page is refreshed. In Power BI Desktop, we can make changes to our visuals or data as needed and then ***deploy to the appropriate workspace file, which will update the report and simultaneously update the dashboard as well***.
* Can create data alerts for pinned visuals:
	* Steps:
	  ![[Pasted image 20231017123245.png]]
	  Then:
	  ![[Pasted image 20231017123254.png]]
	* Note: <mark style="background: #FFB8EBA6;">data alerts are available to whomever has access to the dashboard, not just the dashboard owner</mark>.
		* I.e., each user can have their own set of alerts.
	* For more information, see [Data Alerts in Power BI service](https://learn.microsoft.com/en-us/power-bi/create-reports/service-set-data-alerts).
* Can get quick insights on the dataset
	* Steps:
	  ![[Pasted image 20231017132825.png]]
	  Then, this appears:
	  ![[Pasted image 20231017132838.png]]
	  Clicking on "View insights" will open the **Quick Insights** page for the selected dataset, which contains up to 32 separate insight cards. Illustration of a single insight card:
	  ![[Pasted image 20231017132934.png]]
	  Clicking on an insight card will make us enter **Focus mode**, where we can:
		* Filter the visualization using the filters pane.
		* Pin the insight card to a dashboard.
		* Run insights on the card (scoped insights) by selecting Get insights in the upper-right corner. 
			* The scoped insights allow you to drill into your data.
		* Return to the original insights canvas by selecting Exit Focus mode in the upper-left corner.
* Can have different dashboard themes
	* Steps:
	  ![[Pasted image 20231017133236.png]]
	  where "Custom" will give us these options:
	  ![[Pasted image 20231017133326.png]]
* Can perform data classification ([M source](https://learn.microsoft.com/en-us/training/modules/create-dashboards-power-bi/8-configure-data-classification))
	* This will raise security awareness to viewers of a dashboard so that they know what level of security should be considered when viewing or sharing a dashboard. 
	* This will not enforce policies because data protection does.
	* Requirements:
		* Only the **dashboard owner who is a Power BI service Admin** can change the dashboard's classification. ^u7k3wc
	* Classification types: **High Impact**, **Low Impact**, and **Medium Impact**
	* Steps:
	  ![[Pasted image 20231017134847.png]]
	  then:
	  ![[Pasted image 20231017134907.png]]
	  Result:
	  ![[Pasted image 20231017135034.png]]
* Can set up mobile view
	* This can be done either from Power BI desktop **for reports**, or from Power BI service **for dashboards**.
	* Note: in a 2020 June release of Power BI, a new grid has been added to this view so that we can orient our visuals with more ease and overlay visuals on top of each other. This feature can be useful if we want to insert a visual on top of an image.
	* For more information, see [Optimize a dashboard for mobile phones](https://learn.microsoft.com/en-us/power-bi/create-reports/service-create-dashboard-mobile-phone-view).








