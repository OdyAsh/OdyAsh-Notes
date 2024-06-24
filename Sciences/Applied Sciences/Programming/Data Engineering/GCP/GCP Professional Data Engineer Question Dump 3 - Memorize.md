

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

