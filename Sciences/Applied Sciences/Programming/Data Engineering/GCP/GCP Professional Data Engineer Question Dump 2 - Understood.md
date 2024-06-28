
# Question #: 212 
Topic #: 1

You are troubleshooting your Dataflow pipeline that processes data from Cloud Storage to BigQuery. You have discovered that the Dataflow worker nodes cannot communicate with one another. Your networking team relies on Google Cloud network tags to define firewall rules. You need to identify the issue while following Google-recommended networking security practices. What should you do?

·         A. Determine whether your Dataflow pipeline has a custom network tag set.

·         B. Determine whether there is a firewall rule set to allow traffic on TCP ports 12345 and 12346 for the Dataflow network tag.

·         C. Determine whether there is a firewall rule set to allow traffic on TCP ports 12345 and 12346 on the subnet used by Dataflow workers.

·         D. Determine whether your Dataflow pipeline is deployed with the external IP address option enabled.

Sol: B

Explanation: even though other answers could work, we chose B, as since we're assuming Google's best practices are being followed, then the workers will have `dataflow` network tag attached to them, so B is more relevant.


# Question #: 214  
Topic #: 1

You have a Standard Tier Memorystore for Redis instance deployed in a production environment. You need to simulate a Redis instance failover in the most accurate disaster recovery situation, and ensure that the failover has no impact on production data. What should you do?

·         A. Create a Standard Tier Memorystore for Redis instance in the development environment. Initiate a manual failover by using the limited-data-loss data protection mode.

·         B. Create a Standard Tier Memorystore for Redis instance in a development environment. Initiate a manual failover by using the force-data-loss data protection mode.

# Question #: 215

You are administering a BigQuery dataset that uses a customer-managed encryption key (CMEK). You need to share the dataset with a partner organization that does not have access to your CMEK. What should you do?

·         A. Provide the partner organization a copy of your CMEKs to decrypt the data.

·         B. Export the tables to parquet files to a Cloud Storage bucket and grant the storageinsights.viewer role on the bucket to the partner organization.

·         C. Copy the tables you need to share to a dataset without CMEKs. Create an Analytics Hub listing for this dataset.

·         D. Create an authorized view that contains the CMEK to decrypt the data when accessed.

Sol: C.

·         C. Increase one replica to Redis instance in production environment. Initiate a manual failover by using the force-data-loss data protection mode.

·         D. Initiate a manual failover by using the limited-data-loss data protection mode to the Memorystore for Redis instance in the production environment.

Sol: B

# Question #: 217  
Topic #: 1

You have a BigQuery table that contains customer data, including sensitive information such as names and addresses. You need to share the customer data with your data analytics and consumer support teams securely. The data analytics team needs to access the data of all the customers, but must not be able to access the sensitive data. The consumer support team needs access to all data columns, but must not be able to access customers that no longer have active contracts. You enforced these requirements by using an authorized dataset and policy tags. After implementing these steps, the data analytics team reports that they still have access to the sensitive columns. You need to ensure that the data analytics team does not have access to restricted data. What should you do? (Choose two.)

·         A. Create two separate authorized datasets; one for the data analytics team and another for the consumer support team.

·         B. Ensure that the data analytics team members do not have the Data Catalog Fine-Grained Reader role for the policy tags.

·         C. Replace the authorized dataset with an authorized view. Use row-level security and apply filter_expression to limit data access.

·         D. Remove the bigquery.dataViewer role from the data analytics team on the authorized datasets.

·         E. Enforce access control in the policy tag taxonomy.

Sol: B., E. (Even though some say A., B.)


