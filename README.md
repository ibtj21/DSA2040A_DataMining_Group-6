# DSA2040A_DataMining_Group-6
End-to-end data mining project analyzing inpatient healthcare costs in the USA. Includes ETL, exploratory analysis, mining techniques, and insights to uncover cost patterns and drivers in hospitalization data.
We started the project with the ETL process. We picked the e-commerce dataset in Olist and performed the ETL process on it

# 🛒 Olist E-commerce Dataset: ETL Project

**Author**: Hana  
**Notebook**: `1_extract_transform.ipynb`  
**Objective**: Perform Extract and Transform operations on Brazil’s largest e-commerce platform dataset (Olist), focusing on the last 3 months of sales.

## 📦 Dataset Overview

The Olist dataset consists of **relational CSV files** representing various aspects of Brazil’s online marketplace.

### 📁 Key Files Used

| File Name | Description |
|----------|-------------|
| `olist_orders_dataset.csv` | Order metadata (status, timestamps) |
| `olist_order_items_dataset.csv` | Products per order |
| `olist_products_dataset.csv` | Product details (name, category, dimensions) |
| `olist_order_payments_dataset.csv` | Payment method and amount |
| `olist_order_reviews_dataset.csv` | Star ratings and text reviews |
| `olist_customers_dataset.csv` | Customer location info |
| `olist_sellers_dataset.csv` | Seller location info |
| `olist_geolocation_dataset.csv` | Postal code coordinates |
| `product_category_name_translation.csv` | English translations of product categories |

- The data was relational because the tables are linked via keys like `order_id`, `product_id` and `customer_id` making it ideal for multi-table analysis.

## Extraction 
-Data was extracted from the nine datasets
<img width="770" height="345" alt="image" src="https://github.com/user-attachments/assets/cb6c404f-5e17-4554-8e7c-4b5e9a54de96" />
- It was then inspected for the first time diplaying the first few rows of each dataset. it first created a dictionary named datasets and then looped through each dataset
- <img width="792" height="888" alt="image" src="https://github.com/user-attachments/assets/247f66ef-f446-4e84-88d6-43e125687921" />
- its structure was then inspected through the same way of creating a dictionary first looping through it as the structure is inspected and printed
- <img width="633" height="887" alt="image" src="https://github.com/user-attachments/assets/925b735d-81ea-453f-b909-b576df4ea25e" />
- Through the output of the initial inspection we were able to draw that
- ___
### *B. Initial Inspection Observations*

From the initial `.info()` checks across the Olist datasets, we observe the following:

- **Data Volume**: Most datasets contain tens of thousands of entries, with `geolocation` being the largest (~1 million rows) and `category translation` the smallest (71 rows).
- **Data Types**: Many columns are stored as `object` type, particularly those representing IDs and dates. This may require type conversion (e.g., to `datetime`) during preprocessing.
- **Missing Data**:
  - The `orders` dataset has some missing timestamps in delivery-related fields.
  - The `products` dataset has a few missing values in product attributes.
  - The `reviews` dataset has many missing values in comment titles and messages, which may be optional fields.
- **Relational Structure**: 
  - Shared keys like `order_id`, `product_id`, `customer_id`, and `seller_id` across tables suggest strong relational integrity.
  - This supports potential joins to create enriched views for further analysis.

These findings guide us to perform data cleaning and transformations in the upcoming ETL steps.
____





---
