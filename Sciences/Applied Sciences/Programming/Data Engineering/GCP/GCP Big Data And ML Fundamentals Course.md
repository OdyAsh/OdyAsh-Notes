

# Google Cloud Basics

#google-cloud #gcp #google #data-engineering

Introductory note: Google cloud is the new name of Google Cloud Platform (GCP). ([source](https://cloud.google.com/blog/topics/developers-practitioners/introducing-new-homepage-google-cloud#:~:text=your%20side%20menu.-,Google%20Cloud%20Platform%20is%20now%20called%20Google%20Cloud,-To%20further%20simplify))

- **Cloud Computing:**
    - Decouples compute and storage for scalability.
    - Differs from desktop computing where processing is tied to storage disks.


- Google Cloud Services offer managed database and **storage services** which <mark style="background: #FFF3A3A6;">aim to reduce the time and effort needed to store data</mark>. Specifically:
	- **[Cloud Storage](#Cloud%20Storage)**
	- **Cloud Bigtable:**
	    - NoSQL database service.
	    - Ideal for large analytical and operational workloads.
	    - Handles massive amounts of data across many machines.
	- **Cloud SQL:**
	    - Fully managed relational database service.
	    - Supports MySQL, PostgreSQL, and SQL Server.
	    - Offers high performance and scalability.
	- **Cloud Spanner:**
	    - Fully managed, scalable, relational database service.
	    - Provides strong consistency and global distribution.
	    - Suited for mission-critical applications.
	- **Firestore:**
	    - NoSQL document database for mobile, web, and server development.
	    - Offers real-time synchronization and offline support.
	    - Scales automatically with usage.
	- **BigQuery:**
	    - Serverless, highly scalable, and cost-effective multi-cloud data warehouse (PaaS).
	    - Designed for business agility.
	    - Allows storage and analysis of unstructured data.
	    - Aims to simplify data storage.


- **Data Storage Types:**
    - **Unstructured Data:**
        - Suited to Cloud Storage.
        - BigQuery also supports unstructured data.
        - Cloud Storage:
            - For objects like files in any format.
            - Stored in buckets associated with a project.
	- **Structured Data** has two workload types:
		- **Transactional Workloads:**
			- Originates from Online Transaction Processing (OLTP) systems.
			- Used for fast data inserts and updates to build row-based records.
			- Requires standardized queries affecting few records.
			- **SQL Access:**
				- **Cloud SQL:** Best for local to regional scalability.
				- **Cloud Spanner:** Ideal for global database scalability.
			- **Non-SQL Access:**
				- **Firestore:** Transactional NoSQL, document-oriented database.
		- **Analytical Workloads:**
			- Originates from Online Analytical Processing (OLAP) systems.
			- Used for reading entire datasets.
			- Requires complex queries, like aggregations.
			- **SQL Access:**
				- **BigQuery:** Analyzes petabyte-scale datasets.
			- **Non-SQL Access:**
				- **Cloud Bigtable:** Scalable NoSQL for real-time, high-throughput applications with millisecond latency.


**Structured data** mapped to **storage services** diagram:
![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240111182352.png)

Another diagram showcasing this ([source](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/mjvAQ/store-all-sorts-of-data-types)):

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113183825.png)

# Transactional vs Analytical Operations

[source: 1:20](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/mjvAQ/store-all-sorts-of-data-types)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113183919.png)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113184134.png)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113184118.png)

# Fully-Managed vs Serverless Solutions

[source: 5:20](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/wQFOB/cloud-sql-as-a-relational-data-lake)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113185109.png)

- **Fully Managed Services:**
    - Provide access similar to on-premises installations.
    - Management tasks like backups and failover are automated by the service provider.
    - **Example Use Case:** Cloud SQL is fully managed, allowing direct SQL operations with automated maintenance.
- **Serverless Services:**
    - Operate as an API without the need to manage servers.
    - Users pay for the service usage, not for the underlying infrastructure.
    - **Example Use Cases:**
        - BigQuery for serverless data analysis without managing servers.
        - Pub/Sub for serverless asynchronous messaging.
        - Dataflow for serverless parallel data processing.
        - Cloud Storage for serverless object storage, abstracting away the hardware interaction.

[A great Google article](https://cloud.google.com/blog/topics/developers-practitioners/serverless-vs-fully-managed-whats-difference) summarizes the difference in these 2 sentences:
* Serverless: “I code my application or service <mark style="background: #FFB8EBA6;">and I don't care where it runs</mark>; just make sure my user is able to get to it when they try.”
* Fully-managed: “<mark style="background: #FFB8EBA6;">I care how and where my service runs</mark> because I have a specific type of service that needs more control over the underlying resources and… my application/team benefits from the extra controls.”

# Row vs Column Oriented Tables

[source: 2:00](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/wbnR5/introduction-to-bigquery)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240114072457.png)

- **Row-Oriented Tables:**
    - Efficient for making updates to data within fields.
    - Necessary for OLTP systems due to frequent updates.
    - **Use Case Example:** Traditional RDBMS for OLTP systems, where quick updates to records are essential.
    - **Slowness in Analytics:** Must read all fields in a row, and possibly extra rows, to find requested information, leading to slower analytics queries.
- **Column-Oriented Tables:**
    - Optimized for reading and appending data.
    - Efficient for analytics as they only read the columns required for a query.
    - **Use Case Example:** BigQuery for OLAP systems, where tables are immutable and designed for query speed.
    - **Slowness in OLTP Tasks:** Not optimized for frequent updates, which are common in OLTP systems.

# Cloud Storage

Google Cloud Storage:
- Stores **immutable objects** like files in any format.
- Objects are stored in buckets.
- Buckets are associated with projects.
- Projects can be grouped under an organization.
- Suitable for unstructured data.
- Used for website content, data archival, disaster recovery, etc.
- Considered a Data Lake
	- However, based on the needs of your project, you may not use cloud storage, and instead rely on BigQuery as both a Data Lake and a Data Warehouse ([source: 5:10](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/HwNEX/introduction-to-data-lakes))
- Essential for unstructured data in the cloud.
- Data persists beyond VM or cluster lifetimes.
- Cost-effective compared to compute.
- Object store with file system compatibility.
- Durable and strongly consistent.
- Global service with controlled privacy.
- Buckets and objects are the main entities.
- Unique global namespace for buckets.
- Data replication across regions or zones.
- Metadata used for access control and lifecycle management.

Now, you may have a variety of storage requirements for a multitude of use cases. Cloud Storage offers different classes for this:
- **Standard Storage:**
    - For frequently accessed data (“hot” data).
    - Ideal for data stored for short periods.
- **Nearline Storage:**
    - For infrequently accessed data (accessed less than once a month).
    - Suitable for backups and long-tail multimedia content.
- **Coldline Storage:**
    - For data accessed less than once a quarter.
    - Low-cost option for infrequently accessed data.
- **Archive Storage:**
    - Lowest-cost option for data accessed less than once a year.
    - Best for archiving, online backup, and disaster recovery.

Regarding how Cloud Storage simulates a file system when naming its objects ([source: 6:21](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/GKMgz/build-a-data-lake-using-cloud-storage)):
- Uses bucket and object names to simulate a file system.
- Object names can include forward slashes, resembling file paths.
- Moving objects simulates file directory changes but differs in performance.
- Avoid using sensitive information in global namespace bucket names.
- Accessible via file access methods and over the web with TLS encryption.

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113113631.png)

Other object management features:   
- Retention policies can be set for object expiration.
- Versioning tracks multiple versions of an object.
- Lifecycle management moves objects to Nearline or Coldline based on access frequency.

## Securing Data Lakes using Cloud Storage's IAM & ACLs

[source](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/zu5vW/secure-cloud-storage)

Cloud Storage implements two completely separate but overlapping methods of controlling access to objects. IAM Policy and access control lists.

IAM (Identity and Access Management):
- Standard across Google Cloud.
- Sets uniform access rules at the bucket level.
	- "Uniform access rules" means that every object in the bucket has the same access level, providing a simplified and uniform approach to access control.
- Provides roles like Reader, Writer, and Owner.
- Custom roles available for project-level access.

Access Control Lists (ACLs):
* Can be set at both bucket and individual object levels.
- Offers fine-grained access control.
- Allows specific permissions like read or write access.

<mark style="background: #FFB8EBA6;">In summary, use IAM for broad, bucket-level permissions and ACLs for detailed, object-level permissions.</mark>

## Data Encryption Options for Cloud Storage

[source: 2:00](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/zu5vW/secure-cloud-storage)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113182708.png)

As a custom step (before and after one of the above options), we can add a <mark style="background: #FFF3A3A6;">client-side encryption</mark>, where:
* Data encrypted by the users before upload.
- Users are responsible for decryption before use.

Here’s a guide on when to use GMEK, CMEK, and CSEK, along with example cases:

- **GMEK (Google Managed Encryption Keys):**
    - **Use Case:** When you prefer Google to manage the encryption process without additional effort on your part.
    - **Example:** A small company without dedicated security personnel can rely on GMEK for secure encryption.
- **CMEK (Customer Managed Encryption Keys):**
    - **Use Case:** When you want control over the encryption keys but still want to use Google’s infrastructure for key management.
    - [**Example:** A healthcare organization that needs to comply with HIPAA regulations may choose CMEK to manage keys within Google Cloud KMS](https://medium.com/google-cloud/data-encryption-techniques-in-google-cloud-gmek-cmek-csek-928d072a1e9d)[1](https://medium.com/google-cloud/data-encryption-techniques-in-google-cloud-gmek-cmek-csek-928d072a1e9d).
- **CSEK (Customer Supplied Encryption Keys):**
    - **Use Case:** When you need full control over the encryption keys and the responsibility of key management.
    - [**Example:** A financial institution with strict regulatory requirements might opt for CSEK to maintain complete control over their encryption keys](https://medium.com/google-cloud/data-encryption-techniques-in-google-cloud-gmek-cmek-csek-928d072a1e9d)[1](https://medium.com/google-cloud/data-encryption-techniques-in-google-cloud-gmek-cmek-csek-928d072a1e9d).

The choice between these encryption methods depends on your organization’s specific security, compliance, and operational needs. 

## Data Locking Options for Cloud Storage

[source: 3:45](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/zu5vW/secure-cloud-storage)

![|250](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113183023.png)

Data Locking options:
- **Object Lock:**
    - Places a hold on an individual object.
    - Suspends operations that could change or delete the object until the hold is released.
- **Bucket Lock:**
    - Applies a lock to an entire bucket.
    - Prevents any changes or deletions to the bucket’s contents until the lock is released.
- **Retention Policy Lock:**
    - Enforces a retention policy that prevents deletion of objects for a specified duration.
    - Remains in effect regardless of whether an object lock or bucket lock is enforced.

These locking mechanisms provide different levels of protection and control over data stored in Cloud Storage.

To summarize encryption vs locking:  <mark style="background: #FF5582A6;">Encryption prevents someone from understanding the data, locking prevents them from modifying the data</mark>.

# DataFlow and Apache Beam - Data Processing Workflows

[source 1](https://cloud.google.com/dataflow/docs/concepts/beam-programming-model)

* Apache Beam is an open source, unified model for defining both batch and streaming pipelines. 
	* This model simplifies the mechanics of large-scale data processing. 
	* Using one of the Apache Beam SDKs, you <mark style="background: #FFF3A3A6;">build a program that defines the pipeline</mark>. <mark style="background: #D2B3FFA6;">Then, you execute the pipeline on a specific platform such as Dataflow</mark>. 
	* This model lets you concentrate on the logical composition of your data processing job, rather than low-level details of distributed processing, such as coordinating individual workers, sharding datasets, and other such tasks. Dataflow fully manages these low-level details.
* The Cloud **Dataflow** SDK distribution **contains a subset of the Apache Beam ecosystem**. This subset includes the **necessary** components **to define your pipeline** and execute it locally and on the Cloud Dataflow service, such as ([source](https://stackoverflow.com/questions/44591782/google-cloud-dataflow-vs-apache-beam#:~:text=8-,Ended%20up%20finding,-answer%20in%20Google)):
	- The core SDK
	- DirectRunner and DataflowRunner
	- I/O components for other Google Cloud Platform services
- Google Dataflow performs the following main steps when a job is received:
	- Optimizes a pipeline model's execution graph to remove any inefficiencies.
	- Schedules distributed work to new workers and scales as needed.
	- Auto-heals any worker faults.
	- Automatically rebalances efforts to most efficiently use its workers.
	- Outputs data to produce a result.



# NoOps

A NoOps (No Operations) environment is one that doesn't require management from an operations team, as maintenance, monitoring, and scaling are automated. Check more details here: [NoOps](../../DevOps/DevOps.md#NoOps). 

Dataflow is [serverless](#Serverless%20Computing) and noops ([source](https://youtu.be/ISDsNP9yZG4?t=57)).


# Serverless Computing

Serverless computing is a cloud computing execution model where the cloud provider manages infrastructure tasks on behalf of the users, including tasks like resource provisioning, performance tuning, and ensuring pipeline reliability. 

Dataflow is serverless and [noops](#NoOps) ([source](https://youtu.be/ISDsNP9yZG4?t=57)).

Illustration of a serverless architecture ([source](https://martinfowler.com/bliki/Serverless.html)):

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240424203746.png)

Serverless vs PaaS ([source](https://www.cloudflare.com/learning/serverless/glossary/serverless-vs-paas/)): 
![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240424201231.png)

Another great explanation is provided [here](https://www.xtivia.com/blog/compare-faas-paas-saas/#:~:text=and%20many%20more.-,Serverless%20Computing,-In%20a%20nutshell).


# Cloud SQL

[source 1](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/26y0w/transactional-databases-versus-data-warehouses)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113101019.png)

Why not simply use Cloud SQL for reporting workflows? You can run SQL directly on the database, right?

Answer:

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113101200.png)

More about record-based storage and column-based storage in [this section](#Row%20vs%20Column%20Oriented%20Tables).

[source 2](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/wQFOB/cloud-sql-as-a-relational-data-lake)

Cloud SQL as a relational [Data Lake](#Data%20Lakes):

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113184359.png)

Cloud SQL replicas:

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113184758.png)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113184813.png)



# BigQuery

#bigquery

where BigQuery fits in the DE picture:

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240112175919.png)


* BigQuery is a fully managed data warehouse.
* BigQuery takes care of the underlying infrastructure, so you can focus on using SQL queries to answer business questions–without worrying about deployment, scalability, and security.
* BigQuery provides two services in one: storage plus analytics.
* **BigQuery is like a common staging area for data analytics workloads**. When your data is there, business analysts, BI developers, data scientists, and machine learning engineers can be granted access to your data for their own insights.

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113100136.png)

## BigQuery Implementation Overview

Customer-centric view of how BigQuery operates under the hood ([source](<[source](https://medium.com/google-cloud/the-12-components-of-google-bigquery-c2b49829a7c7)>)):

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115124933.png)


[source: 3:10](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/wbnR5/introduction-to-bigquery)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240114072721.png)

* Storage and Compute are separated.
	* Communication between them happens through Jupiter.

## How BigQuery Loads Data

[source: 3:00](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/DcYqO/load-data-into-bigquery)

Regarding files:
* BigQuery imports newline-delimited JSON, Avro, Parquet, and ORC files.
- CSV files are commonly used for imports from spreadsheets to BigQuery.

Importing via APIs:
* Data can be imported via API from various sources like Compute Engine, Kubernetes, App Engine, and Cloud Functions.
- API usage often requires recreating the data processing foundation.
	- "Data processing foundation" could refer to: writing custom code or using services like Dataproc or Dataflow, which are designed to handle data collection, transformation, and loading into BigQuery.
	- Therefore, <mark style="background: #FFB8EBA6;">API is mainly utilized with Dataproc or Dataflow</mark>.
- BigQuery Data Transfer Service offers connectors and pre-built load jobs for direct data loading from various services

### Data Transfer Service (DTS) for ELT

#data-transfer-service #data-backfill #connectors #pre-built #load-jobs

DTS:
- <mark style="background: #FFB8EBA6;">Used before the data warehouse stage to facilitate the transfer of data from the data lake (or directly from various sources) into the data warehouse</mark>, where it can be structured, queried, and analyzed. 
	- <mark style="background: #ABF7F7A6;">It’s an integral part of the Extract, Load, Transform (ELT) process</mark>, ensuring that data is properly prepared for use in the data warehouse.
	- Simplifies data warehouse system requirements by reducing the need for extensive coding by handling the initial stage of data warehousing: data transfer, cleaning, quality checks, transformation (ELT), and processing.
	- Supports [Cloud Storage](#Cloud%20Storage) use in the Extract, Load (EL) process.
- <mark style="background: #ABF7F7A6;">Provides connectors (E) and pre-built load jobs (LT)</mark> for direct data loading into BigQuery.
	-  A "connector" handles the initial communication and data extraction from the source service, which is then transformed and loaded into BigQuery using pre-built load jobs.
	- A “job” is an operation that BigQuery executes on your behalf to perform data-related tasks.
	- A "load job" is a task(s) of loading data from a source (Cloud Storage, CSV, etc.) into a [Data Warehouse (DW)](#Data%20Warehouse%20(DW)) (e.g., BigQuery).
	- A "pre-built data load job" is a predefined configuration or template that automates the process of loading data into a data warehouse or database.
- Offers <mark style="background: #FFB8EBA6;">automatic data backfill to address late arriving data and ensure complete datasets</mark>.
	- Data backfilling is the process of adding missing historical data to a dataset or system that previously lacked this information, or updating existing records with new data.
	- Example: A retail company’s database misses a day’s sales due to a system outage, and later, the missing transactions are added to ensure the sales records are complete and accurate.
- Enables repeated, periodic, scheduled imports from SaaS systems into BigQuery tables.
- Is a Google managed service, eliminating the need for operation, maintenance, or security overhead.

### User-Defined Functions (UDFs)

#user-defined-functions #javascript

What if your transformations went beyond what functions were currently available in BigQuery?: use UDFs.

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240114193629.png)

It is strongly suggested to use [standard SQL](https://www.reddit.com/r/bigquery/comments/178i3hh/why_do_many_websites_say_bigquery_uses_standard/), because BigQuery can optimize the execution of SQL much better than it can for JavaScript.

JavaScript in this case can contain other libraries.

Google has its own set of UDFs [here](https://github.com/GoogleCloudPlatform/bigquery-utils).

## How BigQuery Stores Data

#capacitor #columnar-storage #run-length-encoding #dictionary-encoding

Now ([source: 3:40](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/wbnR5/introduction-to-bigquery)), <mark style="background: #FFF3A3A6;">BigQuery uses "Capacitor" for storage optimization purposes</mark>, and is defined as:
- A columnar storage file format used in BigQuery.
- Enhances query speed by storing data in a compressed, efficient manner.

This "compressed manner" is essentially:
- **Run Length Encoding:**
    - Compresses repetitive values into a count and a single value.
    - Example: “Q1” appears 300 times, encoded as (Q1, 1, 300).
- **Dictionary Encoding:**
    - Maps distinct values to integers for efficient storage.
    - Example: Unique product IDs are assigned integer identifiers.

So basically:
- Capacitor uses both run length and dictionary encoding.
- Optimizes storage efficiency and query performance.

Diagram illustration:

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240114074302.png)

## Partitioned Tables

#partitioned-table #table-pruning #ingestion-time-partitioning #partially-sorted-table

[source 1](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/7dOQL/optimize-with-partitioning-and-clustering), [source 2](https://towardsdatascience.com/how-to-reduce-your-analytics-costs-with-bigquery-partitioned-tables-9298c274bf7d), [source 3](https://cloud.google.com/bigquery/docs/clustered-tables), [source 4](https://cloud.google.com/bigquery/docs/partitioned-tables), [source 5](https://cloud.google.com/bigquery/docs/partitioned-tables#:~:text=column%2Dpartitioned%20table.-,Ingestion%20time%20partitioning,are%20based%20on%20UTC%20time.), [source 6](https://hoffa.medium.com/bigquery-optimized-cluster-your-tables-65e2f684594b)

A partitioned table ([s2](https://towardsdatascience.com/how-to-reduce-your-analytics-costs-with-bigquery-partitioned-tables-9298c274bf7d)):

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115140649.png)

More about partitioning ([s4](https://cloud.google.com/bigquery/docs/partitioned-tables)):
* A partitioned table is divided into segments, called partitions.
* If a query uses a qualifying filter on the value of the partitioning column, <mark style="background: #FFF3A3A6;">BigQuery can scan the partitions that match the filter and skip the remaining partitions.</mark> 
	* This process is called [pruning](https://cloud.google.com/bigquery/docs/querying-partitioned-tables).
* In a partitioned table, data is stored in physical blocks, each of which holds one partition of data. 
* Each partitioned table maintains various metadata about the sort properties across all operations that modify it. 
	* The metadata lets BigQuery more accurately estimate a query cost before the query is run.
	* Examples of metadata: the partitioning key, partition ranges, the number of rows in each partition, and partition properties.
		* "Partition properties" include the rules and behaviors for how data is organized, stored, and accessed within each partition.

Methods of partitioning ([s1](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/7dOQL/optimize-with-partitioning-and-clustering)):

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115141855.png)

Note ([s5](https://cloud.google.com/bigquery/docs/partitioned-tables#:~:text=column%2Dpartitioned%20table.-,Ingestion%20time%20partitioning,are%20based%20on%20UTC%20time.)): When you create a table partitioned by "<mark style="background: #FFF3A3A6;">ingestion time</mark>", BigQuery automatically assigns rows to partitions based on the time when BigQuery ingests the data. This happens by creating a <mark style="background: #FFF3A3A6;">pseudocolumn</mark>, which is a virtual column used for partitioning, such as the `_PARTITIONTIME` column in BigQuery, which represents the ingestion time but <mark style="background: #ABF7F7A6;">isn’t physically stored in the table.</mark>

Implementation note: 

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115142800.png)

that's the only way BigQuery can quickly discard unnecessary partitions. It will also allow BigQuery use the table's metadata to <mark style="background: #ABF7F7A6;">more accurately estimate the query's cost before it is run.</mark>

Partitioning summary and benefits:

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115145004.png)

## Clustered Tables

#clustered-table #record-colocation

Same sources in [Partitioned Tables](#Partitioned%20Tables) section.

A clustered and partitioned table ([s3](https://cloud.google.com/bigquery/docs/clustered-tables)):

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115140835.png)

More about clustering:
* A clustered table in BigQuery is a table that **sorts data** into storage blocks of colocated records **based on the values in** user-defined **clustered columns**.
	* <mark style="background: #FFF3A3A6;">Record colocation</mark> refers to the practice of storing related records close together to improve query performance by minimizing the amount of data scanned.
* Over time as more and more operations modify a table, the degree to which the data is sorted begins to weaken and the table becomes only <mark style="background: #FFF3A3A6;">partially sorted</mark>. 
* In a partially sorted table, queries that use the clustering columns may need to scan more blocks compared to a table that is fully sorted.
* BigQuery periodically re-clusters your data:
  
  ![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115143652.png)
  
	* Previously, you can re-cluster the data in a partition table by running any redundant query on the partition column(s). For example:
	  
	  ![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115143602.png)

When to use clustering?:

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115145431.png)

Implementation note: If you don't have partitioned columns and you want the benefits of clustering, you can:
* create a fake underscore date column of type date and have all the values being null.
* use "ingestion time" method of partitioning
* This is just an implementation caveat within BigQuery; where it requires that a table has any column that can be partitioned in order for clustering mechanism to be applicable on that table.

Summary, benefits, and caveats of clustering:

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115145301.png)

## How BigQuery Run Queries

[source: 4:05](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/wbnR5/introduction-to-bigquery)

- **BigQuery Slot:**
    - Represents a unit of CPU, memory, and networking resources.
    - Includes supporting technologies and sub-services.
    - Specifications may vary during query execution.
        - I.e., some slots may have more CPU, etc., than others.


![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240114075144.png)

**Slot Allocation Factors:**
- **Default Quota:** Each account has a default limit of 2000 slots for on-demand querying.
- **Flat Rate Pricing:** Offers reserved slots for consistent billing.
- **Query Complexity:** Simple queries using fewer slots execute faster.
- **Concurrent Queries:** Slots are shared among all queries; excess demand leads to slower execution.
	- "Excess demand" example: If you've reserved 10,000 slots but you have 30 concurrent queries that together ask for 15,000 slots, the queries will not get all the slots they require.


![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240114075400.png)

## How BigQuery Structures Information

[source](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/b9AEc/get-started-with-bigquery)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240114181155.png)

## SQL Query's Lifecycle in BigQuery

[source: 1:10](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/b9AEc/get-started-with-bigquery) 

- **BigQuery Query and Storage Services:**
    - **Separate but Collaborative:** The query service is distinct from the storage service, yet they work in tandem.
    - **Native Tables:** Querying native tables within BigQuery’s public data project is common and highly efficient.
    - **Data Organization:** Both services internally organize data to facilitate efficient querying of large datasets.
- **Query Execution:**
    - **Federated Queries:** Is an option for querying of external data sources, like CSV files in Cloud Storage, without loading into BigQuery.
    - **Temporary Tables:** Query results are placed in temporary tables, visible in the UI for 24 hours, enabling cache usage for repeat queries.
    - **Cache and Charges:** Cached query results are free, while permanent destination tables incur storage charges.

Now, since querying and storage are separate, we can separate the costs as well:

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240114170434.png)

## Schema Design

#schema-design 

### Normalized vs Denormalized Tables

#table-normalization #table-denormalization

[source 1](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/X4GjI/schema-design), [source 2](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/VGWmR/nested-and-repeated-fields), [source 3](https://cloud.google.com/bigquery/docs/best-practices-performance-nested), [source 4](https://cloud.google.com/bigquery/docs/migration/schema-data-overview#denormalization), [source 5](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/23f9f/demo-nested-and-repeated-fields), [source 6](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/xbJOp/design-the-optimal-schema-for-bigquery)

Normalizing vs Denormalizing data ([s2](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/VGWmR/nested-and-repeated-fields)):

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115101301.png)

- **Normalization**:
    - Stores one fact in one place, typical for relational systems.
    - Reduces data redundancy and improves data integrity.
    - Often requires JOIN operations across multiple tables, which can be computationally intensive.
    - Suitable for systems where data consistency and accuracy are prioritized over query speed.
- **Denormalization**:
    - Combines all levels of granularity into a single large table.
    - Faster for querying as it avoids complex JOIN operations.
    - <mark style="background: #D2B3FFA6;">Can lead to data redundancy and requires careful handling of data at different granularity levels.</mark>
        - Must be cautious with aggregations to avoid issues like double counting due to duplicated keys (e.g., OrderID).
    - <mark style="background: #FF5582A6;">Nested and repeated fields can mitigate some drawbacks by preserving granular data within a single row.</mark>
        - <mark style="background: #FFF3A3A6;">A schema which uses nested and repeated fields is aligned with the BigQuery internal data representation.</mark> ([s4](https://cloud.google.com/bigquery/docs/migration/schema-data-overview#denormalization))
        - Internally, BigQuery organizes data using the [Dremel model](https://www.goldsborough.me/distributed-systems/2019/05/18/21-09-00-a_look_at_dremel/) and stores it in a columnar storage format called [Capacitor](https://cloud.google.com/blog/products/gcp/inside-capacitor-bigquerys-next-generation-columnar-storage-format).
    - Ideal for scenarios where query speed is critical and the data structure allows for efficient aggregation without redundancy issues.


More about denormalization ([s1](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/X4GjI/schema-design)):
- Flattened (i.e., denormalized) data consumes more storage but allows efficient <mark style="background: #FFF3A3A6;">parallel query processing</mark>.
- Denormalization is typically done before loading into BigQuery, but it can hinder performance when grouping by a one-to-many column.
	- Example: `OrderID` is a one-to-many column in the tables below:
	  
	  ![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115100405.png)
	  ![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115100123.png)
	  
	- Side note: while all “group by” operations involve aggregating multiple rows, the mention of “grouping by a one-to-many column” in the context of BigQuery is to emphasize the specific performance considerations that arise when dealing with denormalized data that originates from a relational pattern with one-to-many relationships.
- <mark style="background: #FF5582A6;">BigQuery supports nested and repeated fields to maintain some original data organization, aiding in efficient data retrieval.</mark>
	- continuation of the example above:
	  
	  ![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115100800.png)
	  
	- Nested fields, a type of repeated field, preserve relational data patterns while enabling efficient columnar processing.
	- Utilizing nested and repeated fields in BigQuery improves performance, especially with data from relational databases, so they are keys for integrating these databases with BigQuery.

Guidelines ([s6](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/xbJOp/design-the-optimal-schema-for-bigquery)):

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115213503.png)

### Nested Fields

#nested-fields  #googlesql #standard-sql

Same sources in [Normalized vs Denormalized Tables](#Normalized%20vs%20Denormalized%20Tables) section.

More on nested fields ([s2](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/VGWmR/nested-and-repeated-fields), [s3](https://cloud.google.com/bigquery/docs/best-practices-performance-nested)):
* Nesting data lets you represent foreign entities inline.
- Querying nested data uses "dot" syntax to reference leaf fields, which is similar to the syntax using a join.
- Nested data is represented as a `STRUCT` [type](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types#struct-type) in GoogleSQL.
	- Side-note: "GoogleSQL" is [Google's new name for "standard SQL"](https://www.reddit.com/r/bigquery/comments/178i3hh/why_do_many_websites_say_bigquery_uses_standard/).
* Example columns of nested fields: the highlighted columns which belong to the `event, pickup, destination` foreign entities (i.e., tables) in the table below:
  
  ![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115103543.png)

Nested fields Implementation notes: suppose you have a table with these columns ([s5](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/23f9f/demo-nested-and-repeated-fields)):

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115205851.png)

Side-note: Quick preview on repeated values:

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115205957.png)


Ok, but what if we want to access `input_script_bytes` column?

We can run this query to do so:

```sql
SELECT
  block_id,
  MAX(i.input_sequence_number) AS max_seq_number,
  COUNT(t.transaction_id) as num_transactions_in_block
FROM `bigquery-public-data.bitcoin_blockchain.blocks` AS b
-- Use the nested STRUCT within BLOCKS table for transactions instead of a separate JOIN
, b.transactions AS t
, t.inputs as i
GROUP BY block_id;

```

Notice how we write `b` for the `blocks` table, `b.transaction as t` to access the outer nested table, and `t.inputs as i` to access the inner nested table, then `i.input_sequence_number` to access the requested column. 

Query output:

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115212236.png)

Side note: but what does `,` refer to? it's a [CROSS JOIN](https://cloud.google.com/blog/topics/developers-practitioners/bigquery-explained-working-joins-nested-repeated-data#:~:text=join%20types%3A-,BigQuery%20join%20types,-Let%E2%80%99s%20look%20at) operation. Moreover, in the context of BigQuery, nested fields, and [repeated fields](#Repeated%20Fields), it is a <mark style="background: #FFF3A3A6;">correlated cross join operation</mark>, which only unpacks the elements associated with a single row ([source](https://www.cloudskillsboost.google/focuses/3696?parent=catalog#:~:text=only%20unpacks%20the%20elements%20associated%20with%20a%20single%20row.)). In other words, if we imagine 'transactions' as a nested table inside of 'blocks' table, then we need to join these 2 tables such that the rows match each other.


### Repeated Fields

#repeated-fields

Same sources in [Normalized vs Denormalized Tables](#Normalized%20vs%20Denormalized%20Tables) section.

Look at the purple rectangles in the [nested fields](#Nested%20Fields) section.

Now, let's look at the part we're interested in querying ([s5](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/23f9f/demo-nested-and-repeated-fields)):

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115212413.png)

To convert an `ARRAY` into a set of rows, also known as "flattening," use the [`UNNEST`](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax#unnest_operator) operator. `UNNEST` takes an `ARRAY` and returns a table with a single row for each element in the `ARRAY`. ([source](https://cloud.google.com/bigquery/docs/arrays#flattening_arrays)) 

Example of flattening a repeated field:

```sql
SELECT DISTINCT 
    block_id,
    TIMESTAMP_MILLIS(timestamp) AS timestamp,
    t.transaction_id,
    t.outputs.output_satoshis AS satoshi_value,
    t.outputs.output_satoshis * 0.00000001 AS btc_value
FROM `bigquery-public-data.bitcoin_blockchain.blocks` AS b
JOIN b.transactions AS t
JOIN UNNEST(t.outputs)
ORDER BY btc_value DESC
LIMIT 10;
```

Output of query:

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115212721.png)

Now, a common error that can be found due to forgetting to `UNNEST`:

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115212836.png)

Ok, but why didn't this error come up in the [Nested Fields](#Nested%20Fields) section's example? Because if you see the SQL of that example, you'll notice that we're grouping by `block_id`, so we don't need to display/map these repeated values to each row, instead we aggregate it (by getting the `MAX`, `COUNT`, etc.) and display the result.

### Nested and Repeated Fields

#nested-fields #repeated-fields 

summary:

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240115204009.png)




# Options to Build ML Models


![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113030917.png)


![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113033540.png)

Vertex AI is responsible for both AutoML and Custom Training.

# The Big Picture - Google's AI Stack

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113033239.png)

* Horizontal solutions usually apply to any industry that would like to solve the same problem.
* Vertical, or industry solutions, represent solutions that are relevant to specific industries.

# What Vertex AI Offers

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113033910.png)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113033918.png)


The backbone of MLOps and Vertex AI is a tool called **Vertex AI Pipelines**. It automates, **monitors**, and governs machine-learning systems by *orchestrating the workflow in a serverless manner*.

# Three Phases of an ML Workflow

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113035730.png)
# Options to Deploy an ML Model

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113034800.png)

* Endpoint example: making instant recommendations based on a user's browsing habits whenever they're online.
* Batch prediction example: sending out new ads every other week based on the user's recent purchasing behavior and what's currently popular on the market.
* Offline prediction example: when the model should be deployed in a specific environment off the cloud.


# The Complete DE Picture

[source](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/26y0w/transactional-databases-versus-data-warehouses)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113100841.png)

[source](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/mAOLi/recap)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113104334.png)

conceptual map of all GCP tools can be found in [this](https://googlecloudcheatsheet.withgoogle.com/) interactive website, and [this](https://github.com/priyankavergadia/google-cloud-4-words) GitHub repo.


## Google Tools for a Data Processing Workloads

[source: 6:10](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/HwNEX/introduction-to-data-lakes)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113110529.png)

# Partners Who Rely on DE

[source](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/jRmtb/partner-effectively-with-other-data-teams)

ML Engineers:
* Will ask DEs questions like:
	* How long does it take for a transaction to make it from raw data all the way into the data warehouse? 
		* They're asking this because any data that they train their models on must also be available at prediction time as well. 
		* If there is a long delay in collecting and aggregating the raw data, it will impact the ML team's ability to create useful models.
	* How difficult it would be to add more columns or rows of data into certain datasets? 
		* Again, the ML team relies on teasing out relationships between the columns of data and having a rich history to train models on. 
* The DE will earn the trust of their partner ML teams by making the datasets easily **discoverable, documented, and available** to ML teams to experiment on quickly.


Data Analysts (DAs):
* Will ask DEs questions like:
	* What data is available in your warehouse for us to access?
	* Our dashboards are slow, can you help us re-engineer our BI tables for better performance?
* One of the Google Cloud products that <mark style="background: #FFF3A3A6;">helps manage the performance of dashboards is BigQuery BI Engine</mark>. 
	* **Bi Engine** is a fast in-memory analysis service that is built directly into BigQuery and available to speed up your BI applications.


Other DEs:
* Will ask questions and requests like:
	* How can we ensure both dataset uptime & performance?
	* We’re noticing high demand for your datasets – be sure your warehouse can scale for many users.
* How can you monitor and scale the health of your entire data ecosystem? 
	* Use the built-in <mark style="background: #FFF3A3A6;">Cloud monitoring</mark> of all resources on Google Cloud. 
	* Since Google Cloud Storage and BigQuery are resources, you can set up alerts and notifications for metrics like query count so you can better track usage and performance. 
	* Cloud monitoring can 
		* track spendings of all the different resources used.
		* Provide insights on our organization's billing trends.
		* Use the **Cloud audit logs** to view actual query job information, in order to see granular-level details about which queries were executed and by whom. 
			* This is useful if you have sensitive datasets that you need to monitor closely

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113102807.png)

# DE Data Governance

[source](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/J8ITW/manage-data-access-and-governance)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113102950.png)

One solution for data governance is the Cloud <mark style="background: #FFF3A3A6;">Data Catalog</mark> and the Data Loss Prevention <mark style="background: #FFF3A3A6;">(DLP) API</mark>:

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113103256.png)

Note: DLP makes sure that users do not send sensitive or critical information outside the corporate network. This is why it's also called Data Leakage Prevention.

# Cloud Composer (using Apache Airflow)

[source](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/GHhrf/build-production-ready-pipelines)

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113103901.png)

* *A Cloud Composer job* can run every night/hour/etc. and kick-off your entire pipeline from raw data to the data lake and into the data warehouse for you.
* The power of this tool comes from the fact that <mark style="background: #D2B3FFA6;">Google Cloud Big Data products and services have API endpoints that you can call</mark>.


# Data Lakes

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240113105311.png)


# Data Warehouse (DW)

[source](https://www.coursera.org/learn/data-lakes-data-warehouses-gcp/lecture/PgM01/the-modern-data-warehouse)

The keyword difference between DW and Data Lakes: "Consolidate";

![](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240114070930.png)

Primary concerns:
* Data Lakes: Storing data
* DWs: Querying data

modern DW requirements:
![|400](Attachments%20-%20GCP%20Big%20Data%20And%20ML%20Fundamentals%20Course/Pasted%20image%2020240114071038.png)



# Civil Engineering Analogy to DE

source:

A Civil Engineering analogy and its mapping to DE:
- **Raw Materials (Data Sources):**
    - Gathering steel, concrete, etc., is like sourcing data into a data lake.
- **Material Processing (Data Transformation):**
    - Cutting wood, shaping metal is akin to transforming raw data for use.
- **Construction Workers (Data Pipelines):**
    - Workers who process materials are like virtual machines processing data.
- **Skyscraper (End-Goal):**
    - The completed building represents the final data product, like insights or models.
- **Site Manager (Orchestration Layer):**
    - Directs workflow, like Apache Airflow managing data pipeline tasks.

# Data Load Methods - EL, ELT, ETL

- **EL (Extract and Load):**
    - **Definition:** Importing data as is into a system.
    - **Usage:** When no transformation is needed.
    - **Example:** Importing Avro files directly into BigQuery.
- **ELT (Extract, Load, and Transform):**
    - **Definition:** Loading raw data into the target and then transforming it.
    - **Usage:** When minimal transformation is needed.
    - **Example:** Loading data into BigQuery and using SQL to transform and create a new table.
- **ETL (Extract, Transform, and Load):**
    - **Definition:** Transforming data in an intermediate service (e.g., Google Cloud's DataFlow) before loading.
    - **Usage:** When significant transformation is essential or reduces data size.
    - **Example:** Converting binary proprietary format data in a data pipeline before loading into BigQuery.
