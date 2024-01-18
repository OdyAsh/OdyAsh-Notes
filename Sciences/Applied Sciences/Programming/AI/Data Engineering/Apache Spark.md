#spark

# Important Concepts

## Window

#pyspark #window-specification

[source 1](https://medium.com/analytics-vidhya/solving-complex-big-data-problems-using-combinations-of-window-functions-deep-dive-in-pyspark-b1830eb00b7d), 

Essentially ([s1](https://medium.com/analytics-vidhya/solving-complex-big-data-problems-using-combinations-of-window-functions-deep-dive-in-pyspark-b1830eb00b7d)):

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

