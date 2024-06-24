

# Question #: 206 - DF, BQ
Topic #: 1

[[All Professional Data Engineer Questions]](https://www.examtopics.com/exams/google/professional-data-engineer/)

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

