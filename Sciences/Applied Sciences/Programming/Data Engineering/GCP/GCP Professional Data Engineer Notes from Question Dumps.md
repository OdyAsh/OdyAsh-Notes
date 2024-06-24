
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

## Networks in Dataflow

Main sources:
* https://cloud.google.com/dataflow/docs/guides/specifying-networks
* https://cloud.google.com/dataflow/docs/guides/routes-firewall

### Default Network Configurations

* The default network has configurations that allow Dataflow jobs to run. 
* However, <mark style="background: #D2B3FFA6;">other services might also use this network</mark>. 
	* Therefore, ensure that your changes to the default network are compatible with all of your services. 
	* <mark style="background: #D2B3FFA6;">Alternatively, create a separate network for Dataflow</mark>.


## Networks Jargon

**VPC network**:
* Stands for Virtual Private Cloud
	* Also called "a network".
* Is a virtual version of a physical network that is implemented inside of Google's production network.
* Provides connectivity for resources in a project.

**Shared VPC network**:
* Allows the designation of a project as a ***host project*** and attach one or more other ***service projects*** to it. 
* The VPC networks in the host project are called _Shared VPC networks_.
* To <mark style="background: #D2B3FFA6;">use some of the subnetworks in host project's network, you need to be a shared VPC admin</mark>.

**VPC Service Controls**:
* creates perimeters that protect the resources and data of services that you explicitly specify.
* This will minimize unwarranted data exfiltration risks.

**Firewall rules**:
* <mark style="background: #FFF3A3A6;">Use firewall rules to allow or deny traffic to and from your VMs</mark>.

## External IP Address

* By default, the Dataflow service <mark style="background: #FFB8EBA6;">assigns workers both external and internal IP addresses</mark>. 
* When you turn off external IP addresses, the Dataflow pipeline can access resources only in the following places:
	*  Another instance in the same VPC network
	- A [Shared VPC network](https://cloud.google.com/vpc/docs/shared-vpc)
	- A network with [VPC Network Peering](https://cloud.google.com/vpc/docs/vpc-peering) enabled

Advantages of turning it off:
* Not using external IP addresses helps to better secure your data processing infrastructure. 
* Additionally, you also lower the number of external IP addresses that you consume against your [Google Cloud project quota](https://cloud.google.com/vpc/docs/quota).

Disadvantages:
* Dataflow jobs cannot access APIs and services outside of Google Cloud that require internet access.

## Network Tags

* [Network tags](https://cloud.google.com/vpc/docs/add-remove-network-tags) are text attributes that you can attach to Compute Engine VMs. 
* A network tags lets you <mark style="background: #FFF3A3A6;">apply a custom network configuration</mark> of VPC network firewall rules (and custom static routes) <mark style="background: #FFF3A3A6;">to specific VM instances</mark>. 

## Firewall Rules for Dataflow

* Firewall rules let you allow or deny traffic to and from your VMs. 
* If your Dataflow jobs use [Dataflow Shuffle](https://cloud.google.com/dataflow/docs/shuffle-for-batch) or [Streaming Engine](https://cloud.google.com/dataflow/docs/streaming-engine), <mark style="background: #FFB8EBA6;">then you don't need to configure any firewall rules</mark>. 
* <mark style="background: #FFB8EBA6;">Otherwise, you must configure</mark> firewalls rules so that Dataflow VMs can send and receive network traffic on TCP port <mark style="background: #FFB8EBA6;">12345 for streaming</mark> jobs and on TCP port <mark style="background: #FFB8EBA6;">12346 for batch</mark> jobs.
* <mark style="background: #FF5582A6;">Caveat</mark>: <mark style="background: #D2B3FFA6;">If you created custom</mark> network tags when you ran the pipeline code, Dataflow VMs use those tags. <mark style="background: #D2B3FFA6;">Create the firewall rules with the custom tags</mark>.

## SSH for Dataflow Debugging

* If your worker VM has an external IP address, you can [connect to the VM](https://cloud.google.com/compute/docs/instances/connecting-to-instance) using CLI. 
* To do so, you <mark style="background: #D2B3FFA6;">must have a firewall rule that allows incoming connections on TCP port 22 from at least the IP address of the system</mark> on which you're running `gcloud` or the system running the web browser you use to access the Google Cloud console.

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

# Memorystore for Redis

Main sources:
* https://cloud.google.com/memorystore/docs/redis/memorystore-for-redis-overview
* https://cloud.google.com/memorystore/docs/redis/about-manual-failover

* Memorystore for Redis provides a fully-managed service that is powered by the Redis in-memory data store to build application caches that provide sub-millisecond data access.
* What it's good for:
	* Caching
	* Gaming
	* Stream processing
		* Twitter feed or stream of data from IoT devices, etc.
* The two available data protection modes are:
	* limited-data-loss mode (default).
		* minimizes data loss by verifying that the difference in data between the primary and replica is below 30 MB before initiating the failover.
	* force-data-loss mode.
		* aggressively executes the failover.

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

# Business Jargon

Main sources: 
* https://cloud.google.com/architecture/dr-scenarios-planning-guide

## Service Level Agreement (SLA)

* An SLA is the <mark style="background: #FFF3A3A6;">entire agreement</mark> that specifies:
	* what service is to be provided, how it is supported, times, locations, costs, performance, penalties, and responsibilities of the parties involved.

## Service Level Objective (SLO)

* SLOs are specific, <mark style="background: #FFF3A3A6;">measurable characteristics of the SLA</mark>, such as:
	* availability, throughput, frequency, response time, or quality, [Recovery Time Objective (RTO)](#Recovery%20Time%20Objective%20(RTO)), [Recovery Point Objective (RPO)](#Recovery%20Point%20Objective%20(RPO)), etc.
* An SLA can contain many SLOs.

# Disaster Recovery (DR) Planning

Main sources: 
* https://cloud.google.com/architecture/dr-scenarios-planning-guide

## Business Impact Analysis (BIA)

- DR Planning begins with BIA ([source](https://cloud.google.com/architecture/dr-scenarios-planning-guide#:~:text=planning%20begins%20with%20a%20business%20impact%20analysis)).
- **BIA** stands for Business Impact Analysis.
- It identifies critical business functions and their dependencies.
- Assesses the impact of disruptions on these functions.
- <mark style="background: #FFB8EBA6;">Estimates potential losses</mark> (financial, operational, reputational).
- Helps prioritize recovery efforts and resource allocation.
- Informs [Disaster Recovery (DR)](#Disaster%20Recovery%20(DR)) and [Business Continuity Planning (BCP)](#Business%20Continuity%20Planning%20(BCP)).
- <mark style="background: #FFB8EBA6;">Aims to minimize downtime and maintain essential services</mark>.

BIA defines two metrics:

###  Recovery Time Objective (RTO)

* It's the maximum acceptable length of <mark style="background: #FFF3A3A6;">time that your application can be offline</mark>. 
* This value is usually defined as part of a larger [service level agreement (SLA)](https://wikipedia.org/wiki/Service-level_agreement).

### Recovery Point Objective (RPO)

* It's the maximum acceptable length of <mark style="background: #FFF3A3A6;">time during which data might be lost</mark> from your application due to a major incident. 
	* Side note: This metric describes only the length of time; it doesn't address the amount or quality of the data that's lost.
* This metric varies based on the ways that the data is used. 
	* For example, user data that's frequently modified could have an RPO of just a few minutes. 
	* In contrast, less critical, infrequently modified data could have an RPO of several hours. 


## Disaster Recovery (DR)

- **Purpose**: Focuses on restoring IT infrastructure and data after a disruption.
- **Scope**: Specifically addresses the technical aspects of recovery.
- **Objective**: Minimize downtime and data loss.
- **Components**: Includes data backups, recovery strategies, and failover mechanisms.
- **Timeframe**: Activated immediately after a disruption to restore normal operations.
- **Example**: Recovering data from backups after a server crash.

### DR Patterns

DR patterns are considered to be cold, warm, or hot. These patterns indicate how readily the system can recover when something goes wrong. An analogy might be what you would do if you were driving and punctured a car tire.

![3 photos of car flat-tire scenarios: no spare; a spare with tools; a run-flat tire.](https://cloud.google.com/static/architecture/images/dr-scenarios-cold-warm-hot-tire-analogy.png)

How you deal with a flat tire depends on how prepared you are:

- Cold: You have no spare tire, so you must call someone. Your trip stops until help arrives.
- Warm: You have a spare tire and a replacement kit, so you can get back on the road. However, you must stop your journey to repair the problem.
- Hot: You have run-flat tires. You might need to slow down a little, but there is no immediate impact on your journey (although you must eventually address the issue).

## Business Continuity Planning (BCP)

- **Purpose**: Ensures that essential business functions continue during and after a disruption.
- **Scope**: Encompasses the entire organization, including non-technical aspects.
- **Objective**: Maintain business operations and minimize impact.
- **Components**: Includes emergency response, communication plans, and alternative work arrangements.
- **Timeframe**: Encompasses proactive measures to sustain operations throughout the disruption.
- **Example**: Having remote work plans in place during a natural disaster.

