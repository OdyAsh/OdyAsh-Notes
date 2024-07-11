

# Question #: 206 - DF, BQ
Topic #: 1


You need ads data to serve AI models and historical data for analytics. Longtail and outlier data points need to be identified. You want to cleanse the data in near-real time before running it through AI models. What should you do?

·         A. Use Cloud Storage as a data warehouse, shell scripts for processing, and BigQuery to create views for desired datasets.

·         B. Use Dataflow to identify longtail and outlier data points programmatically, with BigQuery as a sink.

·         C. Use BigQuery to ingest, prepare, and then analyze the data, and then run queries to create views.

·         D. Use Cloud Composer to identify longtail and outlier data points, and then output a usable dataset to BigQuery.

Sol: B.


# Question #: 207  - SQL, Clustering, Partitioning
Topic #: 1

[[All Professional Data Engineer Questions]](https://www.examtopics.com/exams/google/professional-data-engineer/)

You are collecting IoT sensor data from millions of devices across the world and storing the data in BigQuery. Your access pattern is based on recent data, filtered by location_id and device_version with the following query:  
  
  ![](Media-Temp/Pasted%20image%2020240623174837.png)
  
You want to optimize your queries for cost and performance. How should you structure your data?

·         A. Partition table data by create_date, location_id, and device_version.

·         B. Partition table data by create_date, cluster table data by location_id, and device_version.

·         C. Cluster table data by create_date, location_id, and device_version.

·         D. Cluster table data by create_date, partition by location_id, and device_version.

Sol: B


# Question #: 208 - Pub/sub, BQ, BT
Topic #: 1

A live TV show asks viewers to cast votes using their mobile phones. The event generates a large volume of data during a 3-minute period. You are in charge of the "Voting infrastructure" and must ensure that the platform can handle the load and that all votes are processed. You must display partial results while voting is open. After voting closes, you need to count the votes exactly once while optimizing cost. What should you do?  
  

·         A. Create a Memorystore instance with a high availability (HA) configuration.

·         B. Create a Cloud SQL for PostgreSQL database with high availability (HA) configuration and multiple read replicas.

·         C. Write votes to a Pub/Sub topic and have Cloud Functions subscribe to it and write votes to BigQuery.

·         D. Write votes to a Pub/Sub topic and load into both Bigtable and BigQuery via a Dataflow pipeline. Query Bigtable for real-time results and BigQuery for later analysis. Shut down the Bigtable instance when voting concludes.

Sol: D


# Question #: 209  - Clustering, Partitioning
Topic #: 1

[[All Professional Data Engineer Questions]](https://www.examtopics.com/exams/google/professional-data-engineer/)

A shipping company has live package-tracking data that is sent to an Apache Kafka stream in real time. This is then loaded into BigQuery. Analysts in your company want to query the tracking data in BigQuery to analyze geospatial trends in the lifecycle of a package. The table was originally created with ingest-date partitioning. Over time, the query processing time has increased. You need to copy all the data to a new clustered table. What should you do?

·         A. Re-create the table using data partitioning on the package delivery date.

·         B. Implement clustering in BigQuery on the package-tracking ID column.

·         C. Implement clustering in BigQuery on the ingest date column.

·         D. Tier older data onto Cloud Storage files and create a BigQuery table using Cloud Storage as an external data source.

Sol: B


# Question #: 213
Topic #: 1

Your company's customer_order table in BigQuery stores the order history for 10 million customers, with a table size of 10 PB. You need to create a dashboard for the support team to view the order history. The dashboard has two filters, country_name and username. Both are string data types in the BigQuery table. When a filter is applied, the dashboard fetches the order history from the table and displays the query results. However, the dashboard is slow to show the results when applying the filters to the following query:  
  
  
  
How should you redesign the BigQuery table to support faster access?

·         A. Cluster the table by country and username fields.

·         B. Cluster the table by country field, and partition by username field.

·         C. Partition the table by country and username fields.

·         D. Partition the table by _PARTITIONTIME.

# Question #: 219  
Topic #: 1

You orchestrate ETL pipelines by using Cloud Composer. One of the tasks in the Apache Airflow directed acyclic graph (DAG) relies on a third-party service. You want to be notified when the task does not succeed. What should you do?

·         A. Assign a function with notification logic to the on_retry_callback parameter for the operator responsible for the task at risk.

·         B. Configure a Cloud Monitoring alert on the sla_missed metric associated with the task at risk to trigger a notification.

·         C. Assign a function with notification logic to the on_failure_callback parameter tor the operator responsible for the task at risk.

·         D. Assign a function with notification logic to the sla_miss_callback parameter for the operator responsible for the task at risk.

Sol: C.

# Question #: 220  
Topic #: 1

You are migrating your on-premises data warehouse to BigQuery. One of the upstream data sources resides on a MySQL. database that runs in your on-premises data center with no public IP addresses. You want to ensure that the data ingestion into BigQuery is done securely and does not go through the public internet. What should you do?

·         A. Update your existing on-premises ETL tool to write to BigQuery by using the BigQuery Open Database Connectivity (ODBC) driver. Set up the proxy parameter in the simba.googlebigqueryodbc.ini file to point to your data center’s NAT gateway.

·         B. Use <mark style="background: #FFF3A3A6;">Datastream (a Change Data Capture, CDC service)</mark> to replicate data from your on-premises MySQL database to BigQuery. Set up Cloud Interconnect between your on-premises data center and Google Cloud. Use Private connectivity as the connectivity method and allocate an IP address range within your VPC network to the Datastream connectivity configuration. Use Server-only as the encryption type when setting up the connection profile in Datastream.

·         C. Use Datastream to replicate data from your on-premises MySQL database to BigQuery. Use Forward-SSH tunnel as the connectivity method to establish a secure tunnel between Datastream and your on-premises MySQL database through a tunnel server in your on-premises data center. Use None as the encryption type when setting up the connection profile in Datastream.

·         D. Use Datastream to replicate data from your on-premises MySQL database to BigQuery. Gather Datastream public IP addresses of the Google Cloud region that will be used to set up the stream. Add those IP addresses to the firewall allowlist of your on-premises data center. Use IP Allowlisting as the connectivity method and Server-only as the encryption type when setting up the connection profile in Datastream.

Sol: B.

# Question #: 221  
Topic #: 1

You store and analyze your relational data in BigQuery on Google Cloud with all data that resides in US regions. You also have a variety of object stores across Microsoft Azure and Amazon Web Services (AWS), also in US regions. You want to query all your data in BigQuery daily with as little movement of data as possible. What should you do?

·         A. Use BigQuery Data Transfer Service to load files from Azure and AWS into BigQuery.

·         B. Create a Dataflow pipeline to ingest files from Azure and AWS to BigQuery.

·         C. Load files from AWS and Azure to Cloud Storage with Cloud Shell gsutil rsync arguments.

·         D. Use the <mark style="background: #FFF3A3A6;">BigQuery Omni functionality</mark> and BigLake tables to query files in Azure and AWS.

Sol: D.

# Question #: 222  
Topic #: 1

You have a variety of files in Cloud Storage that your data science team wants to use in their models. Currently, users do not have a method to explore, cleanse, and validate the data in Cloud Storage. You are looking for a low code solution that can be used by your data science team to quickly cleanse and explore data within Cloud Storage. What should you do?

·         A. Provide the data science team access to Dataflow to create a pipeline to prepare and validate the raw data and load data into BigQuery for data exploration.

·         B. Create an external table in BigQuery and use SQL to transform the data as necessary. Provide the data science team access to the external tables to explore the raw data.

·         C. Load the data into BigQuery and use SQL to transform the data as necessary. Provide the data science team access to staging tables to explore the raw data.

·         D. Provide the data science team access to Dataprep to prepare, validate, and explore the data within Cloud Storage.

Sol: D.

# Question #: 223  
Topic #: 1

You are building an ELT solution in BigQuery by using Dataform. You need to perform uniqueness and null value checks on your final tables. What should you do to efficiently integrate these checks into your pipeline?

·         A. Build BigQuery user-defined functions (UDFs).

·         B. Create Dataplex data quality tasks.

·         C. Build <mark style="background: #FFF3A3A6;">Dataform assertions</mark> into your code.

·         D. Write a Spark-based stored procedure.

Sol: C.

# Question #: 224  
Topic #: 1

A web server sends click events to a Pub/Sub topic as messages. The web server includes an eventTimestamp attribute in the messages, which is the time when the click occurred. You have a Dataflow streaming job that reads from this Pub/Sub topic through a subscription, applies some transformations, and writes the result to another Pub/Sub topic for use by the advertising department. The advertising department needs to receive each message within 30 seconds of the corresponding click occurrence, but they report receiving the messages late. Your Dataflow job's system lag is about 5 seconds, and the data freshness is about 40 seconds. Inspecting a few messages show no more than 1 second lag between their eventTimestamp and publishTime. What is the problem and what should you do?

·         A. The advertising department is causing delays when consuming the messages. Work with the advertising department to fix this.

·         B. Messages in your Dataflow job are taking more than 30 seconds to process. Optimize your job or increase the number of workers to fix this.

·         C. Messages in your Dataflow job are processed in less than 30 seconds, but your job cannot keep up with the backlog in the Pub/Sub subscription. Optimize your job or increase the number of workers to fix this.

·         D. The web server is not pushing messages fast enough to Pub/Sub. Work with the web server team to fix this.

Sol: C.

# Question #: 226  
Topic #: 1

Your organization has two Google Cloud projects, project A and project B. In project A, you have a Pub/Sub topic that receives data from confidential sources. Only the resources in project A should be able to access the data in that topic. You want to ensure that project B and any future project cannot access data in the project A topic. What should you do?

·         A. Add firewall rules in project A so only traffic from the VPC in project A is permitted.

·         B. Configure VPC Service Controls in the organization with a perimeter around project A.

·         C. Use Identity and Access Management conditions to ensure that only users and service accounts in project A. can access resources in project A.

·         D. Configure VPC Service Controls in the organization with a perimeter around the VPC of project A.

Sol: <mark style="background: #FF5582A6;">C. or B.</mark> , but I believe C. (full discussion: [here](https://www.examtopics.com/discussions/google/view/129873-exam-professional-data-engineer-topic-1-question-226/))

# Question #: 227  
Topic #: 1

You stream order data by using a Dataflow pipeline, and write the aggregated result to Memorystore. You provisioned a Memorystore for Redis instance with Basic Tier, 4 GB capacity, which is used by 40 clients for read-only access. You are expecting the number of read-only clients to increase significantly to a few hundred and you need to be able to support the demand. You want to ensure that read and write access availability is not impacted, and any changes you make can be deployed quickly. What should you do?

·         A. Create a new Memorystore for Redis instance with Standard Tier. Set capacity to 4 GB and read replica to No read replicas (high availability only). Delete the old instance.

·         B. Create a new Memorystore for Redis instance with Standard Tier. Set capacity to 5 GB and create multiple read replicas. Delete the old instance.

·         C. Create a new Memorystore for Memcached instance. Set a minimum of three nodes, and memory per node to 4 GB. Modify the Dataflow pipeline and all clients to use the Memcached instance. Delete the old instance.

·         D. Create multiple new Memorystore for Redis instances with Basic Tier (4 GB capacity). Modify the Dataflow pipeline and new clients to use all instances.

Sol: B.

# Question #: 230  
Topic #: 1

You need to modernize your existing on-premises data strategy. Your organization currently uses:  
• Apache Hadoop clusters for processing multiple large data sets, including on-premises Hadoop Distributed File System (HDFS) for data replication.  
• Apache Airflow to orchestrate hundreds of ETL pipelines with thousands of job steps.  
  
You need to set up a new architecture in Google Cloud that can handle your Hadoop workloads and requires minimal changes to your existing orchestration processes. What should you do?

·         A. Use Bigtable for your large workloads, with connections to Cloud Storage to handle any HDFS use cases. Orchestrate your pipelines with Cloud Composer.

·         B. Use Dataproc to migrate Hadoop clusters to Google Cloud, and Cloud Storage to handle any HDFS use cases. Orchestrate your pipelines with Cloud Composer.

·         C. Use Dataproc to migrate Hadoop clusters to Google Cloud, and Cloud Storage to handle any HDFS use cases. Convert your ETL pipelines to Dataflow.

·         D. Use Dataproc to migrate your Hadoop clusters to Google Cloud, and Cloud Storage to handle any HDFS use cases. Use Cloud Data Fusion to visually design and deploy your ETL pipelines.

Sol: B.

# Question #: 232  
Topic #: 1

You are on the data governance team and are implementing security requirements to deploy resources. You need to ensure that resources are limited to only the europe-west3 region. You want to follow Google-recommended practices.  

What should you do?

·         A. Set the constraints/gcp.resourceLocations organization policy constraint to in:europe-west3-locations.

·         B. Deploy resources with Terraform and implement a variable validation rule to ensure that the region is set to the europe-west3 region for all resources.

·         C. Set the constraints/gcp.resourceLocations organization policy constraint to in:eu-locations.

·         D. Create a Cloud Function to monitor all resources created and automatically destroy the ones created outside the europe-west3 region.

Sol: A.

