# Enterprise Sales & Subscription Analytics Model

An end-to-end Power BI data model designed to track physical product sales alongside recurring software subscriptions. Built using a strict Star Schema architecture to ensure high-performance DAX calculations and unambiguous cross-filtering.

## 📊 Project Overview
This project demonstrates advanced data modeling techniques in Power BI, specifically handling the complexities of tracking Active and Churned Monthly Recurring Revenue (MRR) using active and inactive relationships. 

It is saved using Power BI Developer Mode (`.pbip`) to expose the underlying metadata, DAX formulas, and structure for version control and CI/CD integration.

## 🏗️ Data Architecture
The data model adheres to best practices for dimensional modeling:
* **Star Schema Design:** All relationships are strictly 1-to-Many (1:*), flowing unidirectionally from Dimension tables to Fact tables to prevent ambiguous paths.
* **Centralized Date Dimension:** A dedicated `Dim_Date` table generated via DAX overlays the entire model, allowing synchronous time-intelligence filtering across multiple distinct transaction dates (`Order_Date`, `Start_Date`, and `End_Date`).
* **Entity Resolution:** Linked physical sales and digital subscriptions via a unified `Customer_ID` primary key, resolving many-to-many date cardinality conflicts.

## 🧮 Advanced DAX & Measures
All measures are organized within a dedicated `_Medidas` table. Key calculations include:

* **Subscription MRR:** Filters context dynamically to isolate revenue from active users.
* **Churned Revenue (Inactive Paths):** Utilizes the `USERELATIONSHIP` function to temporarily activate a dashed secondary relationship between `Dim_Date` and `Fact_Subscriptions[End_Date]`, allowing precise calculation of lost revenue without breaking the primary timeline.
* **Dynamic Profitability:** Row-context iteration using `SUMX` and `RELATED` to calculate real-time profit margins based on relational product costs.

## 📷 Dashboard Previews
*(Insert a high-quality screenshot of your Dashboard here)*
> **Figure 1:** Interactive breakdown of MRR, Churned Revenue, and Total Sales, sliced by region and product category.

*(Insert a high-quality screenshot of your Data Model / Gray Canvas here)*
> **Figure 2:** The underlying Star Schema, showcasing the 1:* unidirectional relationships and the inactive relationship required for the Churned Revenue DAX calculation.

## 🚀 How to Run Locally
1. Clone this repository.
2. Ensure you have the latest version of [Power BI Desktop](https://powerbi.microsoft.com/) installed with "Power BI Project (.pbip) save option" enabled in Preview Features.
3. Open the `.pbip` file to view the model, DAX, and report canvas.
