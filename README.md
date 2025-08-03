# DSA2040A_DataMining_Group-6
End-to-end data mining project analyzing inpatient healthcare costs in the USA. Includes ETL, exploratory analysis, mining techniques, and insights to uncover cost patterns and drivers in hospitalization data.
# READ-ME file 
# Student Responsible : Levin913 and Angela
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

## Transformation
- This part entails changing the datasets into the required formats so as to be able to draw meaningful insights from it.
- We started by converting the date time columns into datetime type to enable filtering
- <img width="1130" height="886" alt="image" src="https://github.com/user-attachments/assets/0c28018d-5c85-4533-8491-1e8aa1fb6021" />
- This was first done by checking if the columns actually appear in the several datasets and then changing them into the dateime format

- Since we wanted to look at only the sales of the last 3 months, we had to do some filtering
- <img width="975" height="853" alt="image" src="https://github.com/user-attachments/assets/7d70915d-c225-4865-878c-1aa1d3399155" />
- <img width="802" height="272" alt="image" src="https://github.com/user-attachments/assets/9362fde7-7e2b-4903-9298-2f7e885321f6" />
- We started by first finding the latest date in the orders table and calculate the date three months before that. Filtering the orders to keep only those within the last three months. Get the order IDs from these recent orders. Filter related tables (order items, payments, reviews) to keep only records linked to these recent orders. Filter customers to keep only those who made recent orders. Filter products to keep only those that appear in recent order items. Filter sellers to keep only those involved in recent order items. Filter product category translations to keep only categories present in recent products. Filter geolocation data to keep only zip codes for the filtered customers and sellers.
- This was done to ensures all tables are temporally consistent (only recent data). Keep only relevant records for analysis, reducing noise and improving performance. Maintain relational integrity across all tables for downstream merging and analysis.

- We then went on to merge the filtered data based on the recent 3 months
- This was done to creates a single, unified DataFrame with all relevant information for each recent order and prepares the data for analysis, modeling, or visualization by having all features in one place.
- <img width="964" height="890" alt="image" src="https://github.com/user-attachments/assets/7176bfb5-07ec-4c4f-bf8e-5317eecb51a6" />
- As a result, a unified dataset with 11,777 entries and 44 columns was created, containing detailed transaction-level information suitable for in-depth analysis. Temporal coverage in this final dataset ranges from 2018-07-17 to 2018-10-17. Missing values in some columns reflect real-world data gaps such as unreviewed orders or incomplete delivery records.

### Cleaning the merged datasets
<img width="1139" height="869" alt="image" src="https://github.com/user-attachments/assets/43d64841-6281-418e-8af9-7f2635df4786" />
- we checked if there are any duplicates and found none but we were able to find that there were several missing values and we were able to get the percenatage of missing values in each column
- we then removed columns with more than 50 % missing values
- <img width="499" height="110" alt="image" src="https://github.com/user-attachments/assets/77f5a260-31f2-4ca7-8733-5f4c47231b94" />
- we then went on forward to deal with the others
- we began by filling date time columns with a related datetime column if known, else we used forward fill
- and also filling missing numeric values with  mean or median using skewness check
- <img width="893" height="661" alt="image" src="https://github.com/user-attachments/assets/0e48fe04-3bcd-467b-ad66-11112eba1343" />
- we also filled missed categorical values with mode
- <img width="852" height="295" alt="image" src="https://github.com/user-attachments/assets/399e8861-3e8d-4869-b3cf-b48617a28cc9" />

- We were also able to add more columns to enable us derive more insights from the data
- we added a profit margin column that shows how much of the product price is left after subtracting the freight costs
- <img width="952" height="620" alt="image" src="https://github.com/user-attachments/assets/6f41a7cf-7c93-4a1d-a2a2-28468f0ce055" />
- we also added the purchase frequency per customer which shows how often a customer makes a purchase
- <img width="1161" height="353" alt="image" src="https://github.com/user-attachments/assets/a5ea9be9-9500-4e08-827d-593bd6c80d8f" />

- we also handled outliers in the dataset to reduce noise in the dataset and keeping extreme values from skewwing models and visualizations
- <img width="1017" height="809" alt="image" src="https://github.com/user-attachments/assets/81e7a8fb-2ea7-43a7-85b5-5de4df20e183" />
- it was done by calculating every percentile in the dataset and then capping any value below the lower bound to the lower bound, and any value above the upper bound to the upper bound

- we also standardized formats so that the dataset while have consistent formats through out
- <img width="935" height="812" alt="image" src="https://github.com/user-attachments/assets/a49a0e3b-6a5b-49b0-b03d-da4ce9b84810" />
- this prevents errors in merging filtering and grouping

  ## Loading
  - we then were able to load the cleaned dataset into its own Parquet file and then preview it to know if it was a success
  <img width="1166" height="782" alt="image" src="https://github.com/user-attachments/assets/d08d3774-377f-4aef-8118-d3f560440e9a" />
- #### Saving as Parquet:
We created a new directory called `data/final/` if it didn't already exist using `os.makedirs()` with `exist_ok=True`.

The DataFrame was then saved as a Parquet file (`loaded_data.parquet`) using `df.to_parquet()`. This format is preferred for analytics workflows due to its:

- Smaller file size (compared to CSV)  
- Faster read/write times  
- Schema support and optimized columnar storage  








- 






---
