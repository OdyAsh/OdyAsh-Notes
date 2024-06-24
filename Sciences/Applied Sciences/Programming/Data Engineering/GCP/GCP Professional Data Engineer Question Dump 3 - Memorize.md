

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

