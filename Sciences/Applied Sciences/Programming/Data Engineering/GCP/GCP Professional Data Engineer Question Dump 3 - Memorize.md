

# Question #: 210  
Topic #: 1

[[All Professional Data Engineer Questions]](https://www.examtopics.com/exams/google/professional-data-engineer/)

You are designing a data mesh on Google Cloud with multiple distinct data engineering teams building data products. The typical data curation design pattern consists of landing files in Cloud Storage, transforming raw data in Cloud Storage and BigQuery datasets, and storing the final curated data product in BigQuery datasets. You need to configure Dataplex to ensure that each team can access only the assets needed to build their data products. You also need to ensure that teams can easily share the curated data product. What should you do?

·         A. 1. Create a single Dataplex virtual lake and create a single zone to contain landing, raw, and curated data.  
2. Provide each data engineering team access to the virtual lake.

·         B. 1. Create a single Dataplex virtual lake and create a single zone to contain landing, raw, and curated data.  
2. Build separate assets for each data product within the zone.  
3. Assign permissions to the data engineering teams at the zone level.

·         C. 1. Create a Dataplex virtual lake for each data product, and create a single zone to contain landing, raw, and curated data.  
2. Provide the data engineering teams with full access to the virtual lake assigned to their data product.

·         D. 1. Create a Dataplex virtual lake for each data product, and create multiple zones for landing, raw, and curated data.  
1. Provide the data engineering teams with full access to the virtual lake assigned to their data product.

Sol: D

# Question #: 211 
Topic #: 1

You are using BigQuery with a multi-region dataset that includes a table with the daily sales volumes. This table is updated multiple times per day. You need to protect your sales table in case of regional failures with a recovery point objective (RPO) of less than 24 hours, while keeping costs to a minimum. What should you do?

·         A. Schedule a daily export of the table to a Cloud Storage dual or multi-region bucket.

·         B. Schedule a daily copy of the dataset to a backup region.

·         C. Schedule a daily BigQuery snapshot of the table.

·         D. Modify ETL job to load the data into both the current and another backup region.

Sol: A (reason why not C is shown [here](https://www.examtopics.com/discussions/google/view/129858-exam-professional-data-engineer-topic-1-question-211/#:~:text=Selected%20Answer%3A%20A-,Why%20not%20C,-%3A%0A%0AA%20table%20snapshot)) ... However, I thought that since the table is updated multiple times a day ... therefore a daily snapshot isn't enough ... rather it should be multiple times per day, so I thought the answer would be D. ... but apparently it's not cost-effective ... so IDK ...

# Question #: 216  
Topic #: 1

You are developing an Apache Beam pipeline to extract data from a Cloud SQL instance by using JdbcIO. You have two projects running in Google Cloud. The pipeline will be deployed and executed on Dataflow in Project A. The Cloud SQL. instance is running in Project B and does not have a public IP address. After deploying the pipeline, you noticed that the pipeline failed to extract data from the Cloud SQL instance due to connection failure. You verified that VPC Service Controls and shared VPC are not in use in these projects. You want to resolve this error while ensuring that the data does not go through the public internet. What should you do?

·         A. Set up VPC Network Peering between Project A and Project B. Add a firewall rule to allow the peered subnet range to access all instances on the network.

·         B. Turn off the external IP addresses on the Dataflow worker. Enable Cloud NAT in Project A.

·         C. Add the external IP addresses of the Dataflow worker as authorized networks in the Cloud SQL instance.

·         D. Set up VPC Network Peering between Project A and Project B. Create a Compute Engine instance without external IP address in Project B on the peered subnet to serve as a proxy server to the Cloud SQL database.

Sol: A. (even though some answered with D. ... I'll just answer with A.)

# Question #: 218  
Topic #: 1

You have a Cloud SQL for PostgreSQL instance in Region1 with one read replica in Region2 and another read replica in Region3. An unexpected event in Region1                                            requires that you perform disaster recovery by promoting a read replica in Region2. You need to ensure that your application has the same database capacity available before you switch over the connections. What should you do?

·         A. Enable zonal high availability on the primary instance. Create a new read replica in a new region.

·         B. Create a cascading read replica from the existing read replica in Region3.

·         C. Create two new read replicas from the new primary instance, one in Region3 and one in a new region. <mark style="background: #FFF3A3A6;">(Ie., cross-region read replicas)</mark>

·         D. Create a new read replica in Region1, promote the new read replica to be the primary instance, and enable zonal high availability.

<mark style="background: #FF5582A6;">Sol: C.</mark>


