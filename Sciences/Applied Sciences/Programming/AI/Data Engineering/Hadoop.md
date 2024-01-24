
#hadoop

[source 1](https://www.edureka.co/blog/hadoop-yarn-tutorial/), [source 2](https://youtu.be/AGgyf9bO_8M?list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi), [source 3](https://mydataexperiments.com/2017/04/11/hadoop-ecosystem-a-quick-glance/)

TOC of s1:
- [Why YARN?](https://www.edureka.co/blog/hadoop-yarn-tutorial/#Why%20YARN?)
- [Introduction to Hadoop YARN](https://www.edureka.co/blog/hadoop-yarn-tutorial/#Introduction%20to%20Hadoop%20YARN)
- [Components of YARN](https://www.edureka.co/blog/hadoop-yarn-tutorial/#Components%20of%20YARN)
- [Application Submission in YARN](https://www.edureka.co/blog/hadoop-yarn-tutorial/#Application%20Submission%20in%20YARN)
- [Application Workflow in Hadoop YARN](https://www.edureka.co/blog/hadoop-yarn-tutorial/#Application%20Workflow)

# Hadoop Ecosystem

#hadoop-ecosystem

Hadoop's ecosystem ([s3](https://mydataexperiments.com/2017/04/11/hadoop-ecosystem-a-quick-glance/), and [s2, 12:20](https://youtu.be/AGgyf9bO_8M?list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi&t=740)):

![](Media-Temp/Pasted%20image%2020240124163932.png)


# Hadoop Core Components (V1.0 vs V2.0)

#distributed-file-storage  #hdfs  #resource-management  #yarn  #mapreduce

![](Media-Temp/Pasted%20image%2020240124121658.png)

([s1](https://www.edureka.co/blog/hadoop-yarn-tutorial/#:~:text=million%20per%20month.-,Introduction%20to%20Hadoop%20YARN,-Now%20that%20I))


## MapReduce

#mapreduce  #apache-spark  

Note: [Apache Spark](Apache%20Spark.md) can be used instead of Hadoop's MapReduce. Check the section for more details.

## YARN

#yarn #job-tracker  #master-node  #name-node  #task-tracker  #slave-node #mapreduce   #resource-management  #job-scheduling

YARN stands for <mark style="background: #FFF3A3A6;">Yet Another Resource Negotiator</mark>.

Why YARN? (s2):
* In Hadoop version 1.0 which is also referred to as MRV1.
* MapReduce performed both processing and resource management functions.
* This design resulted in <mark style="background: #FFB8EBA6;">scalability bottleneck due to a single Job Tracker</mark>.
	* A <mark style="background: #FFF3A3A6;">Job tracker</mark> (i.e., <mark style="background: #FFF3A3A6;">master node</mark> or <mark style="background: #FFF3A3A6;">name node</mark>) allocates resources to <mark style="background: #FFF3A3A6;">slave nodes</mark>, and schedules/monitors processing jobs.
		* These slave nodes are called <mark style="background: #FFF3A3A6;">Task Trackers</mark>.

YARN was introduced in Hadoop version 2.0 in the year 2012 by Yahoo and Hortonworks.

So instead of MapReduce, <mark style="background: #FFB86CA6;">YARN is now responsible of resource management and job scheduling</mark>.


