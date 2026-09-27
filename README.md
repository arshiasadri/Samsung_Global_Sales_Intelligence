# Samsung Global Sales Intelligence Dashboard

### Power BI | Data Analytics | DAX | Power Query | REST API

An interactive business intelligence dashboard designed to analyze international sales performance, revenue trends, product categories, and regional performance through a unified USD-based reporting model.

This project demonstrates an end-to-end Power BI analytics workflow, including data preparation, dimensional modeling, currency conversion using a public REST API, DAX measure development, and interactive dashboard design.

---

## Dashboard Preview

![Samsung Global Sales Intelligence Dashboard](assets/dashboard.png)

*Interactive sales intelligence dashboard developed in Microsoft Power BI.*

---

## Project Overview

The **Samsung Global Sales Intelligence Dashboard** is a portfolio project focused on transforming multi-currency sales data into meaningful business insights.

The dashboard provides a consolidated view of sales performance across multiple countries, regions, cities, and product categories.

By integrating exchange-rate data from the Frankfurter public API, sales transactions denominated in different currencies are converted into USD, enabling more consistent cross-country revenue analysis.

The project simulates an international retail analytics environment inspired by Samsung Electronics' product portfolio.

> **Data Disclaimer:** This is an educational and portfolio project. The sales transactions and customer records are synthetic and do not represent actual Samsung Electronics sales, customers, or internal company data. Product names are used for illustrative purposes.

---

## Business Objectives

The main objectives of this project are to:

* Monitor overall sales performance through key performance indicators (KPIs).
* Analyze monthly revenue trends and year-over-year growth.
* Compare revenue performance across geographic regions and cities.
* Identify product categories contributing to total revenue.
* Standardize multi-currency sales reporting using USD.
* Develop an interactive dashboard to support data-driven business analysis.

---

## Key Features

### 1. Sales Performance KPIs

The dashboard includes key metrics for monitoring business performance:

| KPI                       | Description                              |
| ------------------------- | ---------------------------------------- |
| Total Revenue             | Aggregated sales revenue                 |
| Average Order Value (AOV) | Average revenue per order                |
| Total Orders              | Number of distinct sales orders          |
| YoY Revenue Growth        | Year-over-year revenue growth percentage |

### 2. Time Intelligence Analysis

* Monthly revenue trend analysis.
* Previous-month revenue comparison.
* Month-over-month (MoM) growth.
* Previous-year revenue comparison.
* Year-over-year (YoY) growth analysis.

### 3. Geographic Sales Analysis

Analyze revenue performance across:

* Regions
* Countries
* Cities

The geographic visuals provide an overview of revenue distribution and allow users to explore differences in sales performance across markets.

### 4. Product Category Analysis

Compare revenue contributions across product categories, including:

* Mobile
* Home Appliance
* TV
* Tablet
* Monitor
* Wearable
* Audio

### 5. Interactive Filtering

The dashboard includes interactive date filtering and Power BI cross-filtering, allowing users to explore sales performance across different periods and business dimensions.

---

## Data Model

The project uses a **Star Schema** data model to organize transactional data and descriptive dimensions.

| Table         | Description                                                                 |
| ------------- | --------------------------------------------------------------------------- |
| FactSales     | Sales transactions, quantities, prices, discounts, and currency information |
| DimProduct    | Product names, categories, subcategories, and pricing information           |
| DimCustomer   | Customer attributes and customer segments                                   |
| DimLocation   | Geographic attributes, including country, region, city, and currency        |
| DimDate       | Calendar table used for time intelligence calculations                      |
| ExchangeRates | Historical exchange-rate data retrieved from the Frankfurter API            |
| Measures      | Dedicated table for organizing DAX measures                                 |

### Relationships

The model follows a one-to-many relationship structure between dimension tables and the sales fact table.

* DimProduct → FactSales
* DimCustomer → FactSales
* DimLocation → FactSales
* DimDate → FactSales

The ExchangeRates data is merged into the sales transactions during Power Query transformations to support currency conversion.

---

## Currency Conversion & REST API Integration

One of the main technical components of this project is the integration of an external exchange-rate API.

**API Provider:** [Frankfurter](https://frankfurter.dev/)

Historical exchange-rate data is retrieved through the Frankfurter public API and integrated into the Power Query workflow.

### Currency Conversion Logic

The exchange-rate API provides currency rates relative to USD.

For example:

`1 USD = 0.86 EUR`

To convert a sales transaction from EUR to USD:

`Revenue USD = Revenue in EUR / EUR per USD exchange rate`

The conversion logic is applied to each transaction:

`Revenue USD = Quantity × Unit Price × (1 - Discount) / Exchange Rate`

USD transactions use an exchange rate of 1.

This approach standardizes revenue reporting across the supported currencies.

---

## DAX Measures

The project includes DAX measures for sales analysis and time intelligence.

### Total Revenue

```dax
Total Revenue =
SUMX(
    FactSales,
    FactSales[Quantity] *
    FactSales[UnitPrice] *
    (1 - FactSales[Discount])
)
```

### Total Orders

```dax
Total Orders =
DISTINCTCOUNT(FactSales[OrderID])
```

### Average Order Value

```dax
Average Order Value =
DIVIDE(
    [Total Revenue],
    [Total Orders]
)
```

### Revenue Previous Month

```dax
Revenue Previous Month =
CALCULATE(
    [Total Revenue],
    DATEADD(
        DimDate[Date],
        -1,
        MONTH
    )
)
```

### Month-over-Month Growth

```dax
MoM Growth % =
DIVIDE(
    [Total Revenue] - [Revenue Previous Month],
    [Revenue Previous Month]
)
```

### Revenue Previous Year

```dax
Revenue Previous Year =
CALCULATE(
    [Total Revenue],
    DATEADD(
        DimDate[Date],
        -1,
        YEAR
    )
)
```

### Year-over-Year Growth

```dax
YoY Growth % =
DIVIDE(
    [Total Revenue] - [Revenue Previous Year],
    [Revenue Previous Year]
)
```

*Note: The measures above illustrate the original sales calculations. The USD-converted revenue column is also available for standardized reporting.*

---

## Tools & Technologies

| Technology         | Purpose                                                     |
| ------------------ | ----------------------------------------------------------- |
| Microsoft Power BI | Dashboard development and data visualization                |
| Power Query        | Data cleaning, transformation, merging, and API integration |
| DAX                | KPI calculations and time intelligence                      |
| REST API           | Retrieval of historical exchange rates                      |
| Excel              | Dataset preparation and source data management              |
| Star Schema        | Dimensional data modeling                                   |

---

## Dataset Information

The project uses a synthetic dataset created for educational and analytical purposes.

The dataset includes:

* 5,000 sales transactions
* 500 customer records
* 12 illustrative products
* 10 geographic locations
* Multiple transaction currencies
* Sales dates covering January 2023 through December 2025

The data is structured into fact and dimension tables to support relational modeling and interactive reporting.

---

## Project Structure

```text
Samsung-Global-Sales-Intelligence/
│
├── assets/
│   └── dashboard.png
│
├── data/
│   └── Samsung_Global_Sales_Intelligence_Dataset.xlsx
│
├── Samsung_Global_Sales_Intelligence.pbix
│
└── README.md
```

*The structure above is the recommended repository layout. Adjust the filenames to match the files included in your repository.*

---

## Key Learning Outcomes

Through this project, I practiced and developed skills in:

* Designing a relational data model using a Star Schema.
* Cleaning and transforming data using Power Query.
* Creating calculated columns and DAX measures.
* Applying time intelligence functions for business reporting.
* Integrating a public REST API into a Power BI workflow.
* Converting multi-currency transactions into a standardized reporting currency.
* Designing interactive dashboards for business intelligence and data analysis.

---

## Author

**Arshia Sadri**

Computer Science Student | Aspiring Data Analyst

* GitHub: [@arshiasadri](https://github.com/arshiasadri)

---

*This project was developed as part of my data analytics and business intelligence portfolio.*
