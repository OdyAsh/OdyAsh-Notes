# From Microsoft Learning Path

[M source](https://learn.microsoft.com/en-us/credentials/certifications/power-bi-data-analyst-associate/)

## Measures

1. Which statement about measures is correct? 

Measures store values in the data model.

Measures must be added to the data model to achieve summarization.

Measures can reference columns directly.
(<mark style="background: #FF5582A6;">not this option</mark>. Why? check [this](https://endjin.com/blog/2022/04/measures-vs-calculated-columns-in-dax#:~:text=When%20you%20write%20a%20calculated%20column%2C%20you,wrap%20the%20column%20in%20an%20aggregation%20function.))

-> Measures can reference other measures directly.
Measures can reference other measures. It's known as a compound measure.

2. Which DAX function can summarize <mark style="background: #D2B3FFA6;">a table</mark>? (self-note: in other words, the passed argument is a table, not a column) 

SUM

AVERAGE

-> COUNTROWS
The COUNTROWS function summarizes a table by returning the number of rows.


DISTINCTCOUNT

3. Which of the following statements describing similarity of measures and calculated columns in an Import model is true? 

-> They can achieve summarization of model data.
A calculated column can be summarized (implicit measure) and a measure always achieves summarization.


They store values in the data model.

They're evaluated during data refresh.

They can be created by using quick calculations.

## Optimize Performance

[M source](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/7-check)

1. What benefit do you get from analyzing the metadata?

-> <mark style="background: #D2B3FFA6;">The benefit of analyzing the metadata is that you can clearly identify data inconsistences with your dataset</mark>.

The benefit of analyzing the metadata is to get familiar with your data.

The benefit of analyzing the metadata is that you can clearly identify data inconsistences with your dataset.


2. What can be achieved by removing unnecessary rows and columns?

It is not necessary to delete unnecessary rows and columns and it is a good practice to keep all metadata intact.

-> Deleting unnecessary rows and columns will reduce a dataset size and it's good practice to load only necessary data into your data model.

Deleting unnecessary rows and columns can damage the structure of the data model.


3. Which of the following statements about relationships in Power BI Desktop is true?

Relationships can only be created between columns that contain the same data type.
Incorrect. This is not true as relationships can be created between columns that contain different data types in Power BI Desktop.

Relationships can only be created between tables that contain the same number of rows.

-> <mark style="background: #FF5582A6;">Relationships can be created between tables that contain different types of data</mark>.
Correct. A working relationship can be created as long as there is at least one common column between them.

## Effective User Experience

[M source](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-user-experience/11-check)

1. At the Contoso Skateboard Company, Sanjay is authoring a report that will be distributed to sales managers. The report contains some sensitive data that shouldn’t be exported. Which report design feature can Sanjay configure to ensure that data isn’t exported?

Bookmark

Drillthrough page

Page tooltip

-> Visual header
The answer is correct. <mark style="background: #D2B3FFA6;">By disabling the More options (…) icon, report consumers can’t export data.</mark>


2. At the Contoso Skateboard Company, Arun is building a report that will help sales managers explore sales revenue by different dimensions. Dimensions include Date, Product, Customer, Territory, and Marketing Campaign. The <mark style="background: #FFB8EBA6;">experience should involve a single data visual and provide guidance on which dimensions to explore</mark>. Which visual should Arun use?

-> <mark style="background: #FFB8EBA6;">Decomposition tree</mark>
The answer is correct. The Decomposition Tree visual helps report consumers visualize data across multiple dimensions. By using AI splits, the visual can recommend the next dimension to drill to.

Key influencers

Paginated reports

Q&A


## Power BI Analytic Capabilities

[M source](https://learn.microsoft.com/en-us/training/modules/perform-analytics-power-bi/11-check)

1. Where are time series charts located?

The filter pane is where all filters on visuals and pages are located.

-> <mark style="background: #D2B3FFA6;">Time series charts can be imported from AppSource</mark>.

The fields pane is where all charts are located.

