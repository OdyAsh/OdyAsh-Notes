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

## Power BI Paginated Reports

[M source](https://learn.microsoft.com/en-us/training/modules/create-paginated-reports-power-bi/7-check)

1. Why are parameters important in Power BI paginated reports?

They allow the report developer to control the refresh interval of the report.

-> They allow the user to control aspects of how the report is rendered when the report is run.
Parameters can be used in the report dataset, the report design surface, and other places. Users insert values into the available parameters, and the report author uses those values in the appropriate location in the report.

They are required so that Power BI can call the paginated report.

## Manage Datasets

[M source](https://learn.microsoft.com/en-us/training/modules/manage-datasets-power-bi/10-check)

1. Where are dataset-scheduled refreshes configured?

-> Power BI service
Dataset-<mark style="background: #FFB8EBA6;">scheduled refreshes are configured in Power BI service</mark>.

Power BI Desktop

AppSource

2. What reserved parameters configure the start and end of where Incremental refresh should occur?

Start and End parameters

StartRange and EndRange

-> <mark style="background: #FFB8EBA6;">RangeStart and RangeEnd</mark>
RangeStart and RangeEnd configure the start and end of where Incremental refresh should occur.

3. What is the difference between Promotion and Certification when you are endorsing a dataset?

Promotion requires write access while Certification requires permission from the dataset owner to access to the dataset.

-> <mark style="background: #FFB8EBA6;">Promotion is for broad usage while Certification needs permission granted on the Admin Tenant settings</mark>.
Promotion does not need specific permissions while Certification requires permission from the dataset owner to access to the dataset.

Promotion is for specific users while Certification needs permission granted on the Admin Tenant settings.

# From Free Practice Test

1. Your company has a SharePoint server located in a datacentre in Montreal.
You plan to create a report in the Power BI service that will use Microsoft Excel files stored on the SharePoint server.
You need to recommend a solution to ensure that the dataset for the report can automatically refresh daily.
What should you include in the recommendation?

a Point to Site virtual private network (VPN)

a Site-to-Site virtual private network (VPN)

-> an on-premises data gateway

Azure Data Box

An on-premises SharePoint server requires the use of a Power BI gateway since it’s an on-premises data source. VPN-based solutions would provide connectivity to an Azure virtual network, but not Power BI service. Azure Data Box is a solution for migrating data to Azure, which is not applicable in this scenario.
[Use a Power BI gateway to connect to on-premises data sources - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/manage-datasets-power-bi/4-power-bi-gateway)


2. You manage a Power BI workspace.
You need to delegate the task to schedule data refreshes. The solution must use the principle of least privilege.
Which role should you use?

Admin

-> Contributor

Member

Viewer

The Contributor role is the least privileged role that grants permissions to schedule data refreshes. The Member role grants permission to schedule data refreshes but is more privileged than Contributor. The Admin role grants the permissions to schedule data refreshes but is more privileged than Member. The Viewer role does not grant the permissions to schedule data refreshes.
[Distribute a report or dashboard - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/create-manage-workspaces-power-bi/2-distribute-report-dashboard)


3. You have several on-premises Microsoft SQL Server databases.
You need to provide Power BI Service users access to the data sources without exposing the database servers directly to the internet.
The solution must minimize the configurations that must be performed by each user.
What should you deploy?

a virtual network data gateway

an ExpressRoute connection

-> an on-premises data gateway

an on-premises data gateway (personal mode)

An on-premises gateway is designed to allow multiple users to access multiple data sources. An on-premises data gateway only allows one user to access multiple data sources. A virtual network data gateway is designed to allow multiple users to access multiple online data sources. However, it isn’t installed locally and only works with data sources secured by virtual networks.
[Use a Power BI gateway to connect to on-premises data sources - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/manage-datasets-power-bi/4-power-bi-gateway)
[On-premises data gateway - Power BI | Microsoft Learn](https://learn.microsoft.com/power-bi/connect-data/service-gateway-onprem)


4. You have a fact table that contains sales data and the following two date columns:
- OrderDate
- ShipDate
Both columns have a relationship to the Date column in the Calendar table, and DAX measures have been configured to use these relationships for calculations related to order or ship dates.
You need to ensure that by default, the Calendar table does **NOT** filter the fact table, unless it is using a DAX measure that uses these relationships.
What should you do?

-> Disable Make this relationship active for both relationships.

Enable Apply security filter in both directions for both relationships.

Enable Make this relationship active for both relationships.

Set the cross-filter direction to both for each relationship.

You can have multiple inactive relationships between two tables in Power BI datasets. DAX measures can then use the `USERELATIONSHIP` function to activate a relationship for calculations. Relationship direction is not required for either the relationships or measures to work in this model setup. Only one active relationship can exist between two tables in a Power BI dataset. Applying a security filter in both directions isn’t required for this model setup.
[Define data granularity - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/design-model-power-bi/5-data-granularity)
[Work with relationships and cardinality - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/design-model-power-bi/6-relationships-cardinality)
[Active vs inactive relationship guidance - Power BI | Microsoft Learn](https://learn.microsoft.com/power-bi/guidance/relationships-active-inactive)

5. You have a Power BI model.
You need to assign items to a display folder.
Which three items can be assigned to a display folder? Each correct answer presents part of the solution.
Select all answers that apply.

-> Calculated column

-> Column

-> Measure

Report

Table

Tables and reports cannot be assigned a display folder. Columns, calculated columns, and measures can be assigned a display folder.
[Lab - Model data in Power BI Desktop, Part 1 - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/design-model-power-bi/8-lab)


6. You have a Power BI Desktop dataset that includes a table named Employees containing a row for each employee with the following columns:
- Employee ID
- Employee Name
- Manager ID
- Manager Name
You need to flatten the parent-child hierarchy in the Employees table by adding an extra column that will contain a listing of employee IDs for all direct and indirect managers of each employee.
Which two Data Analysis Expression (DAX) functions should you use? Each correct answer presents part of the solution.
Select all answers that apply.

`PATHCROSSJOIN`

`EXCEPT PATHITEM`

-> <mark style="background: #FF5582A6;">EXCEPTPATH</mark>

-> <mark style="background: #FF5582A6;">PATHITEM CROSSJOIN</mark>

`RELATED`

The `PATH` function returns a string with identifiers of all the parents of the current identifier, which is used for flattening. The `PATHITEM` function returns the item at the specified position of a string, which is also used for flattening. The `EXCEPT` function returns rows from one table which do not appear in another table, which would require another table. The `CROSSJOIN` function returns a Cartesian product of all rows from all tables that the function references. The `RELATED` function returns a related value from another table, which would require another table.
[Design a data model in Power BI - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/design-model-power-bi/)

7. You are creating a report in a Power BI Desktop by using a dataset that contains sales data.
You need to create a measure that always provides the value of total sales for the year 2022, regardless of which year is selected in any visual in the same report.
Which DAX function should you use in combination with the `SUM` function to override the context and provide the result?

-> `CALCULATE`

`FILTER`

`IGNORE`

`SUMX`

The `CALCULATE` function provides the result of the calculation with the ability to override the context. The `IGNORE` function modifies the behavior of the `SUMMARIZECOLUMNS` function by omitting specific expressions from the `BLANK/NULL` evaluation. The `FILTER` function returns a table that represents a subset of another table or expression. The `SUMX` function returns the sum of an expression evaluated for each row in a table.
[Use the Calculate function - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/create-measures-dax-power-bi/3-calculate-function)


8. You need to use DAX quick measures to generate results to use in a report.

Which type of DAX quick measure calculations will **NOT** work against a DirectQuery table?

aggregate per category

mathematical operations

-> time intelligence

X-functions

Time intelligence functions have performance implications and are disabled for quick measures against DirectQuery tables. Mathematical operations, aggregate per category, and X-functions are all supported against DirectQuery.
[Introduction to DAX - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/create-measures-dax-power-bi/1-introduction)
[Use quick measures for common and powerful calculations - Power BI | Microsoft Learn](https://learn.microsoft.com/power-bi/transform-model/desktop-quick-measures)

9. You plan to run Power BI Desktop Performance Analyzer.
You need to ensure that the data engine cache will NOT impact the test results without restarting Power BI Desktop.
What should you do first?
Select only one answer.

Add a blank page to the .pbix file and select it.

-> Connect DAX Studio to the data model.

Invoke the Clear Cache function.

Invoke the Refresh Metadata function.

DAX Studio, once connected to the data model, can be used to clear the data engine cache. The Clear Cache function can be invoked from DAX Studio, once you connect it to the data model. The Refresh Metadata function can be invoked from DAX Studio to update the metadata of the currently selected model. ***Adding a blank page to the .pbix file and selecting it is the first step in clearing the visual cache, not the data engine cache***.
[Review performance of measures, relationships, and visuals - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/optimize-model-power-bi/2-performance)

10. You decide to remove unnecessary columns from your data model.

What are two potential performance benefits of doing this? Each correct answer presents a complete solution.

Select all answers that apply.

decreasing report page load times

increasing DAX performance

-> increasing the refresh speed

-> reducing the size of the data model

Fewer columns mean there is less data to import and will reduce the model size and decrease the time it takes to refresh the model. <mark style="background: #D2B3FFA6;">Since row counts aren’t changing, the calculation speed of any existing DAX measures won’t change</mark>. <mark style="background: #FFB86CA6;">Report page load times are primarily determined by number of visuals (objects) on the page, and DAX performance</mark>. Neither of which are impacted by unnecessary model columns.
[Review performance of measures, relationships, and visuals - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/optimize-model-power-bi/2-performance)

11. You have Power BI Desktop.
You need to determine query timings for a report page visual.
Which method should you use?
Select only one answer.

Refresh the data model.

Run the Best Practices analyzer in Tabular Editor.

Use Session Diagnostics from the Power Query Editor.

-> Use the Performance analyzer.

The **Performance analyzer** will show the **query timings for each object** on a report page. **Session diagnostics** measures Power Query **query performance as it relates to refresh times**. It is unrelated to measuring DAX performance or report page query timings. The Best Practices analyzer reviews the model for best practices around things like model design, relationships, field naming conventions, and measures. But is unrelated to any query timings for report page visuals.

[Review performance of measures, relationships, and visuals - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/optimize-model-power-bi/2-performance)
11. You have a Power BI data source.
You need to analyze the data to meet the following requirements:
- Add a Top 10 filter to a visual.
- Ensure that the filter does NOT display in the **Filters on this visual** display for that **Visual Header** icon.
- Title the visual “Top 10 Product Category by Sales Amount”.
What should you do?
Select only one answer.

Hide **Filters on this visual** icon from the Header configuration for this visual.

Hide the **Filters** pane panel.

Hide the Top 10 filter in the visual level filters for this visual in the **Filters** pane.

-> Hide the visual header for this visual.

Only hiding the top 10 filter from the visual level filters in the filters pane will hide just this filter but allow other filters to show under the **Filters on this visual** icon for this visual.
[Use advanced interactions and drill through - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/data-driven-story-power-bi/6-advanced-interactions)

12. You plan to create a report in Power BI Desktop.
You need to create a visualization to display a running total. The solution must meet the following requirements:
- The initial and the final value columns must start on the horizontal axis.
- The intermediate values must be floating columns.
Which type of visualization should you use?
Select only one answer.

combo

funnel

scatter

-> waterfall

A waterfall visualization is a chart that displays a running total, with the initial and the final value columns starting on the horizontal axis while the intermediate values are floating columns. A combo visualization is a chart that combines a column chart and a line chart and can have one or two Y axes. A funnel visualization is a chart that has sequential connected stages, where items flow sequentially from one stage to the next. A scatter visualization is a chart with two value axes, with one set of numerical data along a horizontal axis and another set of numerical values along a vertical axis.
[Choose an effective visualization - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/visuals-power-bi/3-effective-visualization)

13. You need to create a custom Python visual by using Power BI Desktop.
What do you need to do first?
Select only one answer.

Configure global Python scripting options in Power BI Desktop.


Enable preview features in Power BI Desktop.

-> Enable the script visuals option in the Visualization pane of Power BI Desktop.


Install Python on your computer.

Enabling the script visuals option in the Visualization pane of Power BI Desktop is required before creating custom Python visuals in Power BI Desktop. Installing Python is not required. Configuring global Python scripting options in Power BI Desktop is not required to create Python visuals. The ability to create a custom Python visual by using Power BI Desktop has no dependency on enabling preview features.
[Add an R or Python visual - Training | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-python-visuals#:~:text=In%20the%20Enable%20script%20visuals%20dialog%20box%20that%20appears%2C%20select%20Enable.)

14. You need to create a custom R visual by using Power BI Desktop.
What do you need to do first?
Select only one answer.

Configure global R scripting options in Power BI Desktop.

Enable preview features in Power BI Desktop.

Enable the script visuals option in the Visualization pane of Power BI Desktop.

-> Install R on your computer.

To create a custom R visual by using Power BI Desktop, you first need to install R on your computer. Configuring global R scripting options in Power BI Desktop might be required once you install R on your computer. Enabling the script visuals option in the Visualization pane of Power BI Desktop is done once R is installed and configured using the global R script options in Power BI Desktop. Creating a custom R visual by using Power BI Desktop has no dependency on enabling preview features.
[Add an R or Python visual - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/visuals-power-bi/6-python-visual?ns-enrollment-type=learningpath&ns-enrollment-id=learn-bizapps.visual-data-power-bi)

15. You need to create a visual that displays sales by employees, trending over months.
The visual must clearly show how employees are performing against each other and have a ranking for each period.
Which visual should you use?
Select only one answer.

clustered bar chart

-> ribbon chart

scatterplot

treemap

A ribbon chart places the highest (ranked) value at the top of the stacked column each month and shows those ranked changes over time. A treemap is not meant for displaying changes over time and wouldn’t easily show ranked comparisons between employees. The clustered bar chart can be used to show changes over time, and a clustered bar chart will show comparisons between employees, but no ranking data is provided between employees. A scatterplot is typically used to compare a relationship between two (or more) calculations and their categorical distribution between each other.
[Choose an effective visualization - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/visuals-power-bi/3-effective-visualization?ns-enrollment-type=learningpath&ns-enrollment-id=learn-bizapps.visual-data-power-bi)
[Use ribbon charts in Power BI - Power BI | Microsoft Learn](https://learn.microsoft.com/power-bi/visuals/desktop-ribbon-charts?tabs=powerbi-desktop)

16. You have a bar chart and column chart visual on a report page. Selecting any column from the bar chart visual filters the column chart data to less than 1% of its unfiltered value.Which type of visual interaction should be used when the bar chart is filtering the column chart to ensure that you can easily see the data?
Select only one answer.

expand

drillthrough

-> <mark style="background: #D2B3FFA6;">filter</mark>

highlight

Filter will show you the filtered data in this visual. So even when showing filtered data that is less than 1% of the unfiltered value, it will still display well in the column visual. Highlight shows you both the unfiltered and filtered values in the visual, for comparison purposes. Drillthrough is a page navigation experience that takes you from one page to another plus applies a set of filters to page navigated to. Expand is a way to navigate down a level using the hierarchy controls.
[Change how visuals interact in a report - Power BI | Microsoft Learn](https://learn.microsoft.com/power-bi/create-reports/service-reports-visual-interactions?tabs=powerbi-desktop)


17. You plan to use Power BI Desktop to analyze sales data for products sold by your company.
You need to create a DAX formula that will list 10 best-selling products sorted by their total sales.
Which DAX function should you use?
Select only one answer.

`MAXA`

`MAXX`

`RANKX`

-> `TOPN`

The `TOPN` function returns Top N rows of the specified table, such as, for example, top 10 best-selling products sorted by their total sales. The `MAXA` function returns the largest value in a column. The `MAXX` function evaluates an expression for each row and returns the largest value. The `RANKX` function returns ranking of a number in a list of numbers for each row of a target table.
[Explore statistical summary - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/perform-analytics-power-bi/2-statistical-summary)


18. You plan to use Power BI Desktop to analyze sales data of your company.
You need to identify two types of data you will be able to use for creating bins that group the sales data.
Which two data types should you identify? Each correct answer presents a complete solution.
Select all answers that apply.

Binary

-> Date/time

-> Numeric

Text

True/false

Date/time and numeric data types support bins-based grouping. Binary, Boolean, and text data types do not support bins-based grouping.
[Group and bin data for analysis - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/perform-analytics-power-bi/4-group-data)

19. You create a Power BI data source which uses a SQL `SELECT` statement. The SQL statement queries multiple tables in a SQL Server database and includes subqueries.
When importing data from the data source into Power BI, you receive the following error message: “Timeout expired.”
You verify that network connection to the SQL Server has sufficient available bandwidth and low latency.
You need to minimize the occurrences of the timeout issues indicated by the message.
What should you do?
Select only one answer.

-> Divide the SQL statement into separate data sources.

Implement aggregations in the SQL statement.

Implement groupings in the SQL statement.

Replace subqueries with nested queries.

Dividing the SQL statement into separate data sources would minimize the amount of processing on the SQL Server side. This would minimize or even eliminate the timeout issues. Groupings, aggregations, and using nested queries would either have no impact on timeout issues or further increase the amount of processing on the SQL Server side, resulting in more frequent timeout issues.
[Resolve data import errors - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/get-data/9-import-errors)

20. You create a Power BI data source which uses a SQL `SELECT` statement. The SQL statement queries multiple tables in a SQL Server database and includes subqueries.
After you import data from the data source into Power BI, you notice that one of the columns in the resulting dataset appears blank. You verify that the source table does include data.
What should you do to resolve the issue?
Select only one answer.

Clear permissions on the data source in Power BI.

-> Use the `CAST` function in the SQL statement.

Use the `DATALENGTH` function in the SQL statement.

Set the privacy levels on the data source.

The issue indicates that Power BI is incorrectly interpreting the data type used by the source column. To resolve it, you need to explicitly specify the intended data type, which can be done by using the `CAST` function. `DATALENGTH` displays the number of bytes used to represent an expression. Clearing permissions could prevent Power BI from being able to access the target database. Setting the privacy levels of the data source would have no impact on addressing the issue of missing data.

[Resolve data import errors - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/get-data/9-import-errors)


21. You have an Excel spreadsheet that contains three columns labeled Year, 2021, and 2012. The entries in rows for the first column consists of names of the individual months in the year while the other two columns contain the sales amount for each month for the corresponding year.
You import data from the Excel spreadsheet into Power BI Desktop.
You need to transform the data so it will consist of three columns, with the first one containing month, the second containing year, and the third containing the sales amount for that month and year.
Which transformation should you use first?
Select only one answer.

Pivot

Remove Columns

Transpose Table

-> Unpivot

Selecting Unpivot will allow you to shape the current table into the one with the year, month, and sales amount columns, which will need to be renamed afterwards. Pivot would be applicable in the opposite scenario, in which flat data needs to be reorganized into one containing aggregate values for each unique value in each column. Transposing would switch rows and columns. Removing columns would result in a table with insufficient data to perform unpivot.
[Shape the initial data - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/clean-data-power-bi/2-shape-data)
[Unpivot columns - Power Query | Microsoft Learn](https://learn.microsoft.com/power-query/unpivot-column)

22. You connect Power Query Editor to a database table.
You need to remove the Row ID column. Your solution must ensure that new columns do NOT display in the table model during a scheduled refresh in the future.
What transformation should you use?
Select only one answer.

Select **Row ID**, then use the **Remove Other Columns** command.

Use the **Remove Column** command on the **Row ID** column.

-> <mark style="background: #FF5582A6;">Use the Select Columns command and chose the columns to keep</mark>.

Use the **Transpose** command, then filter the rows to remove **Row ID**.

Only the **Select Columns** command will let you choose columns to keep, delete the columns you do not want, and prevent new columns from showing up in the table in the future.
[Shape the initial data - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/clean-data-power-bi/2-shape-data)



23. You have a Power BI model with the following fact tables and storage modes.
- `FactStoreSales` (Import mode)
- `FactOnlineSales` (DirectQuery mode)
You have a dimension table named `DimCalendar` that has a relationship to both fact tables.
You need to assign a storage mode for `DimCalendar`. The solution must minimize the time to execute queries that combine data from the dimension table and the fact tables.
Which storage mode should you use?
Select only one answer.

DirectQuery

-> Dual

Import

none

Using Dual mode means that either an import query can be run when accessing data from `FactStoreSales`, or a DirectQuery query can be run when accessing data from `FactOnlineSales`. Using Import mode means the queries are only optimized for `FactStoreSales` (Import). Using DirectQuery mode means the queries are only optimized for `FactOnlineSales` (DirectQuery). A storage mode of Import, DirectQuery, or Dual must be assigned.
[Select a storage mode - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/get-data/6-storage-mode)
[Use storage mode in Power BI Desktop - Power BI | Microsoft Learn](https://learn.microsoft.com/power-bi/transform-model/desktop-storage-mode)

24. In Power BI Desktop, you <mark style="background: #FFB8EBA6;">need to create a role.
Which two interfaces can you use?</mark> Each correct answer presents a complete solution.
Select all answers that apply.

Data view

-> Model view

Page view

Power Query Editor

-> Report view

The Model view provides the ability to design and implement structure of a dataset and include the option to create a role. The Report view provides the ability to manage roles, including their creation. The Data view provides access to data within a dataset Power Query Editor provides the ability to transform and analyze data. The Page view is an option available from within the Report view and is intended to simplify designing and building reports.
[Implement row-level security - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/row-level-security-power-bi/)

26. You need to create a new hierarchy in Power BI Desktop.
What should you do first?
Select only one answer.

From the Model view, drag-and-drop one column onto another column in the Fields pane.

-> From the Model view, right-click and select Create hierarchy.

From the Report view, drag-and-drop one column onto another column in the Fields pane.

To create a new hierarchy in Power BI Desktop, you must select Create hierarchy from the Model view or Report view. The option to create hierarchies by dragging and dropping was removed as an option in 2021 because too many hierarchies were being accidentally created during development. You cannot drag-and-drop one field onto another to create a new hierarchy. You can only use this method to add additional fields to an already existing hierarchy.
[Work with dimensions - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/design-model-power-bi/4-dimensions)

27. You plan to use the calculated table functionality to add a duplicate table in Power BI Desktop.
Which characteristics of the original table will be duplicated?
Select only one answer.

data and column visibility only

data and hierarchies only

data, hierarchies, and column visibility

-> data only

A calculated table only duplicates data. Any model configurations such as column visibility or hierarchies must be recreated if needed.
[Introduction - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/dax-power-bi-add-calculated-tables/1-introduction)

28. You need to develop a <mark style="background: #FF5582A6;">quick measure</mark> in Power BI Desktop.
Which two elements can you use? Each correct answer presents a complete solution.
Select all answers that apply.

-> <mark style="background: #FF5582A6;">Calculations</mark>

Conditional columns

Data Analysis Expression (DAX) queries

-> <mark style="background: #FF5582A6;">Fields</mark>

Power Query M functions

When creating a quick measure in Power BI Desktop, you apply calculations to fields. You do not explicitly create a DAX query, but you choose calculations and fields, which result in automatic generation of a DAX query. Conditional columns are separate from quick measures. Unlike quick measures, they create a value for each row in a table and are stored in the .pbix file. Power Query M functions are not directly accessible from the Quick Measure interface.
[Lab - Model data in Power BI Desktop, Part 1 - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/design-model-power-bi/8-lab)
[Introduction to DAX - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/create-measures-dax-power-bi/1-introduction)


29. You need to enhance a data model by using Power BI Desktop.
Data for which two model items can be created using the DAX language? Each correct answer presents a complete solution.
Select all answers that apply.

-> calculated table

display folder

hierarchies

-> numeric range parameter

Calculated tables are generated with DAX queries. Numeric range parameters create a table and measure, both generated with DAX queries. Hierarchies are helpful for drilldown and are defined as part of the data model, but they are not generated by using DAX. Display folders are a way to visually organize measures, columns, or hierarchies. DAX is not used to create them.
[Introduction to DAX - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/create-measures-dax-power-bi/1-introduction)

30. You plan to optimize the performance of Power BI Desktop queries against a remote data source.
You need to disable the default behavior that automatically applies cross highlighting and filtering of visuals within the same report.
Which option should you configure in Power BI Desktop?
Select only one answer.

the Filters Query reduction settings

the Persistent filters of Report settings

-> the Reduce number of queries sent by Query reduction setting

the Slicers Query reduction settings

The Reduce number of queries sent by Query reduction setting disables the default behavior that automatically applies cross highlighting and filtering of visuals within the same report. The Slicers Query reduction settings allow you to instantly apply slicer changes and add an Apply button to each slicer. The Filters Query reduction settings allow you to instantly apply basic filter changes. The Persistent filters of Report settings allow you to prevent users from saving filters in the Power BI service.
[Optimize DirectQuery models with table level storage - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/optimize-model-power-bi/5-directquery-models)

31. You plan to get data for a Power BI dataset from flat files.
You need to select a location for the files. The location must provide the ability to configure scheduled refresh for the dataset by using ***Microsoft 365 credentials***.
Which two location types should you recommend? Each correct answer presents a complete solution.
Select all answers that apply.

local file

-> OneDrive for Business

Personal OneDrive account

-> SharePoint – Team Sites

A personal OneDrive account provides the ability to automatically synchronize flat files residing in a user's OneDrive and Power BI datasets. Since it relies on OneDrive access, it requires the user's credentials of the corresponding Microsoft account. The OneDrive - Business option uses Azure Active Directory credentials (i.e., ***Microsoft 365 credentials***). The SharePoint – Team Sites option uses the same Azure Active Directory credentials as the ones used to access SharePoint Online. For the local file option, no additional credentials are required to access them.
[Get data from files - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/get-data/2-data-files)


32. From Power BI Desktop, you create a data source by importing an Excel file that contains ***10,000*** rows.
You plan to identify data anomalies within the data source.
You need to ensure that column distribution considers all rows in the Excel file.
What should you do?
Select only one answer.

In the Data Source Settings, modify the Advanced settings.

In the Data Source Settings, modify the Edit Permissions settings.

-> <mark style="background: #ABF7F7A6;">In the Power Query Editor window, enabled the Column Profile view</mark>.

In the Power Query Editor window, modify the Query Settings.

By default, Power BI uses the top 1,000 rows for profiling. To ensure that column distribution considers all rows in the Excel file, you need to modify the Power Query Editor profiling status setting. The Power Query Editor settings, Advanced settings, and Permissions settings have no bearing on the profiling characteristics.
[Profile data in Power BI - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/clean-data-power-bi/6-profile-data)

