
# Dataplex

Great video for an overview can be found [here](https://www.youtube.com/watch?v=rDANpCVsO9s).

Overview:

**Definition:**
- Unified data management and governance platform.
- Centralized data storage and processing across distributed environments.

**Usage:**
- Manage data across cloud and on-premises environments.
- Automate data discovery, metadata management, and policy enforcement.
- Enhance data security and compliance.
- Simplify data analytics and machine learning workflows.

**Case Scenario:**
- A company with data stored in multiple locations (cloud, on-premises) needs a single platform to manage, govern, and analyze their data efficiently.
- Ensuring compliance with data privacy regulations by automating policy enforcement.
- Centralizing metadata management to improve data discovery and collaboration among data teams.

**Side notes**:
* The term "plex" suggests a multiplex environment, indicating the platform's capability to handle multiple data sources, environments, and types in a unified manner.

Terminologies are mentioned in [Data Mesh](#Data%20Mesh)

# Dataflow

* Dataflow allows you to process data in near-real time
* implement custom data cleansing and outlier detection algorithms that operate on streaming data.

# Pub/Sub

* Google Cloud Pub/Sub can manage high-volume data ingestion.
	* This is done by decoupling vote collection (for example) from processing, which ensures scalability and resilience under high load.

# Bigtable

* Bigtable is excellent for handling high-throughput writes and reads (i.e., low-latency), making it suitable for real-time vote tallying (for example).

# BigQuery

* Using BigQuery as a sink allows you to store the cleaned and processed data efficiently for further analysis or ***use in AI models***. 


## BigQuery Storage
### Clustering

![](Media-Temp/Pasted%20image%2020240623175356.png)

([source](https://cloud.google.com/bigquery/docs/clustered-tables))

* Usage using example columns:
	* Clustering the data by location_id and device_version within each partition will keep related data close together and optimize the performance of filters on those columns.

### Partitioning

![](Media-Temp/Pasted%20image%2020240623175531.png)

([source](https://cloud.google.com/bigquery/docs/partitioned-tables))

* Usage using example columns:
	* Partitioning the data by create_date will allow BigQuery to prune partitions that are not relevant to the query by date.

# Data Architectures

## Data Mesh

**Definition:**
- Decentralized data architecture approach.
- Treats data as a product managed by domain-oriented teams.

**Usage:**
- Promote cross-functional teams owning their data pipelines and datasets.
- Improve scalability and agility in data management.
- Facilitate data democratization and access across the organization.

**Case Scenario:**
- A large organization with multiple departments wants each team to manage their data independently while ensuring interoperability.
- Enhancing data quality and availability by assigning data ownership to the teams that best understand the data.
- Enabling faster data-driven decision-making by reducing dependencies on centralized data teams.

## Terminologies: Dataplex vs Data Mesh

In each of the following sub-headers, first and second terms are related to dataplex and data mesh respectively.

sources:
* https://cloud.google.com/architecture/data-mesh
* https://cloud.google.com/blog/products/data-analytics/build-a-data-mesh-on-google-cloud-with-dataplex-now-generally-available

Side note: Illustration of Dataplex related terminologies ([source](https://medium.com/@poojakhaire000/dataplex-1-an-overview-of-google-cloud-dataplex-12894f37e784#:~:text=implementation%2Dagnostic%20understanding.-,Manage%20Lakes,-%3A)):

![](Media-Temp/Pasted%20image%2020240623194400.png)

### Dataplex Zone vs Data Domain

**Dataplex Zones:**
- **Definition:** Logical partitions within Dataplex to organize and manage data.
- **Usage:** Segregate data based on data lifecycle stages, security requirements, or business domains.
- **Case Scenario:** <mark style="background: #FFB8EBA6;">Separate zones for raw data ingestion, processed data, and analytical data</mark>.
	- Therefore, <mark style="background: #D2B3FFA6;">focuses on structuring data based on technical criteria or lifecycle stages</mark> for efficient management and governance within a data platform.

**Data Domain:**
- **Definition:** Specific business areas or categories to which [data products and resources](#Dataplex%20Asset%20vs%20Data%20Product,%20Data%20Resource) belong, often aligned with organizational functions or units.
- **Usage:** Organizes data according to business functions to promote better management, ownership, and accountability.
- **Case Scenario:** Defining domains like finance, marketing, and HR, where each domain manages its own data products and resources, ensuring that relevant teams have control and responsibility over their data.
	- Therefore, <mark style="background: #D2B3FFA6;">focuses on aligning data with business</mark> functions or organizational units to facilitate decentralized data management and ownership.
- Side note: Some [sources](https://medium.com/@poojakhaire000/dataplex-1-an-overview-of-google-cloud-dataplex-12894f37e784#:~:text=Lake%20is%20represents%20a%20data%20domain%20or%20business%20unit) compare data domain with [Dataplex Lake](#Dataplex%20Lake), but I don't know if that's a logical comparison or not.

### Dataplex Asset vs Data Product, Data Resource

**Dataplex Assets:**
- **Definition:** Individual data entities within a Dataplex zone, such as datasets or tables.
	- So a Dataplex asset is either a ***data product*** (e.g., dataset), or a ***data resource*** (e.g., table)
- **Usage:** Managed and governed through Dataplex for accessibility and compliance.
- **Case Scenario:** A BigQuery table within a Dataplex zone dedicated to sales data.

**Data Product:**
- **Definition:** A curated dataset or data service designed to be easily consumable and usable.
	- A logical container or grouping of one or more related [data resources](#Dataplex%20Asset%20vs%20Data%20Resource).
- **Usage:** Shared across teams to facilitate data analysis and decision-making.
- **Case Scenario:** A marketing team creates a customer segmentation dataset for use by sales and finance teams.


**Data Resource:**
- **Definition:** Any data entity managed within a data platform, such as tables, files, or streams.
	- A physical asset in a storage system which holds structured data or stores a query that yields structured data.
	- Side note: a **data attribute** is a field or element of a data resource.
- **Usage:** Registered and cataloged for easy access and governance.
- **Case Scenario:** A cloud storage bucket containing transaction logs.

### Dataplex Lake

**Dataplex Lake:**
- **Definition:** A centralized data repository within Google Cloud's Dataplex that consolidates data from various sources for unified management, governance, and analytics.
- **Usage:** Facilitates the integration and management of diverse data sources, allowing for streamlined data operations and analytics.
- **Case Scenario:** <mark style="background: #FFB8EBA6;">A company consolidates (i.e., integrates) its sales, customer, and product data into a Dataplex lake for centralized governance and to support advanced analytics and machine learning initiatives</mark>.



# Data Jargon

## Data Discovery

![](Media-Temp/Pasted%20image%2020240623183551.png)

([source](https://www.cloudskillsboost.google/paths/420/course_templates/962/video/472053))

## Data Curation

![](Media-Temp/Pasted%20image%2020240623183616.png)

([source](https://www.cloudskillsboost.google/paths/420/course_templates/962/video/472053))

## Data Unification

![](Media-Temp/Pasted%20image%2020240623184101.png)

([source](https://www.cloudskillsboost.google/paths/420/course_templates/962/video/472053))