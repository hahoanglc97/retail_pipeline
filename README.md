# Retail Project

## Objective


## Prerequisites
- Docker
- Astro CLI
- Airflow
- DBT Cosmos
- Soda
- Google Cloud Storage
- Bigquery
- Metabase

## Dataset
https://www.kaggle.com/datasets/tunguz/online-retail
| Column    | Description |
| -------- | ------- |
| InvoiceNo  | Invoice number. Nominal, a 6-digit integral number uniquely assigned to each transaction. If this code starts with letter 'c', it indicates a cancellation.|
| StockCode | Product (item) code. Nominal, a 5-digit integral number uniquely assigned to each distinct product.|
| Description | Product (item) name. Nominal.|
| Quantity | The quantities of each product (item) per transaction. Numeric. |
| InvoiceDate | Invice Date and time. Numeric, the day and time when each transaction was generated. |
| UnitPrice | Unit price. Numeric, Product price per unit in sterling. |
| CustomerID | Customer number. Nominal, a 5-digit integral number uniquely assigned to each customer. |
| Country | Nominal |

## Data model
![Alt text](/data_model.png "Data Model")


## Pipeline
![Alt text](/pipeline.png "Pipeline")

1. Create task airflow ingest raw data (file csv) into Google Cloud Storage.
2. Load data from raw files placed in GCS into a table that stores raw data in Bigquery.
3. Run task data quality check with soda to make sure raw data stored correctly in Bigquery. That will check the required column and column type.
4. Next task with DBT, it will transform raw data to save in fact table and dimension table in Bigquery. We will have 3 dimensions table:
    - customer
    - datetime
    - product

    and 1 fact table: invoices.

5. Then run task check to make sure the tranformations are correct.
6. Aftert that, we get analytics from tranformed data with DBT. It will create 3 report tables:         
    - customer_invoices: Report total invoices and total revenue coming from customers in different countries.
    - product_invoices: Report total quantity sold of products.
    - yser_invoices: Report number invoices and total revenue by month every year.
7. Finally, task run check quality of soda for data analytics store in table report.
8. Build dashboard report with metabase.

![Alt text](/airflow_pipeline.png "Airflow Pipeline")

## Dashboard

1. Total revenue per month
![Alt text](/revenue_per_month.png "Total revenue per month") 

2. Top 10 product by quantity sold
![Alt text](/top_product.png "Top 10 product by quantity sold")

3. Primary markets
![Alt text](/primary_markets.png "Primary markets")

4. Dashboard
![Alt text](/dashboard.png "Dashboard")


```
Read STEP_IMPL.md to implement step by step this project
```