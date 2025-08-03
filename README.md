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


 # Exploratory Data Analysis
 - we started by loading the data and inspecting it
 -<img width="1138" height="579" alt="image" src="https://github.com/user-attachments/assets/26b06c9e-a535-4f20-b27c-16e70464441f" />
 - we then went forward to cleaning the data to check the data types, detect missing values and identifying any potential data quality issues but we had already done this in the etl process
 - <img width="665" height="827" alt="image" src="https://github.com/user-attachments/assets/1b00b53f-1368-459f-940b-cd1ff33b09ac" />
 - we then went forward to interpret the summary where we were able to find that
 - <img width="1071" height="671" alt="image" src="https://github.com/user-attachments/assets/4d3b473f-0d5e-4f6f-83b5-f1ee1743c67e" />
 
 ### descriptive statistics for the numerical features so as to understand the central tendency, spread and distribution of numerical variables
 - <img width="1132" height="720" alt="image" src="https://github.com/user-attachments/assets/53c14345-ae41-4bcc-afa3-42614d6b0550" />
 - Through this we can see the output and insights drawn such as range of values of the different columns
 - We then went forward to visualize the data to help us understand better the data through histograms and boxplots
 - We focused on the key numerical features which are the `price`, `freight_value`, `payment_value`, `review_score` and ` profit_margin`
 - <img width="967" height="549" alt="image" src="https://github.com/user-attachments/assets/0ebd90aa-3d8a-4cc6-9e53-b241c5a6bd99" />
 - Through this we have created histograms and boxplots of each numerical variable to show us the distribution of the data
 - <img width="1102" height="808" alt="image" src="https://github.com/user-attachments/assets/c5ff2d7a-308f-4f2f-92e6-1f48d0e61256" />
 - <img width="1107" height="686" alt="image" src="https://github.com/user-attachments/assets/5b147275-66e8-4dee-b3f7-85f65fb881e0" />
- Through this visualizations we were able to draw insights such as :
- <img width="1167" height="867" alt="image" src="https://github.com/user-attachments/assets/5f17af2c-6c0d-46af-b6e6-ae11a12600be" />
- the overall insights are that
-  1. pricing, payments and shipping costs show diversity and clear outliers
   2. Customer satisfaction is high
   3. profit margins are consistently strong

### Analysis of categorical variables 
- this include `order_status`, `payment_type`, `customer_state`, `seller_state` and `product_category_name_english`
- This categorical variables help us understand distribution patterns, dominant categories and potential relationships
- <img width="827" height="435" alt="image" src="https://github.com/user-attachments/assets/d1ef33a3-8699-4ac8-8136-0b59f35aa416" />
- we decided to create count plots for each categorical variable
- <img width="1072" height="897" alt="image" src="https://github.com/user-attachments/assets/3396af30-342f-4732-9bc5-14279cae5b16" />
- <img width="674" height="489" alt="image" src="https://github.com/user-attachments/assets/f7441b12-1c65-4f6e-97ac-478704fe70e5" />
- Through this we were able to draw some insights which include
- <img width="1161" height="446" alt="image" src="https://github.com/user-attachments/assets/873bbc00-c204-4381-b778-5471e8a3badc" />
- overall insights are that :
- 1. Order Status: Most orders delivered, few canceled.
  2. Payment Type: Credit card dominates.
  3. Customer/Seller State: São Paulo (SP) is the main hub.
  4. Product Category: Health & Beauty is top-selling.
  5. Business is concentrated in certain regions and categories.
  6. Payment and logistics are streamlined.
 
### Bivariate analysis
- In this part we check for the relationships between two variables focusing on
  i. correlation between numerical variables
  ii. comparison of categorical variables with numerical variables
  iii. Detection of patterns or trends
- we began with a correlation heatmap to visualize relationships between numerical features
- <img width="770" height="324" alt="image" src="https://github.com/user-attachments/assets/37a7fd67-4324-4ab3-96c4-1c145c5e3d99" />
- <img width="1071" height="886" alt="image" src="https://github.com/user-attachments/assets/fb041818-6bed-4297-90a5-a7b0756efb23" />
- We were able to draw some insights from this which are
- <img width="1175" height="711" alt="image" src="https://github.com/user-attachments/assets/245e8d6d-3f21-471b-b0cb-407265acf98a" />
- overall insights are :
- 1. Some features are highly correlated (may need to drop/reduce for modeling).
  2. Price and freight are linked.

### Categorical vs Numerical variables
-This helps identify **how categories influence numerical metrics** such as price, freight value, payment value, and review scores.
- <img width="942" height="799" alt="image" src="https://github.com/user-attachments/assets/528b3422-8090-49ee-ac07-730a14cb2eaf" />
- we created boxplots for price/freight value by category and state
- This were the output of the boxplots
- <img width="1007" height="601" alt="image" src="https://github.com/user-attachments/assets/7448ddba-e323-4076-9855-4785c762dea8" />
The boxplot for **Price vs Product Category** provides insights into how prices vary across the top 15 product categories.

- **Key Observations:**
  - Categories like **watches_gifts** and **industry_commerce_and_business** exhibit **higher median prices**, suggesting they are premium or specialized products.
  - **Computers** and **home_appliances_2** also show relatively high prices, along with several outliers indicating a few extremely expensive items.
  - **Cool_stuff** and **office_furniture** have **lower median prices**, highlighting these categories as more affordable.
  - The **presence of many outliers** across categories implies significant price diversity within the same category.

- <img width="999" height="616" alt="image" src="https://github.com/user-attachments/assets/87b8dc07-bad5-45fe-8aa1-43dcb8c01087" />

The boxplot for **Freight Value vs Product Category** reveals shipping cost variations among product categories.

- **Key Observations:**
  - Categories like **kitchen_dining_laundry_garden_furniture**, **garden_tools**, and **furniture_living_room** have **higher median freight costs**, possibly due to larger or heavier items.
  - **Fashion_male_clothing** and **books_imported** tend to have **lower freight costs**, reflecting smaller and lighter products.
  - Outliers with **very high freight values** suggest occasional special shipping requirements or long-distance deliveries.
    
- <img width="1034" height="624" alt="image" src="https://github.com/user-attachments/assets/ef6fa699-32c6-4b04-90c2-4964bcd08018" />
The boxplot for **Freight Value vs Customer States** helps to understand regional differences in shipping costs.

- **Key Observations:**
  - States like **ce**, **m**, **to**, and **pa** have **higher median freight values**, suggesting that deliveries to these areas are costlier—likely due to distance or logistics.
  - Most states cluster around **freight values between 20 and 30**, indicating stable shipping costs for the majority of customers.
  - Several **outliers** reflect shipments with abnormally high costs.

- <img width="1007" height="637" alt="image" src="https://github.com/user-attachments/assets/4c4846f1-462c-432e-91bb-ba4cc2b641f4" />
The boxplot for **Freight Value vs Seller States** examines shipping costs from different seller regions.

- **Key Observations:**
  - Sellers in **pe**, **es**, and **ce** incur **higher median freight values**, which may indicate these locations are farther from major customer bases or involve higher handling costs.
  - Most seller states have freight costs within a narrow range (20–35), showing general uniformity in shipping rates.
  - Some states like **se** and **pi** display **outliers** with extremely high freight costs, possibly for large shipments or distant deliveries.
 
  The boxplot for **Freight Value vs Seller States** examines shipping costs from different seller regions.

- **Key Observations:**
  - Sellers in **pe**, **es**, and **ce** incur **higher median freight values**, which may indicate these locations are farther from major customer bases or involve higher handling costs.
  - Most seller states have freight costs within a narrow range (20–35), showing general uniformity in shipping rates.
  - Some states like **se** and **pi** display **outliers** with extremely high freight costs, possibly for large shipments or distant deliveries.























---
