#pyspark 

[source 1](https://www.quora.com/What-is-the-difference-between-spark-and-pyspark), [source 2](https://www.youtube.com/watch?v=YEGnTKRHpu8&list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi&index=3), [source 3](https://medium.com/analytics-vidhya/solving-complex-big-data-problems-using-combinations-of-window-functions-deep-dive-in-pyspark-b1830eb00b7d), [source 4](https://yuanxu-li.github.io/technical/2018/06/10/reduce-and-fold-in-spark.html), [source 5](https://github.com/tirthajyoti/Spark-with-Python), [source 6](https://www.youtube.com/watch?v=rkoYVCJPX6o&list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi&index=6), [source 7](https://towardsdatascience.com/parallelize-pandas-dataframe-computations-w-spark-dataframe-bba4c924487c), [source 8](https://medium.zenika.com/a-comparison-between-rdd-dataframe-and-dataset-in-spark-from-a-developers-point-of-view-a539b5acf734), [source 9](https://igorshvab.medium.com/from-pandas-to-pyspark-dataframes-c25104879c29)

# PySpark vs Apache Spark

#pyspark  #apache-spark 

![](Media-Temp/Pasted%20image%2020240125102807.png)

([s1](https://www.quora.com/What-is-the-difference-between-spark-and-pyspark#:~:text=Let%E2%80%99s%20consider%20an%20example%20to%20make%20things%20easier%20to%20understand))

# PySpark vs Pandas

#pyspark  #pandas  #immutable  #lazy-execution  #eager-execution  #pyspark-transform

![](Media-Temp/Pasted%20image%2020240125103033.png)

([s2, 1:30](https://youtu.be/YEGnTKRHpu8?list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi&t=92))

Side note 1: "access is slower" in PySpark because it has to retrieve (i.e., access) the data from multiple nodes.

## PySpark DataFrame vs Pandas DataFrame

#pyspark  #pyspark-dataframe  #spark-dataframe  #pandas-dataframe  #pandas

![](Media-Temp/Pasted%20image%2020240126145130.png)

([s7](https://towardsdatascience.com/parallelize-pandas-dataframe-computations-w-spark-dataframe-bba4c924487c))

![](Media-Temp/Pasted%20image%2020240126145307.png)

([s8](https://medium.zenika.com/a-comparison-between-rdd-dataframe-and-dataset-in-spark-from-a-developers-point-of-view-a539b5acf734#705c))

<mark style="background: #ADCCFFA6;">Important</mark>: images comparing between the two DataFrame types can be found in ([s9](https://igorshvab.medium.com/from-pandas-to-pyspark-dataframes-c25104879c29#:~:text=Below%20is%20short%20cheatsheet)).

# PySpark Syntax

## Reduce and Fold

#pyspark  #reduce  #fold  #driver-program #flow-chart

Looking at the signatures of `reduce` and `fold` methods ([s4](https://yuanxu-li.github.io/technical/2018/06/10/reduce-and-fold-in-spark.html)):

```python
def reduce(self, op):
    # rest of the function's code
```

```python
def fold(self, zeroValue, op):
    # rest of the function's code
```

We find that both  accept a function `op`, but `fold` also takes a `zeroValue` to be used <mark style="background: #ABF7F7A6;">in the initial call of each partition</mark> <mark style="background: #ADCCFFA6;">and as the starting point in the driver program</mark> (explained in the `fold` code below).

Code example to illustrate the difference:

Initial code:

```python
rdd = sc.parallelize([2, 3, 4])
def add(x, y):
    print '{}+{}={}'.format(x, y, x+y)
    return x+y
```

Code example of `reduce`:

```python
rdd.reduce(add)
# 2+3=5
# 5+4=9
# 9
```

Flowchart explanation of `reduce` ([s4](https://yuanxu-li.github.io/technical/2018/06/10/reduce-and-fold-in-spark.html)):

![](Media-Temp/Pasted%20image%2020240125162942.png)

Code example of `fold`:

```python
rdd.fold(1, add)
# # no output for partition 1 since it is empty (however, it gives `1`)
# 1+3=4 # partition 2
# 1+2=3 # partition 3
# 1+4=5 # partition 4
# 1+1=2 # (acc.1) driver program's `zeroValue` added to partition 1's output
# 2+3=5 # (acc.2) accumulating (acc.1) to partition 2's output
# 5+4=9 # (acc.3) accumulating (acc.2) to partition 3's output
# 9+5=14 # (acc.4) accumulating (acc.3) to partition 4's output
# 14
```

Flowchart explanation of `fold` ([s4](https://yuanxu-li.github.io/technical/2018/06/10/reduce-and-fold-in-spark.html)):

![](Media-Temp/Pasted%20image%2020240125163021.png)

When to prefer `fold` over `reduce`: 

Case 1: <mark style="background: #ABF7F7A6;">Empty RDD</mark>: If you run reduce on an empty RDD, you will come across the following error ([s4](https://yuanxu-li.github.io/technical/2018/06/10/reduce-and-fold-in-spark.html#:~:text=fold%20is%20desired.-,Empty%20RDD,-If%20you%20run)):

```python
rdd = sc.parallelize([])
rdd.reduce(lambda x, y: x+y)
# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
#   File "/Users/yuanxu/spark-2.2.0-bin-hadoop2.7/python/pyspark/rdd.py", line 838, in reduce
#     raise ValueError("Can not reduce() empty RDD")
# ValueError: Can not reduce() empty RDD
```

But you can safely run `fold` on it with a correct `zeroValue`:
```python
rdd = sc.parallelize([])
rdd.fold(0, lambda x, y: x+y)
# 0
```

In this case, `zeroValue` is playing the role of a default value for an empty RDD.

Case 2: <mark style="background: #ABF7F7A6;">Bar raiser</mark>. Example:

```python
rdd = sc.parallelize([280, 250, 210, 285, 100])
rdd.fold(300, lambda x, y: max(x, y))
# 300
```

We've technically "raised the bar" of any RDD to produce a value of 300 or more.

Final note: I highly suggest checking out ([s4](https://yuanxu-li.github.io/technical/2018/06/10/reduce-and-fold-in-spark.html)) for more details; it's a relatively small article.

## Partitioning and Gloming


#pyspark  #partitioning  #rdd  #glom

To be honest ([s5](https://github.com/tirthajyoti/Spark-with-Python/blob/master/Partioning%20and%20Gloming.ipynb)) does a great job at explaining this section, so I'll just add code snippets that I <mark style="background: #CACFD9A6;">personally</mark> want to remember :\].

```python
# Creating SparkContext with 2 workers:
sc = SparkContext(master="local[2]")
A = sc.parallelize(range(1000000))
print(A.getNumPartitions())
# 2

# We can also set the number of partitions while creating the RDD with numSlices argument
A = sc.parallelize(range(1000000),numSlices=8)
print(A.getNumPartitions())
# 8
```

Regarding `Glom()`:
- In general, <mark style="background: #D2B3FFA6;">Spark does not allow the worker to refer to specific elements of the RDD</mark>.
- Keeps the language clean, but can be a major limitation.
* `glom()` transforms each partition into a tuple (immutable list) of elements. 
* It does this transformation by creating an RDD of tuples; One tuple per partition.
* <mark style="background: #ABF7F7A6;">Using glom, workers can refer to elements of the partition by index</mark> but you cannot assign values to the elements, the RDD is still immutable.

Example 1 ([s6, 17:20](https://youtu.be/rkoYVCJPX6o?list=PLlUZLZydkS7_8WnK8fMENmJFSfPwxw9Fi&t=1047)):

![](Media-Temp/Pasted%20image%2020240125184550.png)



## PySpark Window

#pyspark #window-specification


Essentially ([s3](https://medium.com/analytics-vidhya/solving-complex-big-data-problems-using-combinations-of-window-functions-deep-dive-in-pyspark-b1830eb00b7d)):

![](Media-Temp/Pasted%20image%2020240118135116.png)

suppose you have this PySpark code:

```python
from pyspark.sql.window import Window
from pyspark.sql.functions import sum

window_spec = Window.orderBy("Age")
df_with_cumsum = df.withColumn("CumulativeSalary", sum("Salary").over(window_spec))
```

Explanation:

In the context of PySpark, a <mark style="background: #FFF3A3A6;">window specification defines ***how to*** apply a function to a group of rows</mark> (i.e., a <mark style="background: #FFF3A3A6;">frame</mark>) in a DataFrame. 

A window specification is used with <mark style="background: #FFF3A3A6;">window functions, which are designed to perform calculations across sets of rows that are related to the current row.</mark> This is similar to how an aggregate function operates but with a focus on individual rows.

Here's an in-depth look at the components of a window specification within PySpark:

- **Partitioning**: The `partitionBy` method can be used to divide the data into partitions (or groups) based on the values of one or more columns. Each partition is treated as an independent group for window calculations. If `partitionBy` is not specified, the entire dataset is treated as a single partition.

- **Ordering**: The `orderBy` method is used to define the ordering of the rows within each partition. In the case of cumulative sum, as in your example, ordering determines the sequence in which the rows' values will be added together.

- <mark style="background: #FFF3A3A6;">Frame Specification: This defines which rows will be included in the frame for each row's calculation.</mark> The frame can be specified using methods like `rowsBetween` or `rangeBetween`. If not explicitly defined, the frame includes all rows in the partition from the start up to the current row, which is suitable for cumulative calculations.

In the code snippet above, the window specification is defined as `window_spec = Window.orderBy("Age")`. This means that the window function will operate over the rows ordered by the "Age" column, and since there is no `partitionBy` clause, the entire DataFrame is assumed to be a single partition.

The cumulative sum is then calculated using `sum("Salary").over(window_spec)`, which means <mark style="background: #CACFD9A6;">for each row in the DataFrame, PySpark will sum up the "Salary" values of all rows up to and including the current row, based on the order defined by "Age".</mark> This cumulative sum is then added to the DataFrame as a new column called "CumulativeSalary".

The concept of window specification in PySpark is essential for performing advanced analytics where you need to carry out calculations across groups of rows <mark style="background: #FF5582A6;">while still retaining the individual row-level detail</mark>.

