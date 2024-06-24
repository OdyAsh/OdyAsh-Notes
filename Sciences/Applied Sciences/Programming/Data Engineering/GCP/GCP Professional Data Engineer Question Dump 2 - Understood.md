
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

·         C. Increase one replica to Redis instance in production environment. Initiate a manual failover by using the force-data-loss data protection mode.

·         D. Initiate a manual failover by using the limited-data-loss data protection mode to the Memorystore for Redis instance in the production environment.

Sol: B

