
# Reports vs Dashboards vs Apps
[Microsoft source 1](https://learn.microsoft.com/en-us/training/modules/get-started-with-power-bi/3-building-blocks-of-power-bi) and [2](https://learn.microsoft.com/en-us/training/modules/get-started-with-power-bi/4-exercise-touring-and-using-power-bi)
## Reports vs Dashboards

![[Pasted image 20230929210107.png]]
([source](https://learn.microsoft.com/en-us/power-bi/create-reports/service-dashboards))

![[Pasted image 20230929210329.png]]
([source](https://k21academy.com/microsoft-azure/data-analyst/dashboards-vs-reports-in-power-bi/))

## Dashboards vs Apps

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

## Visualizing The Three

App example:
![[Pasted image 20230929211052.png]]
([source](https://learn.microsoft.com/en-us/training/modules/get-started-with-power-bi/4-exercise-touring-and-using-power-bi))

Dashboard example is the same as the image above, but only the dashboard tab:
![[Pasted image 20230929211103.png]]

Report example:
![[Pasted image 20230929211134.png]]
(note: the "Top 100 Contributors" is a page in the report, so the report contains 6 pages in total)

# Power BI Core Components

[Microsoft Source](https://learn.microsoft.com/en-us/training/modules/get-started-with-power-bi/5-summary-cleanup)

**Microsoft Power BI** is a comprehensive set of software tools, apps, and connectors that transform data into interactive insights. It accommodates various data sources and can be tailored to match your organization's complexity.

- **Power BI Desktop** for authoring reports made up of datasets and visualizations.
- **Power BI service** for creating dashboards from published reports and distributing content with apps.
- **Power BI Mobile** for on-the-go access to the Power BI service content, designed for mobile.

# Parameter Value Types

([source](https://www.youtube.com/watch?v=twBUmqVOGgg))
There are two types: 
1. Power BI Query Parameters.
	1. By changing these you can **change the data that is loaded** in it your Power BI model.
2. Parameters used in Power BI Reports.
	1.  by changing these parameters users can **change what is shown on the report**.

# Custom Invoke Functions

https://www.youtube.com/watch?v=ynr9VE9QQXc

# Change The Source File

[M source](https://learn.microsoft.com/en-us/training/modules/get-data/2-data-files#:~:text=Change%20the%20source,select%20Close.)

# Load JSON Using Expander

when loading NoSQL data (from Cosmos DB for example), data will initially look like this:
![[Pasted image 20230930080619.png]]

So click load, then click on the expander button, then uncheck prefix option, then apply:
![[Pasted image 20230930080722.png]]

# Selecting a Storage Mode

([Microsoft source](https://learn.microsoft.com/en-us/training/modules/get-data/6-storage-mode))

The most popular way to use data in Power BI is to **import it into a Power BI dataset**. Importing the data means that the data is stored in the Power BI file and gets published along with the Power BI reports.

The three different types of storage modes you can choose from:
- Import
	- Create a local Power BI copy of your datasets from your data source. You can use all Power BI service features with this storage mode, including Q&A and Quick Insights. Data refreshes can be scheduled or on-demand.
- DirectQuery
	- query the specific tables that you'll need by using native Power BI queries, and the required data will be retrieved from the underlying data source.
- Dual (Composite)
	- identify some data to be directly imported and other data that must be queried. Any table that is brought in to your report is a product of both Import and DirectQuery modes. Using the Dual mode allows Power BI to choose the most efficient form of data retrieval.


# Querying Methods

## SQL vs T-SQL

([source](https://pediaa.com/what-is-the-difference-between-sql-and-tsql/))
![[Pasted image 20230930081913.png]]

# Fixing Performance Issues

[Microsoft source](https://learn.microsoft.com/en-us/training/modules/get-data/8-performance-issues)

Tips: 
* **Separate date and time, if bound together.** If any of your tables have columns that combine date and time, make sure that you separate them into distinct columns before importing them into Power BI. This approach will increase compression abilities.
* **Process as much data as possible in the original data source.** Power Query and Power Query Editor allow you to process the data; however, the processing power that is required to complete this task might lower performance in other areas of your reports. Generally, a good practice is to process, as much as possible, in the native data source.
## Query Folding

ChatGPT:
Query Folding is a performance optimization feature in Power BI that allows the Power Query engine to push data transformation operations back to the data source, such as a database or web service, instead of performing them locally within Power BI. This can significantly improve query performance by reducing the amount of data transferred over the network and processed locally.

Example: Let's say you have a Power BI report that connects to a SQL database. You want to filter the data to only include records where the sales amount is greater than $1,000 and then aggregate the results. Without query folding, Power BI might first retrieve all the data from the database and then apply the filter and aggregation operations locally. With query folding, Power BI sends a SQL query to the database that includes the filter and aggregation operations, and the database performs these operations. This results in faster and more efficient data processing.

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

## Model framework

<mark style="background: #FF5582A6;">Table storage mode settings determine the model framework</mark>, which can be either import, DirectQuery, or <mark style="background: #D2B3FFA6;">composite</mark>. The following units in this module describe each of these frameworks and provides guidance on their use.

- An import model comprises tables that have their storage mode property set to **Import**.
- A DirectQuery model comprises tables that have their storage mode property set to **DirectQuery**, and they belong to the same **source group**. Source group is described later.
- A composite model comprises more than one source group.

check [this](https://learn.microsoft.com/en-us/training/modules/choose-power-bi-model-framework/6-choose-model-framework), only after you finish the subsequent sections, to see the guidelines of choosing the right model framework.

### Import Model

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

### DirectQuery Model

[M source](https://learn.microsoft.com/en-us/training/modules/choose-power-bi-model-framework/4-determine-when-to-develop-directquery-model)

* A DirectQuery model consists of DirectQuery storage mode tables that belong to the same source group. ^ngupkb
	* A source group is a set of tables that are related to a data source. It has two types:
	* Import source group: set of import storage mode tables related to a data source. ^v8cl9b
	* DirectQuery source group: set of DirectQuery storage mode tables related to a data source.
	* Side note: if we have more than one source group, then the model framework we're currently using is called a composite model.

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

In regards to optimizing the performance issues, you can use **DirectQuery user-defined aggregation tables** by adding user-defined aggregation tables to a DirectQuery model. 
User-defined aggregation tables are special model tables that are hidden (from users, calculations, and RLS). They work best when they satisfy higher-grain analytic queries over large fact tables. When you set the aggregation table to use DirectQuery storage mode, it can query a materialized view in the data source. You can also set an aggregation table to use import storage mode or enable automatic aggregations, and these options are described in Unit 4.

For more information, see [DirectQuery model guidance in Power BI Desktop](https://learn.microsoft.com/en-us/power-bi/guidance/directquery-model-guidance).

### Composite Model

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

#### Boost DirectQuery model performance with import data

When there’s a justification to develop a DirectQuery model, you can mitigate some limitations by using specific Power BI features that involve import tables.

##### Import aggregation tables

* Enable automatic aggregations to direct fact queries to a cached aggregation. 
* ensure that related dimension tables are set to use dual storage mode.
* Automatic aggregations are a Premium feature. For more information, see [Automatic aggregations](https://learn.microsoft.com/en-us/power-bi/enterprise/aggregations-auto).

##### Dual storage mode

A dual storage mode table is set to use both import and DirectQuery storage modes. At query time, Power BI determines the most efficient mode to use. Whenever possible, Power BI attempts to satisfy analytic queries by using cached data.

Dual storage mode tables work well with import aggregation tables.

Slicer visuals and filter card lists, which are often based on dimension table columns, render more quickly because they’re queried from cached data.

#### Deliver real-time data from an import model

When you set up an import table with incremental refresh, you can enable the **Get the latest data in real-time with DirectQuery** option.

![Animated diagram shows the incremental refresh and real-time data set up, and it highlights the Get the latest data in real-time with DirectQuery option.](https://learn.microsoft.com/en-us/training/wwl-data-ai/choose-power-bi-model-framework/media/model-framework-incremental-refresh.png)

By enabling this option, Power BI automatically creates a table partition that uses DirectQuery storage mode. In this case, the table becomes a hybrid table, meaning it has import partitions to store older data, and a single DirectQuery partition for current data.

When Power BI queries a hybrid table, the query uses the cache for older data, and passes through to the data source to retrieve current data.

This option is only available with a Premium license.

For more information, see [Configure incremental refresh and real-time data](https://learn.microsoft.com/en-us/power-bi/connect-data/incremental-refresh-configure).

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
* CALENDAR()
	* returns a contiguous range of dates based on a start and end date that are entered as arguments in the function.
* CALENDARAUTO()
	* returns a contiguous, complete range of dates that are automatically determined from your dataset (using earliest and last dates of found in your dataset. However, ending date [can be even later than that](<https://learn.microsoft.com/en-us/training/modules/design-model-power-bi/3-date-table#:~:text=plus%20data%20that%20has%20been%20populated%20to%20the%20fiscal%20month%20that%20you%20can%20choose%20to%20include%20as%20an%20argument%20in%20the%20CALENDARAUTO()%20function.>))

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

Note:
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

# DAX (Data Analysis Expression)

## DAX Calculation Types

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-write-formulas/1-introduction)

By using Data Analysis Expressions (DAX), you can add three types of calculations to your data model:
- Calculated tables
- Calculated columns
- Measures

Note:
DAX can also be used to define row-level security (RLS) rules, which are expressions that enforce filters over model tables. However, rules aren't considered to be model calculations so they're out of scope for this module. More information will be shown later, but for now, see [Row-level security (RLS) with Power BI](https://learn.microsoft.com/en-us/power-bi/admin/service-admin-rls/).

### Calculated Tables

* The formula can duplicate or transform _existing model data_, or create a series of data, to produce a new table.
* Calculated table data is always imported into your model, so it increases the model storage size and can prolong data refresh time.

Note
A calculated table can't connect to external data; you need to use Power Query to accomplish that task.

Calculated tables can be useful in various scenarios:
- [[#Creating a Date Table|Date tables]]
- [[#Role-Playing Dimensions|Role-playing dimensions]]
- What-if analysis

#### What-If Analysis (Disconnected Tables)

When you create a [What-if parameter](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-what-if/), a calculated table is automatically added to your model. Example ([source](https://www.youtube.com/watch?v=6a_5uderwAg)):
![[Pasted image 20231004113636.png]]

What-if parameters allow report users to select or filter by values that are stored in the calculated table. Measure formulas can use selected value(s) in a meaningful way. In the example above, the what-if parameter is the chosen numeric range in `Pct Sales Forecast`, and the measure formula is to multiply this numeric value by the `Total Sales` column to get the `Total Sales Forecast` bars in the bar chart above.

Notably, what-if calculated tables aren't related to other model tables because they're not used to propagate filters. For this reason, they're sometimes called _disconnected tables_.

### Calculated Columns

* write a DAX formula to add a calculated column to any table in your model. 
	* The formula is evaluated for each table row and it returns a single value.
* Increases the storage size of your model.

Its appearance is like this:
![[Pasted image 20231004131317.png]]

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
	* Are identified in the Fields pane because they're shown with the sigma symbol ( ∑ ).
		* Note: Any column can be summarized when added to a visual. Therefore, whether they're shown with the sigma symbol or not, when they're added to a visual, they can be set up as implicit measures.
	* Are automatic behaviors that allow visuals to summarize model column data.

#### "Calculated Measure" is a Non-Existent Term

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-measures/2-simple-measures#:~:text=In%20tabular%20modeling%2C%20no%20such%20concept%20as%20a%20calculated%20measure%20exists.%20The%20word%20calculated%20is%20used%20to%20describe%20calculated%20tables%20and%20calculated%20columns.%20It%20distinguishes%20them%20from%20tables%20and%20columns%20that%20originate%20from%20Power%20Query%2C%20which%20doesn%27t%20have%20the%20concept%20of%20an%20explicit%20measure)

Regarding the word "calculated":
* It describes calculated tables and calculated columns
	* These are created from DAX while normal tables and columns are created from Power Query
* Therefore, it doesn't apply to measures.

TLDR; Power Query doesn't have the concept of a measure.

### Calculated Columns vs Measures

[M source](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-add-measures/5-compare-calculated-columns-measures)

Calculated columns and measures differ in the following points:
- **Purpose** - Calculated columns extend a table with a new column, while measures define how to summarize model data.
- **Evaluation** - Calculated columns are evaluated by using <mark style="background: #D2B3FFA6;">row context</mark> at data refresh time, while measures are evaluated by using <mark style="background: #D2B3FFA6;">filter context</mark> at query time. Filter context is introduced in a later module; it's an important topic to understand and master so that you can achieve complex summarizations.
	- Side note ([source](https://endjin.com/blog/2022/04/measures-vs-calculated-columns-in-dax#:~:text=When%20you%20write%20a%20calculated%20column%2C%20you,wrap%20the%20column%20in%20an%20aggregation%20function.)): <mark style="background: #FF5582A6;">because measures don't see row context, you can't refer to columns directly</mark>, and instead you must wrap the columns in aggregation functions first. For example, the `SUM` in `Quantity = SUM(Sales[Order Quantity])`.
- **Storage** - Calculated columns (in Import storage mode tables) store a value for each row in the table, but a measure never stores values in the model.
- **Visual use** - Calculated columns (like any column) can be used to filter, group, or summarize (as an implicit measure), whereas measures are designed to summarize.

## DAX Syntax

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

Note: check out logical operators [here](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-write-formulas/5-operators#:~:text=%26%20%27Product%27%5BColor%5D-,Logical%20operators,-Use%20logical%20operators). Moreover, here's an example of `IN` operator:
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

### BLANK Data Type

* DAX uses BLANK for both database NULL and for blank cells in Excel. 
* BLANK doesn't mean zero.
* Think of it as the _absence of a value_.
* [`BLANK`](https://learn.microsoft.com/en-us/dax/blank-function-dax/) DAX function returns BLANK, while the [`ISBLANK`](https://learn.microsoft.com/en-us/dax/isblank-function-dax/) DAX function tests whether an expression evaluates to BLANK.
* Regarding how BLANK is dealt with in [implicit conversions](https://learn.microsoft.com/en-us/training/modules/dax-power-bi-write-formulas/5-operators#:~:text=DAX%20operators.-,Implicit%20conversion,-When%20writing%20a):
	* It's handled similar to how Excel treats BLANK
	* It's different to how databases (SQL) treat NULL.
	* <mark style="background: #D2B3FFA6;">BLANK is treated as zero when acted on by arithmetic operators and as an empty string when concatenated to a string.</mark>

### DAX Variables

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

Notice how the `CALCULATE(...)` part is repeated twice. So, to run this definition formula in at least half the time, let's define this part as a variable like so:
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


### DAX Confusing Functions

#### COUNT Related Functions

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



