
# Candy Market Share

Dashboard Link : https://app.powerbi.com/view?r=eyJrIjoiYWU5ZWFiNjEtNGYwNC00OTdjLWJlNTUtNjcxMmQ3NGMwODRmIiwidCI6IjQ2NTRiNmYxLTBlNDctNDU3OS1hOGExLTAyZmU5ZDk0M2M3YiIsImMiOjl9

Candy Sales Analytics Project

Project Description

This project focuses on analyzing candy sales data to provide key business insights. The objective is to clean, store, and analyze the data to generate actionable reports. By leveraging SQL for data manipulation and Power BI for visualization, the project demonstrates expertise in data storytelling and dashboard creation.

# Steps Data Analytics
Collection > Cleaning > Storage > Explore > Analyzing > Report 

## 1. Collection

Access the data through the FP20 November Challenge link.

Download the Excel file containing sales data.

## 2. Cleaning and Storage

Cleaning: Ensure the dataset is cleaned by handling missing or inconsistent values.

Time Columns: The dataset includes separate columns for Month and Year. These are combined into a new column "Date" in the format MM-YYYY using the formula:

> Date = FORMAT(DATE('Table'[Year],'Table'[Month],1),"MM-YYYY")

Create a Calendar Table: Generate a calendar table for continuous time series analysis since the data in the original table is discontinuous. Use the following DAX formula:
```DAX
Calendar =
ADDCOLUMNS(
    CALENDARAUTO(),
     "Year", YEAR([Date]),
     "Month", FORMAT([Date], "mmmm"),
     "Month number", MONTH([Date]),
     "Quarter", FORMAT([Date],"\QQ")
)
```
## 3. Exploration and Metrics Calculation (Using SQL)

Calculate total sales volume in EUR:

```SQL
SELECT SUM([Sales Volume in EUR]) AS Total_Sales_EUR
FROM Data;
```

Calculate total sales volume in KG:
```SQL
SELECT SUM([Sales Volume in KG]) AS Total_Sales_KG
FROM Data;
```
## 4. Slicer for KPI Selection

Create a new table named "Select KPI" with the necessary metrics to display dynamically in the slicer.

Add a slicer using the following DAX formulas:

Selected KPI:
```DAX

Selected KPI = MIN('Select Metrics'[KPI_ID])
```
Selected Value:
```DAX
Selected Value =
SWITCH('Select Metrics'[Selected KPI],
1, SUM('Data'[Sales Volume in KG]),
2, SUM('Data'[Sales Volume in EUR])
)
```
## 5. Growth Analysis

Calculate the percentage growth of sales:

Growth % = (Current Value - Last Period Value) / Last Period Value

Display this value as a percentage.

## 6. Best Month Identification

Identify the month with the highest sales:

Best Month | Sales =
CONCATENATEX(
    TOPN(
        1,
        FILTER(
            Data,
            [SUM sales EUR] <> BLANK()
        ),
    [SUM sales EUR]
    ),
    Data[MONTH] & " | € " & [SUM sales EUR],
    UNICHAR(10),
    [SUM sales EUR], DESC
)

## 7. Analyzing and Reporting

Apply data storytelling techniques to create meaningful charts in Power BI.

Include key metrics such as total sales in EUR, total sales in KG, growth %, and best month performance.

Choose appropriate visualizations (e.g., bar charts, line graphs, KPIs) to present data effectively.

Use slicers to allow dynamic filtering of the data.

Final Deliverables

A comprehensive Power BI dashboard showing:

Total sales metrics

Growth trends

Best-performing months

Dynamic KPI slicers

A public link to the Power BI report.

A downloadable PDF version of the report for offline sharing.

This project demonstrates proficiency in data analysis, SQL, DAX, and Power BI, with a strong emphasis on creating user-friendly and insightful dashboards.

