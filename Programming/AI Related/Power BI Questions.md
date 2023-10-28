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
You need to delegate the task to <mark style="background: #FF5582A6;">schedule data refreshes</mark>. The solution must use the principle of least privilege.
Which role should you use?

Admin

-> <mark style="background: #FF5582A6;">Contributor</mark>

Member

Viewer

The Contributor role is the least privileged role that grants permissions to schedule data refreshes. The Member role grants permission to schedule data refreshes but is more privileged than Contributor. The Admin role grants the permissions to schedule data refreshes but is more privileged than Member. The Viewer role does not grant the permissions to schedule data refreshes.
[Distribute a report or dashboard - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/create-manage-workspaces-power-bi/2-distribute-report-dashboard)

3. You manage a Power BI workspace.
You need to delegate the task to <mark style="background: #FF5582A6;">update workspace metadata</mark>. The solution must use the principle of least privilege.
Which role should you use?
Select only one answer.

-> <mark style="background: #FF5582A6;">Admin</mark>

Contributor

Member

Viewer

The Admin role is the only one that has the permission to update workspace metadata.
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


33. In Power BI Desktop, you plan to use M-language to define a common date table spanning a period of 10 years.
You need identify the M language function that would allow you to specify that rows in the table should represent consecutive days within the date range you designated. Your solution must minimize administrative effort.
Which syntax should you use?
Select only one answer.

`#date`

-> `#duration`

`List.Combine`

`List.Durations`

The `#duration` function of the M language allows you to specify the datetime values that will be entered into individual rows of a date table. The `#date` function creates a date value based on the date parameters you specify. The `List.Combine()` combines multiple lists into one. `List.Durations` returns a list of count duration values, rather than dates.
[Create a date table - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/design-model-power-bi/3-date-table)
[Power Query M function reference - PowerQuery M | Microsoft Learn](https://learn.microsoft.com/powerquery-m/power-query-m-function-reference)


34. You create a data model in Power BI Desktop that contains DAX calculated columns and measures. You now need to create a report.
In which two places can a ***DAX calculated column be used, but a DAX calculated measure cannot be used?*** Each correct answer presents a complete solution.
Select all answers that apply.

-> <mark style="background: #ABF7F7A6;">as a filter in the “Filters on this page” well of the Filters pane</mark>

as a filter in the “Filters on this visual” well of the Filters pane

as an item in the “Add drill-through fields here” well of the Visualizations pane

-> as an item in the Fields well of a slicer

Unlike a measure, a calculated column can be used in a slicer to place filter options on the report page. DAX measures cannot be placed in the “Filters on this page” well. They can only be placed per visual, in the “Filters on this visual” well of the Filters Pane. Both DAX columns and measures may be used as a visual-level filter. Both DAX columns and measures can be used in the drillthrough well.
[Introduction to DAX - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/create-measures-dax-power-bi/1-introduction)

36. In Power BI Desktop, you need to create a measure.
Which two interfaces can you use? Each correct answer presents a complete the solution.
Select all answers that apply.

-> Data view

Model view

Page view

-> Power Query Editor (but description says it's incorrect, and it really IS incorrect)

Report view (but description says it's correct, and it really IS correct)

**The Report view provides the ability to create measures**. To create a measure, use the context sensitive menu of the Fields list or the Calculations section of the ribbon. The Data view provides access to data within a dataset and includes the option to create a measure in the Calculations section of the ribbon. Model view, Page view, and **Power Query Editor do not include the option to create a measure**.
[Introduction to DAX - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/create-measures-dax-power-bi/1-introduction)

37. From the Power Query Editor, you import data from a .csv file. The data includes a column named ZIP that contains postal codes from the United States.
You notice that Power Query Editor automatically applies the Whole Number data type to the ZIP column.
You need to ensure that the ZIP column uses the Text data type and that all values remain 5 characters long.
What should you do?
Select only one answer.

From the data view in Power BI Desktop, change the column data type from number to text.

From Power Query Editor, add a new applied step at the end of the query to convert the ZIP column from number back to text.

From Power Query Editor, delete the changed type step.

-> From Power Query Editor, update the current changed type step and replace convert from number to text for the ZIP column.

To correctly update the data to text you need to replace the number type conversion with a text conversion, and to keep all other data type column transformations. This needs to be done in the Power Query Editor. <mark style="background: #D2B3FFA6;">Adding a new applied step at the end of the query would result in loosing zip codes that start with 0</mark>. Changing the data type in Data View is equivalent to adding an applied step at the end of the query and would not preserve leading zeros. Deleting the changed type step would not set the data type to Text.
[Evaluate and change column data types - Training | Microsoft Learn](https://learn.microsoft.com/training/modules/clean-data-power-bi/4-column-data-types)

# From Examtopics

[Source](https://www.examtopics.com/exams/microsoft/pl-300/view/), 2023-10-2 update

Note 1: some questions are paraphrased for me to easily understand.

Note 2: T1 means Topic 1, etc.

1 (T1)
given this model:
![Pasted image 20231018110806](../../Media/Default/Pasted%20image%2020231018110806.png)
and these refresh specifications:
* Sales -> real time
* Customer -> daily
* SalesAggregate -> Weekly
* Date -> every three years

mention the storage mode for each table.

Answer (in same order of tables):
* DirectQuery
* Dual
* Import
* Dual

reason for using Dual can be visualized like this:
![Pasted image 20231018111418](../../Media/Default/Pasted%20image%2020231018111418.png)
So `Date` is queried as DirectQuery when dealing with `Sales` and as Import when dealing with `SalesAggregate`

2 (T1)
You have a project management app that is fully hosted in **Microsoft Teams**. The app was developed by using Microsoft Power Apps.  
You need to create a Power BI report that connects to the project management app.  
Which connector should you select?  

- A. Microsoft Teams Personal Analytics
- B. SQL Server database
- C. Dataverse
- D. Dataflows

Answer:
C. Dataverse

3 (T1)
Suppose you have these tables:
![Pasted image 20231018115643](../../Media/Default/Pasted%20image%2020231018115643.png)
You need to perform the following analyses:  
* Orders sold over time that include a measure of the total order value  
* Orders by attributes of products sold
The solution must minimize update times when interacting with visuals in the report.  
What should you do first?

- A. From Power Query, merge the Order Line Items query and the Products query.
- B. Create a calculated column that adds a list of product categories to the Orders table by using a DAX function.
- C. Calculate the count of orders per product by using a DAX function.
- D. From Power Query, merge the Orders query and the Order Line Items query.

Answer:
D. 
Explanation:
the 2 latter tables are both fact tables (Header/Detail schema), so they should be first merged to one fact table, so that star schema is applied. Check out [this](https://www.sqlbi.com/articles/header-detail-vs-star-schema-models-in-tabular-and-power-bi/) article for details. 

4 (T1)
You have a Microsoft SharePoint Online site that contains several document libraries.  
One of the document libraries contains manufacturing reports saved as Microsoft Excel files. All the manufacturing reports have the same data structure.  
You need to use Power BI Desktop to load only the manufacturing reports to a table for analysis.  
What should you do?  

- A. Get data from a SharePoint folder and enter the site URL Select Transform, then filter by the folder path to the manufacturing reports library.
- B. Get data from a SharePoint list and enter the site URL. Select Combine & Transform, then filter by the folder path to the manufacturing reports library.
- C. Get data from a SharePoint folder, enter the site URL, and then select Combine & Load.
- D. Get data from a SharePoint list, enter the site URL, and then select Combine & Load.

Answer:
A.
Explanation/Demonstration can be found in [this](https://www.youtube.com/watch?v=XuLnSYjmsJo) video.

5 (T1)
You have a Microsoft Excel file in a Microsoft OneDrive folder.  
The file must be imported to a Power BI dataset.  
You need to ensure that the dataset can be refreshed in powerbi.com.  
Which two connectors can you use to connect to the file? Each correct answer presents a complete solution.  
NOTE: Each correct selection is worth one point.

- A. Excel Workbook
- B. Text/CSV
- C. Folder
- D. SharePoint folder
- E. Web

Answer:
Examtopics says A. & C., [another website](https://zhuanlan.zhihu.com/p/601138239) says D. & E.

6 (T1)
You have a folder that contains 100 CSV files.  
You need to make the file metadata available as a single dataset by using Power BI. The solution must NOT store the data of the CSV files.  
Which three actions should you perform in sequence. To answer, move the appropriate actions from the list of actions to the answer area and arrange them in the correct order.  
Select and Place:
![Pasted image 20231018134226](../../Media/Default/Pasted%20image%2020231018134226.png)
Answer (I think):
Get data and select folder -> expand attributes -> remove content (note, last two could be switched, I don't know)
Explanation (source):
PowerBI has added two additional columns of content, content and attribute. Attribute contains metadata, including the file type, whether it is a temporary file, and when the file was last modified. Content is the data in the csv table. Therefore, content needs to be removed and attributes expanded.

7 (T1)
You publish a dataset that contains data from an on-premises Microsoft SQL Server database.    
The dataset must be refreshed daily.  
You need to ensure that the Power BI service can connect to the database and refresh the dataset.  
Which four actions should you perform in sequence? To answer, move the appropriate actions from the list of actions to the answer area and arrange them in the correct order:
![Pasted image 20231018140245](../../Media/Default/Pasted%20image%2020231018140245.png)
Answer:
![Pasted image 20231018140256](../../Media/Default/Pasted%20image%2020231018140256.png)
Explanation: Check [this](https://youtu.be/iq9M_ncz0tw?t=338) video.

9 (Q19) (T1)
Note: if you have this:
![Pasted image 20231018140821](../../Media/Default/Pasted%20image%2020231018140821.png)
and you want to unpivot, answer will be:
![Pasted image 20231018140901](../../Media/Default/Pasted%20image%2020231018140901.png)


10 (Q20) (T1)
You are using Power BI Desktop to connect to an Azure SQL database.
The connection is configured as follows:
![Pasted image 20231018141140](../../Media/Default/Pasted%20image%2020231018141140.png)
what is true in the following statements?:
![Pasted image 20231018141156](../../Media/Default/Pasted%20image%2020231018141156.png)
Answer:
10mins, only data (bec. full hierarchy is not checked. If it was checked, then "all the tables")

11 (Q25) (T1)
From Power Query Editor, you attempt to execute a query and receive the following error message.  
Datasource.Error: Could not find file.  
What are two possible causes of the error? Each correct answer presents a complete solution.

- A. You do not have permissions to the file.
- B. An incorrect privacy level was used for the data source.
- C. The file is locked.
- D. The referenced file was moved to a new location.

Answer:
<mark style="background: #ABF7F7A6;">A</mark>. & D.

You have a CSV file that contains user complaints. The file contains a column named Logged. Logged contains the date and time each complaint occurred. The data in Logged is in the following format: 2018-12-31 at 08:59.
You have a CSV file that contains user complaints. The file contains a column named Logged. Logged contains the date and time each complaint occurred. The data in Logged is in the following format: 2018-12-31 at 08:59.

28 (T1)
You have two Microsoft Excel workbooks in a Microsoft OneDrive folder.  
Each workbook contains a table named Sales. The tables have the same data structure in both workbooks.  
You plan to use Power BI to combine both Sales tables into a single table and create visuals based on the data in the table. The solution must ensure that you can publish a separate report and dataset.  
Which storage mode should you use for the report file and the dataset file? To answer, drag the appropriate modes to the correct files. Each mode may be used once, more than once, or not at all.

![Pasted image 20231018151039](../../Media/Default/Pasted%20image%2020231018151039.png)
Answer:
<mark style="background: #ABF7F7A6;">Import, DirectQuery</mark>

29 (T1)
You are creating a report in Power BI Desktop.  
You load a data extract that includes a free text field named coll.  
You need to analyze the frequency distribution of the string lengths in col1. The solution must not affect the size of the model.  
What should you do?  

- A. In the report, add a DAX calculated column that calculates the length of col1
- B. In the report, add a DAX function that calculates the average length of col1
- C. From Power Query Editor, add a column that calculates the length of col1
- D. From Power Query Editor, change the distribution for the Column profile to group by length for col1

Answer:
D.

30 (T2, Q3)
You need to provide a user with the ability to add members to a workspace. The solution must use the principle of least privilege.  
Which role should you assign to the user?  

- A. Viewer
- B. Admin
- C. Contributor
- D. Member

Answer:
<mark style="background: #FF5582A6;">D.</mark>


31 (T2, Q6)
You have a custom connector that returns ID, From, To, Subject, Body, and Has Attachments for every email sent during the past year. More than 10 million records are returned.  
You build a report analyzing the internal networks of employees based on whom they send emails to.  
You need to prevent report recipients from reading the analyzed emails. ***The solution must minimize the model size***.  
What should you do?  

- A. From Model view, set the Subject and Body columns to Hidden.
- B. Remove the Subject and Body columns during the import.
- C. Implement row-level security (RLS) so that the report recipients can only see results based on the emails they sent.

Answer:
<mark style="background: #FFB8EBA6;">B.</mark>


32 (T2, Q7)
You have this Power BI dataset:
![Pasted image 20231018205026](../../Media/Default/Pasted%20image%2020231018205026.png)
You need to make the table available as an ***organizational data type in Microsoft Excel***.   (i.e., ***featured tables in Power BI***)
How should you configure the properties of the table? To answer, select the appropriate options in the answer area:
![Pasted image 20231018205049](../../Media/Default/Pasted%20image%2020231018205049.png)

Answers:
ID, Name, Yes
[Demonstration video](https://www.youtube.com/watch?v=FE3jgq1exRM)


33 (T2, Q8)
You have the Power BI model:
![Pasted image 20231018214848](../../Media/Default/Pasted%20image%2020231018214848.png)
A manager can represent only a single country.  
You need to use row-level security (RLS) to meet the following requirements:  
* The managers must only see the data of their respective country.  
* The number of RLS roles must be minimized.  
Which two actions should you perform?

- A. Create a single role that filters Country[Manager_Email] by using the USERNAME DAX function.
- B. Create a single role that filters Country[Manager_Email] by using the USEROBJECTID DAX function.
- C. For the relationship between Purchase Detail and Purchase, select Apply security filter in both directions.
- D. Create one role for each country.
- E. For the relationship between Purchase and Purchase Detail, change the Cross filter direction to Single.

Answer:
A. & <mark style="background: #FFB8EBA6;">C.</mark> 
Explanation is in [this](https://asankap.wordpress.com/2018/05/28/how-does-row-level-security-works-when-there-is-a-bi-directional-filter-in-power-bi-tabular-model/) article.


34 (T2, Q9)
You have a Power BI imported dataset that contains this data model:
![Pasted image 20231018221248](../../Media/Default/Pasted%20image%2020231018221248.png)
Use the drop-down menus to select the answer choice that completes each statement based on the information presented in the graphic:
![Pasted image 20231018221259](../../Media/Default/Pasted%20image%2020231018221259.png)

Answer:
<mark style="background: #D2B3FFA6;">Cross filter direction</mark>, star schema
Notes:
* Cross filter direction was chosen as all of the relationships are bi-directionals (look at the red rectangles), and assuming this is a star schema, we usually filter the fact table by dimension tables, and not vice versa.
	* Also, "Assume Referential Integrity" is for DirectQuery models only, but this model is imported.
* People debated whether the model is star schema or [snowflake](https://www.integrate.io/blog/snowflake-schemas-vs-star-schemas-what-are-they-and-how-are-they-different/#:~:text=number%20of%20levels.%E2%80%9D-,Snowflake%20Schema%20Diagram,-Before%20we%20go), I personally think it is star schema, under the assumption that `Employee` is a [](Power%20BI.md#^zuytek|factless%20fact%20table).


35 (T2, Q10)
You have a Power BI model that contains a table named Sales and a related date table. Sales contains a measure named Total Sales.  
You need to create a measure that calculates the total sales from the equivalent month of the previous year.  
How should you complete the calculation? To answer, select the appropriate options in the answer area:
![Pasted image 20231018222930](../../Media/Default/Pasted%20image%2020231018222930.png)

Answer:
CALCULATE -> SAMEPERIODLASTYEAR -> 'Date'[Date]


36 (T2, Q15)
You have a Microsoft Power BI data model that contains three tables named Orders, Date, and City. There is a one-to-many relationship between Date and  
Orders and between City and Orders.  
The model contains two row-level security (RLS) roles named Role1 and Role2. Role1 contains the following filter.  
City[State Province] = "Kentucky"  
Role2 contains the following filter.  
Date[Calendar Year] = 2020 -  
If a user is a member of both Role1 and Role2, what data will they see in a report that uses the model?  

- A. The user will see data for which the State Province value is Kentucky or where the Calendar Year is 2020.
- B. The user will receive an error and will not be able to see the data in the report.
- C. The user will only see data for which the State Province value is Kentucky.
- D. The user will only see data for which the State Province value is Kentucky and the Calendar Year is 2020.

Answer:
<mark style="background: #D2B3FFA6;">A.</mark>
Explanation ([MD source](https://learn.microsoft.com/en-us/power-bi/guidance/rls-guidance#:~:text=When%20a%20report%20user%20is%20assigned%20to%20multiple%20roles%2C%20RLS%20filters%20become%20additive.%20It%20means%20report%20users%20can%20see%20table%20rows%20that%20represent%20the%20union%20of%20those%20filters.)):
When a report user is assigned to multiple roles, <mark style="background: #D2B3FFA6;">RLS filters become additive</mark>. It means report users can see table rows that represent the union of those filters.


37 (T2, Q16)
You are modeling data by using Microsoft Power BI. Part of the data model is a large Microsoft SQL Server table named Order that has more than 100 million records.  
During the development process, you need to import a sample of the data from the Order table.  
Solution: From Power Query Editor, you import the table and then add a filter step to the query.  
Does this meet the goal?

- A. Yes
- B. No

Answer:
A. Yes
Explanation:
Since it is a Microsoft SQL Server table, query folding can be applied to imported data (and must be imported to DirectQuery and Dual storage modes, but that's besides the point), therefore Power BI will attempt to fold the filtering step into the original query used to get the data from the data source. [M source 1](<https://learn.microsoft.com/en-us/power-query/power-query-folding#sources-that-support-folding:~:text=Filtering%20rows%2C%20with%20static%20values%20or%20Power%20Query%20parameters%20(WHERE%20clause%20predicates).>), [M source 2](https://learn.microsoft.com/en-us/power-query/native-database-query)


38 (T2, Q19)
You connect to the data stored in a Microsoft Excel spreadsheet by using Power Query Editor as shown here:
![[Pasted image 20231020222727.png]]
You need to prepare the data to support the following:  
✑ Visualizations that include all measures in the data over time  
✑ Year-over-year calculations for all the measures  
Which four actions should you perform in sequence? To answer, move the appropriate actions from the list of actions to the answer area and arrange them in the correct order:
![[Pasted image 20231020222741.png]]
Answer1:
Transpose -> use first row as headers -> unpivot -> rename measure to Year.
Answer2 (I think this is the correct one):
***use first row as headers -> unpivot -> rename "Attribute" to Year --> change datatype to Date*** (as "Date" type is used by DAX Time Intelligent functions like year-over-year (YOY)).
Explanation:
if answer1
then:
original data (short version):
![[Pasted image 20231020221600.png]]
Transpose then use first row as header:
![[Pasted image 20231020221658.png]]

Unpivot other columns than "m":
![[Pasted image 20231020221729.png]]
then, rename "m" to "Year".

However, if answer2
then:
original table (short version):
![[Pasted image 20231020221600.png]]

use first row as header:
![[Pasted image 20231020221914.png]]

unpivot columns other than "m":
![[Pasted image 20231020222405.png]]

then, Rename "Attribute" to "Year", then change its datatype to "Date".

39 (T2, Q21)
You plan to create Power BI dataset to analyze attendance at a school. Data will come from two separate views named View1 and View2 in an Azure SQL database.  
View1 contains the columns shown in the following table:
![[Pasted image 20231021110418.png]]
View2 contains the columns shown in the following table:
![[Pasted image 20231021110427.png]]
The views can be related based on the Class ID column.  
Class ID is the unique identifier for the specified class, period, teacher, and school year. For example, the same class can be taught by the same teacher during two different periods, but the class will have a different class ID.  
You need to design a star schema data model by using the data in both views. The solution must facilitate the following analysis:  
✑ The count of classes that occur by period  
✑ The count of students in attendance by period by day  
✑ The average number of students attending a class each month  
In which table should you include the Teacher First Name and Period Number fields? To answer, select the appropriate options in the answer area:
![[Pasted image 20231021110447.png]]

Answer:
Teacher Dim., ***Class Dim***.
Explanation:
The catch here is Count of Classes occur by Period; As soon as we call it by period it is referring to Dimension Period which will be static with Start Time & End Time hence it will go in Class Dimension rather than Fact. 
Another explanation:
Period number should be considered in Class dim, because it is a duplicate and is an attribute of the class in the first place. So a class has a period number even before any attendance is recorded.

40 (T2, Q27)
You are creating a Microsoft Power BI data model that has the tables shown in the following table:
![[Pasted image 20231021190550.png]]
The Products table is related to the ProductCategory table through the ProductCategoryID column. Each product has one product category.  
You need to ensure that you can analyze ***sales by product category***.  
How should you configure the relationship ***from ProductCategory to Products***? To answer, select the appropriate options in the answer area:
![[Pasted image 20231021190617.png]]

Solution:
one-to-many, single
Explanation for single:
recall the question:
"analyze ***sales by product category***", so ProductCategory -> Products -> Sales
and single cross-filtering always goes from 1 (i.e., ProductCategory) to many (i.e., Products), so no need to enable filtering in the other direction (i.e., ProductCategory <- Products)


41 (T2, Q28)
You import a Power BI dataset that contains the following tables:  
✑ Date  
✑ Product  
✑ Product Inventory  
The Product Inventory table contains 25 million rows. A sample of the data is shown in the following table:
![[Pasted image 20231021191113.png]]
The Product Inventory table relates to the Date table by using the DateKey column. The Product Inventory table relates to the Product table by using the  
ProductKey column.  
You need to reduce the size of the data model ***without losing information***.  
What should you do?
- A. Change Summarization for DateKey to Don't Summarize.
- B. Remove the relationship between Date and Product Inventory
- C. Change the data type of UnitCost to Integer.
- D. Remove MovementDate.

Answer:
D. 
Explanation:
The <mark style="background: #D2B3FFA6;">DateKey and MovementDate columns have the same information</mark>. Movementdate can be removed.


42 (T2, Q31)
You have a Power BI report that imports a date table and a sales table from an Azure SQL database data source. The sales table has the following date foreign keys:  
✑ Due Date  
✑ Order Date  
✑ Delivery Date  
You need to support the analysis of sales over time ***based on all the date foreign keys***.  
Solution: For each date foreign key, you ***add inactive relationships*** between the sales table and the date table.  
**Does this meet the goal**?

- A. Yes
- B. No

Answer:
<mark style="background: #D2B3FFA6;">B. No</mark>
Explanation:
1. only adding inactive relationships isn't the full solution; only a part of it, so technically, this didn't meet the entire goal
2. Even if it is implicitly assumed that we use USERRELATIONSHIP, this only enables one relationship at a time.
	1. Therefore, if we want to simultaneously use all relationships at the same time, we would need to rename the date table as Due Date and then use a DAX expression to create Order Date and Delivery Date as calculated tables. This is known as [[Power BI#Role-Playing Dimensions|role-playing dimension modelling]]


43 (T2, Q35)
You have a Power BI report named Orders that supports the following analysis:  
✑ Total sales over time  
✑ The count of orders over time  
✑ New and repeat customer counts  
The data model size is nearing the limit for a dataset in shared capacity.  
The model view for the dataset is shown in the following exhibit:
![[Pasted image 20231022215109.png]]
The data view for the Orders table is shown in the following exhibit:
![[Pasted image 20231022215135.png]]
The Orders table relates to the Customers table by using the CustomerID column.  
The Orders table relates to the Date table by using the OrderDate column.  
For each of the following statements, select Yes if the statement is true, Otherwise, select No:
![[Pasted image 20231022215206.png]]

Answer:
No, No, Yes
Explanation for first NO:
NOtice how `OrderID` and `ProductID` always change even for the same customer `TORTU`, this would make us assume that the system's logic directs each product purchased by a customer to a different `OrderID`, which would mean that grouping by `OrderID` and the other keys <mark style="background: #FF5582A6;">won't decrease the model size, as OrderID is now considered a unique column</mark>.


43 (T2, Q35)
You are creating a Power BI model that contains a table named Store. Store contains the following fields:
![[Pasted image 20231023212641.png]]
You plan to create a map visual that will show store locations and provide the ability to drill down from Country to State/Province to City.  
What should you do to ensure that the locations are mapped properly?
- A. Change the data type of City, State/Province, and Country.
- B. Set Summarization for City, State/Province, and Country to Don't summarize.
- C. Set the data category of City, State/Province, and Country.
- D. Create a calculated column that concatenates the values in City, State/Province, and Country.

Answer:
C.
Explanation:
Setting the <mark style="background: #FFF3A3A6;">data category</mark> for these fields will allow Power BI to recognize them as <mark style="background: #FFF3A3A6;">location-related fields</mark>, enabling proper mapping and drilling down capabilities.


44 (T2, Q44)
You have a table named Sales that contains the following fields:
![[Pasted image 20231024204745.png]]
You have a table named Transaction Size that contains the following data:
![[Pasted image 20231024204758.png]]
You need to create a calculated column to classify each transaction as small, medium, or large based on the value in Sales Amount.  
How should you complete the code? To answer, drag the appropriate values to the correct targets. ***Each value may be used once, more than once, or not at all***:
![[Pasted image 20231024204826.png]]

Answer:
FILTER, AND, <mark style="background: #FFB8EBA6;">CALCULATE</mark>
Explanation:
CALCULATE evaluates an expression in a modified filter context.  
Syntax: `CALCULATE(<expression>[, <filter1> [, <filter2> [, ג€¦]]])`
The expression used as the first parameter is essentially the same as a measure.  
Filters can be:  
  
Boolean filter expressions -  
  
Table filter expressions -  
  
Filter modification functions -  
  
Table filter expression -  
A table expression filter applies a table object as a filter. It could be a reference to a model table, but more likely it's a function that returns a table object. You can use the FILTER function to apply complex filter conditions, including those that cannot be defined by a Boolean filter expression.


45 (T2, Q47)
You are creating a quick measure as shown in the following exhibit:
![[Pasted image 20231025222401.png]]
You need to create a **monthly rolling average measure for Sales over time**.  
How should you configure the quick measure calculation?:
![[Pasted image 20231025222418.png]]

Answer:
<mark style="background: #FFB8EBA6;">Total Sales</mark>, Date, Months


46 (T2, Q50)
From Power Query Editor, you profile the data shown in the following exhibit:
![[Pasted image 20231025223109.png]]
The IoT GUID and IoT ID columns are unique to each row in the query.  
You need to **analyze IoT events by the hour and day of the year**. The solution **must improve dataset performance**.  
Q50: Solution: You **split** the IoT DateTime column into a column named Date and a column named Time.  
(Another question (Q51)): Solution: You remove the IoT GUID column and retain the IoT ID column.
Does this meet the goal?

For Q50:
- A. Yes
- B. No

For Q51:
- A. Yes
- B. No

Answer:
Q50: in Examtopics, B., however, 85% of users answered with A., as "splitting DateTime into date and time columns" should increase performance. However, I personally think B. should be correct for two reasons:
* Only splitting the column won't "meet the goal"; we need to create measures as well.
* We didn't delete the original datetime column, so technically the performance shouldn't have increased.
However, I think Microsoft wants us to neglect the first bullet point, and automatically assume that the second bullet point is implicitly applied. Therefore, if this comes up in the exam, I (personally) will probably answer with A.
Q51: in Examtopics,  A., moreover, most people chose A., but a lot of people have answered B. too. Therefore, if this comes up in the exam, I (personally) will probably answer with A.


47 (T2, Q54)
You have a Power BI data model that contains two tables named Products and Sales.  
A one-to-many relationship exists between the tables.  
You have a report that contains a report-level filter for Products.  
You need to create a measure that will return the percent of total sales for each product. ***The measure must respect the report-level filter when calculating the total***.  
How should you complete the DAX measure? To answer, drag the appropriate DAX functions to the correct targets. Each function may be used once, more than once, or not at all. You may need to drag the split bar between panes or scroll to view content.
![[Pasted image 20231026220638.png]]

Answer:
CALCULATE, <mark style="background: #FF5582A6;">ALLSELECTED</mark>.
Explanation:
The tricky thing here is that the report contains a report-level filter for Products and you need to calculate all sales (for all products) for the divisor. So here's both functions' definitiond from dax.guide: 
* ALLSELECTED: Returns all the rows in a table, or all the values in a column, ignoring any filters that might have been applied inside the query, ***but keeping filters that come from outside***. 
* ALL: Returns all the rows in a table, or all the values in a column, ignoring any filters that might have been applied.
The key point is: The measure must respect the report-level filter when calculating the total.
Therefore, I think it should be ALLSELECTED.


48 (T2, Q55)
You have a Power BI data model that analyzes product sales over time. The data model contains the following tables:
![[Pasted image 20231026221147.png]]
A one-to-many relationship exists between the tables.  
The auto date/time option for the data model is enabled.  
***You need to reduce the size of the data model while maintaining the ability to analyze product sales by month and quarter.***  
Which two actions should you perform? Each correct answer presents part of the solution:

- A. Create a relationship between the Date table and the Sales table.
- B. Disable the auto date/time option.
- C. Create a Date table and select Mark as Date Table.
- D. Disable the load on the Date table.
- E. Remove the relationship between the Product table and the Sales table.

Answer:
A. and C.
Explanation:
According to [this M source](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-date-tables), <mark style="background: #FFF3A3A6;">marking a table as a Date Table automatically removes the auto-generated date table</mark>.


