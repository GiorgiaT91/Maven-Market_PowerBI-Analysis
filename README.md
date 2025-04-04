# Maven Market Project - Power BI Analysis

| |
|:---:|
|  |


## Introduction to the Project
In completion of the **Microsoft Power BI Desktop for Business Intelligence** course on ***Udemy***, I analyzed data from Maven Market, a multi-national grocery chain with locations in Canada, Mexico and the United States.

---

## Data Source
The datasets were provided within the course and includes tables containing information on Transactions, Returns, Customers, Products, Regions, Stores and Calendar.

Below is an overview of the key tables in the database and their descriptions:

| Table       | Description                                           |
|-------------|-------------------------------------------------------|
| Transactions | Contains data on transactions between 1997 and 1998  |
| Returns     | Contains data on returns                              |
| Customers   | Contains data on customers, such as socio and demographics attributes |
| Products    | Details of products                                   |
| Regions     | Details of regions, such as sales district            |
| Store       | Details of stores, such as city                       |
| Calendar    | Date for time data analysis                           |

---

## Tools & Scope:
+ Excel: Data Exploration
+ PowerBI: Data Cleaning with Power Query, Data Modeling, DAX functions, Data Visualization

---

## Connecting & Shaping the Data

In this project, several steps were undertaken to prepare and connect data sources in Power BI:

1. **Configuration Settings**: Updated Power BI settings to ensure data integrity, such as turning off auto-detection of relationships and setting the locale for imports.

2. **Data Connection and Preparation**:
   - Connected to various CSV files including Customers, Products, Stores, Regions, Calendar, and Returns.
   - Promoted headers and confirmed data types across tables.
   - Added and formatted columns to enhance data utility, such as merging names and addresses, calculating discount prices, and extracting date components.

3. **Advanced Data Manipulations**:
   - Implemented calculated columns to derive new insights like full name, birth year, and has children status.
   - Utilized statistical tools to analyze product data, performing operations like grouping and calculating average prices.

4. **Data Cleaning**:
   - Managed null values and ensured consistent data formatting.
   - Combined and cleaned transaction data spanning two years from multiple files.

5. **Finalization**:
   - Disabled refresh on certain data tables to optimize performance.
   - Saved the final report as "MavenMarket_Report.pbix" ensuring all tables are correctly linked and accessible within Power BI's relationship and data views.

| |
|:---:|
|  |

---
 
## Creating the Data Model

This section outlines the steps taken to build and refine the data model using the Power BI report developed in the initial phase:

1. **Model Configuration**:
   - Arranged tables in the MODEL view, placing lookup tables above data tables for clarity.
   - Established relationships between Transaction_Data and other tables like Customers, Products, and Stores, ensuring connections were made using appropriate primary and foreign keys.
   - Configured additional relationships, including an inactive relationship and a "snowflake" schema between Stores and Regions.

2. **Relationship Management**:
   - Ensured all relationships were set to one-to-many cardinality with primary keys on the lookup side.
   - Applied one-way filters to maintain clear, unidirectional filter contexts that flow from lookup to data tables.
   - Connected data tables indirectly through shared lookup tables to avoid direct connections that could complicate the model.

3. **Data Privacy and Clarity**:
   - Hid foreign key fields in the report view to prevent confusion and maintain a clean visual space.

4. **Data Formatting and Categorization**:
   - Updated date fields across all tables to "M/d/yyyy" format to ensure consistency.
   - Formatted key financial metrics like retail price and cost to Currency format for better readability and analysis.
   - Categorized geographical data within Customers and Stores tables to enhance geographic reporting capabilities.

5. **Final Touches**:
   - Saved the updated data model as a Power BI (.pbix) file ensuring all configurations and formatting were preserved for reporting and analysis purposes.

---

## Adding DAX Measures

In this phase of the project, numerous calculated columns and DAX measures were added to enhance the data model and provide deeper insights into the dataset:

1. **Calculated Columns**:
   - Added various calculated columns across tables like Calendar, Customers, Products, and Stores to enrich the data attributes. Examples include identifying weekends, calculating current age, customer priorities, price tiers, and years since the last store remodel.

```DAX
Current Age = 
year(today()) - Customers[birth_year]
```

```DAX
House Number = 
left(Customers[customer_address],
search(" ",Customers[customer_address])
-1
)
```

```DAX
Priority = 
if(Customers[homeowner] = "Y" && Customers[member_card] = "Golden", "High", "Standard")
```

```DAX
Short_country = 
UPPER(
    mid(Customers[customer_country],1,3))
```

```DAX
Price_tier = 
if('Products'[product_retail_price] > 3, "High",
if('Products'[product_retail_price] > 1, "Mid", 
"Low")
)
```

```DAX
Year_since_remodel = 
YEAR(TODAY()) - Stores[last_remodel_date].[Anno]
)
```

```DAX
End of Month = 
EOMONTH([date],0)
```

```DAX
Weekend = 
if('Calendar'[Nome del giorno] IN {"Sunday","Saturday"}, "Y", "N")
```

2. **Creation of a Dedicated Measure Table**:
   - For cleanliness and clarity, a dedicated table named "Measure Table" was created to house all the DAX measures. This centralized location aids in managing and organizing measures separately from the data tables.

3. **DAX Measures in Report View**:
   - Developed key performance measures such as "Quantity Sold", "Total Transactions", "Return Rate", "Weekend Transactions", and "Total Profit".
   - Implemented advanced calculations like "YTD Revenue", "60-Day Revenue", "Revenue Target", and measures to track last month's performance metrics.
   - Each measure was carefully formatted (e.g., currency, percentage) and tested with spot checks to ensure accuracy against expected values.

4. **Spot Checks and Validation**:
   - Conducted several spot checks to validate the calculations, such as total sales, return rates, and revenue targets, ensuring the measures reflect accurate and meaningful insights.

| |
|:---:|
|  |

---

## Building the Report

The final phase of the project involved creating and refining the visual components of the Power BI report, ensuring that data insights are clearly communicated:

1. **Setup and Branding**:
   - Renamed the primary tab to "Topline Performance" and added the Maven Market logo to establish brand presence.

2. **Matrix and KPI Visuals**:
   - Inserted a Matrix visual displaying Total Transactions, Total Profit, Profit Margin, and Return Rate by product brand, enhanced with conditional formatting and a visual level Top N filter to focus on the top 30 brands.
   - Added KPI Cards to track Total Transactions, Total Profit, and Total Returns, each compared against the last month's figures, with appropriate color coding and formatting for clarity and emphasis.

3. **Geographic and Time-Series Analysis**:
   - Implemented a Map visual to show Total Transactions by store city, coupled with a slicer for store country to filter the data interactively.
   - Accompanied the map with a Treemap visual to further break down transactions by country and enable drill-up/drill-down through state and city levels.
   - Added a Column Chart to display the Weekly Revenue Trending for the year 1998, using a report level filter.

4. **Target Comparisons**:
   - Placed a Gauge Chart to visually compare Total Revenue against the Revenue Target, fine-tuning the display to highlight performance against goals.

5. **Interactivity and User Engagement**:
   - Adjusted the Matrix interactions to prevent it from influencing the Treemap visual, enhancing user control over data exploration.
   - Set up a bookmark for the "Portland 1000 Sales" scenario, linking detailed notes and actionable insights with a user-friendly navigation button to enhance the interactive report experience.

6. **Documentation and Insights**:
   - Created a dedicated "Notes" page to document additional insights and observations, ensuring all relevant information is accessible and well-organized within the report.

These steps resulted in a dynamic and insightful report that not only highlights key data points but also provides interactive tools for users to explore and understand the data in depth.


| |
|:---:|
|  |

---

## Power BI Dashboard Link
Click the link to view the [Dashboard](https://app.powerbi.com/view?r=eyJrIjoiNGQ2MjIyYjAtYzE0YS00OWQzLWE1NzgtN2I4NTY0N2MxYWU2IiwidCI6ImM5NDI0M2ViLTZmMGUtNDU2Ni1hMjk2LWI1ZGZjOWQyNTczYiIsImMiOjh9&pageName=1458df3c202a09cd95d1).

---

## About me
Hi folks!
I am Giorgia and I am a real passionate about DATA! 

This is my first dashboard in Power BI, I am more than open to criticisms and tips!

Let's stay in contact!

+ 📩: giorgiatagliaferri91@gmail.com
+ 🔗: [Linkedin](https://www.linkedin.com/in/giorgiatagliaferri91/)


