#  DSA2040A_DataMining_Group-6

##  Overview
This project is an **end-to-end data analytics and mining pipeline** applied to the **Olist E-commerce dataset**.  
The workflow spans from **data extraction and transformation (ETL)** to **exploratory analysis**, **interactive dashboards**, and **data mining** to uncover meaningful patterns and insights.

---

##  Team & Responsibilities  
- **ETL Phase Lead:** Hana Gashaw
- **EDA Phase leads:** Trizzah Nzioka & Ted Korir
- **Data Mining leads:** Selmah Tzindori & Hana Gashaw
- **Dashboard lead:** Selmah Tzindori
- **Documentation:** Levin Ekuam &Angela Irungu
 

---

## 🛠️ Project Workflow
1. **ETL Process** – Data extraction, cleaning, and transformation.  
2. **Exploratory Data Analysis (EDA)** – Identifying trends and relationships.  
3. **Dashboards** – Building interactive dashboards for visualization.  
4. **Data Mining** – Discovering hidden patterns using analytical techniques.  

---

## 🗂️ Olist E-commerce Dataset

The Olist dataset represents real-world data from **Brazil’s largest e-commerce platform**.  
It consists of **relational CSV files** capturing transactions, customer behavior, and seller performance.

### 📌 Dataset Overview
- **Source**: Olist (public dataset)  
- **Focus**: Last 3 months of sales  
- **Structure**: Multiple tables linked via keys like `order_id`, `product_id`, and `customer_id`.

---

### 📄 Key Files Used

| File Name                            | Description |
|-------------------------------------|-------------|
| `olist_orders_dataset.csv`          | Order metadata (status, timestamps) |
| `olist_order_items_dataset.csv`     | Products per order |
| `olist_products_dataset.csv`        | Product details (name, category, dimensions) |
| `olist_order_payments_dataset.csv`  | Payment method and amount |
| `olist_order_reviews_dataset.csv`   | Star ratings and text reviews |
| `olist_customers_dataset.csv`       | Customer location info |
| `olist_sellers_dataset.csv`         | Seller location info |
| `olist_geolocation_dataset.csv`     | Postal code coordinates |
| `product_category_name_translation.csv` | English translations of product categories |

---

## 🧹 ETL Phase Details
**Notebook:** `1_extract_transform.ipynb`  
**Objective:** Perform Extract and Transform operations on the Olist dataset, preparing it for analysis by:  
- Selecting data from the last 3 months of sales.  
- Cleaning missing values and inconsistencies.  
- Merging relational tables for seamless analysis.  

---

## 🚀 Next Steps
- **EDA**: Analyze and visualize data distributions and relationships.  
- **Dashboards**: Develop interactive tools to present insights dynamically.  
- **Data Mining**: Apply clustering, association, and predictive techniques to uncover deeper patterns.

---

## ✅ Conclusion
The ETL process successfully prepared the dataset, ensuring it is clean, structured, and ready for subsequent **EDA, dashboards, and data mining** phases.

---

## Extraction 
-Data was extracted from the nine datasets

<img width="770" height="345" alt="image" src="https://github.com/user-attachments/assets/cb6c404f-5e17-4554-8e7c-4b5e9a54de96" />
- It was then inspected for the first time, displaying the first few rows of each dataset. It first created a dictionary named datasets and then looped through each dataset
- <img width="792" height="888" alt="image" src="https://github.com/user-attachments/assets/247f66ef-f446-4e84-88d6-43e125687921" />
- its structure was then inspected in the same way as creating a dictionary, first looping through it as the structure is inspected and printed
- <img width="633" height="887" alt="image" src="https://github.com/user-attachments/assets/925b735d-81ea-453f-b909-b576df4ea25e" />
- Through the output of the initial inspection, we were able to draw that
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
- This part entails changing the datasets into the required formats so as to be able to draw meaningful insights from them.
- We started by converting the date time columns into datetime type to enable filtering
- <img width="1130" height="886" alt="image" src="https://github.com/user-attachments/assets/0c28018d-5c85-4533-8491-1e8aa1fb6021" />
- This was first done by checking if the columns actually appear in the several datasets and then changing them into the datetime format

- Since we wanted to look at only the sales of the last 3 months, we had to do some filtering
- <img width="975" height="853" alt="image" src="https://github.com/user-attachments/assets/7d70915d-c225-4865-878c-1aa1d3399155" />
- <img width="802" height="272" alt="image" src="https://github.com/user-attachments/assets/9362fde7-7e2b-4903-9298-2f7e885321f6" />
- We started by first finding the latest date in the orders table and calculating the date three months before that and filtering the orders to keep only those within the last three months. Get the order IDs from these recent orders. Filter related tables (order items, payments, reviews) to keep only records linked to these recent orders. Filter customers to keep only those who made recent orders. Filter products to keep only those that appear in recent order items. Filter sellers to keep only those involved in recent order items. Filter product category translations to keep only categories present in recent products. Filter geolocation data to keep only zip codes for the filtered customers and sellers.
- This was done to ensure all tables are temporally consistent (only recent data). Keep only relevant records for analysis, reducing noise and improving performance. Maintain relational integrity across all tables for downstream merging and analysis.

- We then went on to merge the filtered data based on the recent 3 months
- This was done to create a single, unified DataFrame with all relevant information for each recent order and to prepares the data for analysis, modeling, or visualization by having all features in one place.
- <img width="964" height="890" alt="image" src="https://github.com/user-attachments/assets/7176bfb5-07ec-4c4f-bf8e-5317eecb51a6" />
- As a result, a unified dataset with 11,777 entries and 44 columns was created, containing detailed transaction-level information suitable for in-depth analysis. Temporal coverage in this final dataset ranges from 2018-07-17 to 2018-10-17. Missing values in some columns reflect real-world data gaps such as unreviewed orders or incomplete delivery records.

### Cleaning the merged datasets
<img width="1139" height="869" alt="image" src="https://github.com/user-attachments/assets/43d64841-6281-418e-8af9-7f2635df4786" />
- We checked if there are any duplicates and found none, but we were able to find that there were several missing values, and we were able to get the percentage of missing values in each column
- We then removed columns with more than 50 % missing values
- <img width="499" height="110" alt="image" src="https://github.com/user-attachments/assets/77f5a260-31f2-4ca7-8733-5f4c47231b94" />
- We then went on to deal with the others
- We began by filling datetime columns with a related datetime column if known, else we used forward fill
- and also filling missing numeric values with the  mean or median using the skewness check
- <img width="893" height="661" alt="image" src="https://github.com/user-attachments/assets/0e48fe04-3bcd-467b-ad66-11112eba1343" />
- We also filled in the missing categorical values with the mode
- <img width="852" height="295" alt="image" src="https://github.com/user-attachments/assets/399e8861-3e8d-4869-b3cf-b48617a28cc9" />

- We were also able to add more columns to enable us to derive more insights from the data
- We added a profit margin column that shows how much of the product price is left after subtracting the freight costs
- <img width="952" height="620" alt="image" src="https://github.com/user-attachments/assets/6f41a7cf-7c93-4a1d-a2a2-28468f0ce055" />
- We also added the purchase frequency per customer, which shows how often a customer makes a purchase
- <img width="1161" height="353" alt="image" src="https://github.com/user-attachments/assets/a5ea9be9-9500-4e08-827d-593bd6c80d8f" />

- We also handled outliers in the dataset to reduce noise in the dataset and keep extreme values from skewing models and visualizations
- <img width="1017" height="809" alt="image" src="https://github.com/user-attachments/assets/81e7a8fb-2ea7-43a7-85b5-5de4df20e183" />
- It was done by calculating every percentile in the dataset and then capping any value below the lower bound to the lower bound, and any value above the upper bound to the upper bound

- We also standardized formats so that the dataset will have consistent formats throughout
- <img width="935" height="812" alt="image" src="https://github.com/user-attachments/assets/a49a0e3b-6a5b-49b0-b03d-da4ce9b84810" />
- This prevents errors in merging, filtering, and grouping

  ## Loading
  - We then were able to load the cleaned dataset into its own Parquet file and then preview it to know if it was a success
  <img width="1166" height="782" alt="image" src="https://github.com/user-attachments/assets/d08d3774-377f-4aef-8118-d3f560440e9a" />
- #### Saving as Parquet:
We created a new directory called `data/final/` if it didn't already exist using `os.makedirs()` with `exist_ok=True`.

The DataFrame was then saved as a Parquet file (`loaded_data.parquet`) using `df.to_parquet()`. This format is preferred for analytics workflows due to its:

- Smaller file size (compared to CSV)  
- Faster read/write times
- Schema support and optimized columnar storage


 # Exploratory Data Analysis
 - We started by loading the data and inspecting it
 -<img width="1138" height="579" alt="image" src="https://github.com/user-attachments/assets/26b06c9e-a535-4f20-b27c-16e70464441f" />
 - We then went forward to cleaning the data to check the data types, detect missing values, and identify any potential data quality issues, but we had already done this in the ETL process
 - <img width="665" height="827" alt="image" src="https://github.com/user-attachments/assets/1b00b53f-1368-459f-940b-cd1ff33b09ac" />
 - We then went forward to interpret the summary, where we were able to find that
 - <img width="1071" height="671" alt="image" src="https://github.com/user-attachments/assets/4d3b473f-0d5e-4f6f-83b5-f1ee1743c67e" />
 
 ### Descriptive statistics for the numerical features to understand the central tendency, spread, and distribution of numerical variables
 - <img width="1132" height="720" alt="image" src="https://github.com/user-attachments/assets/53c14345-ae41-4bcc-afa3-42614d6b0550" />
 - Through this, we can see the output and insights drawn, such as the  range of values of the different columns
 - We then went forward to visualize the data to help us understand the data better through histograms and boxplots
 - We focused on the key numerical features which are the `price`, `freight_value`, `payment_value`, `review_score`, and ` profit_margin`
 - <img width="967" height="549" alt="image" src="https://github.com/user-attachments/assets/0ebd90aa-3d8a-4cc6-9e53-b241c5a6bd99" />
 - Through this, we have created histograms and boxplots of each numerical variable to show us the distribution of the data
 - <img width="1102" height="808" alt="image" src="https://github.com/user-attachments/assets/c5ff2d7a-308f-4f2f-92e6-1f48d0e61256" />
 - <img width="1107" height="686" alt="image" src="https://github.com/user-attachments/assets/5b147275-66e8-4dee-b3f7-85f65fb881e0" />
- Through these visualizations, we were able to draw insights such as :
- <img width="1167" height="867" alt="image" src="https://github.com/user-attachments/assets/5f17af2c-6c0d-46af-b6e6-ae11a12600be" />
- The overall insights are that
-  1. Pricing, payments, and shipping costs show diversity and clear outliers
   2. Customer satisfaction is high
   3. Profit margins are consistently strong

### Analysis of categorical variables 
- this include `order_status`, `payment_type`, `customer_state`, `seller_state` and `product_category_name_english`
- These categorical variables help us understand distribution patterns, dominant categories, and potential relationships
- <img width="827" height="435" alt="image" src="https://github.com/user-attachments/assets/d1ef33a3-8699-4ac8-8136-0b59f35aa416" />
- We decided to create count plots for each categorical variable
- <img width="1072" height="897" alt="image" src="https://github.com/user-attachments/assets/3396af30-342f-4732-9bc5-14279cae5b16" />
- <img width="674" height="489" alt="image" src="https://github.com/user-attachments/assets/f7441b12-1c65-4f6e-97ac-478704fe70e5" />
- Through this, we were able to draw some insights which include
- <img width="1161" height="446" alt="image" src="https://github.com/user-attachments/assets/873bbc00-c204-4381-b778-5471e8a3badc" />
- overall insights are that :
- 1. Order Status: Most orders delivered, few canceled.
  2. Payment Type: Credit card dominates.
  3. Customer/Seller State: São Paulo (SP) is the main hub.
  4. Product Category: Health & Beauty is top-selling.
  5. Business is concentrated in certain regions and categories.
  6. Payment and logistics are streamlined.
 
### Bivariate analysis
- In this part, we check for the relationships between two variables, focusing on
  i. Correlation between numerical variables
  ii. Comparison of categorical variables with numerical variables
  iii. Detection of patterns or trends
- We began with a correlation heatmap to visualize relationships between numerical features
- <img width="770" height="324" alt="image" src="https://github.com/user-attachments/assets/37a7fd67-4324-4ab3-96c4-1c145c5e3d99" />
- <img width="1071" height="886" alt="image" src="https://github.com/user-attachments/assets/fb041818-6bed-4297-90a5-a7b0756efb23" />
- We were able to draw some insights from this, which are
- <img width="1175" height="711" alt="image" src="https://github.com/user-attachments/assets/245e8d6d-3f21-471b-b0cb-407265acf98a" />
- overall insights are :
- 1. Some features are highly correlated (may need to drop/reduce for modeling).
  2. Price and freight are linked.

### Categorical vs Numerical variables
-This helps identify **how categories influence numerical metrics** such as price, freight value, payment value, and review scores.
- <img width="942" height="799" alt="image" src="https://github.com/user-attachments/assets/528b3422-8090-49ee-ac07-730a14cb2eaf" />
- We created boxplots for price/freight value by category and state
- This was the output of the boxplots
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

### Multivariate analysis
- This helps us understand the interactions between multiple variables to help in decision-making making
- We first decided to create a scatter plot of price vs Freight value by product category
- This plot examines how product prices relate to freight value and whether this relationship varies across top product categories.
- 
- <img width="969" height="893" alt="image" src="https://github.com/user-attachments/assets/47de78d3-40ec-4ae0-abed-a7381f26cd6f" />

- ##  Price vs. Freight Value by Top 5 Product Categories  
**Visualization Used:** Scatter Plot colored by product categories.

### Purpose:
- To analyze how shipping costs relate to product prices across categories.  
- To detect differences in freight strategies or product characteristics.

### Detailed Insights:
- **Distribution Patterns:**  
  - Categories like **furniture_decor** and **auto** show higher freight values due to larger or heavier products.  
  - Categories such as **books_general_interest** or **toys** have lower freight costs due to lighter items.

- **Category-Specific Trends:**  
  - **bed_bath_table:** Moderate to high freight with a wide range of prices.  
  - **sports_leisure:** Variable freight depending on item type (large vs. small equipment).  

- **Outliers:**  
  - High-priced items with high freight costs appear as rare cases, significant for logistics analysis.

### Business Implications:
- Identifies categories where shipping costs are disproportionately high.  
- Provides insights to optimize logistics and adjust pricing strategies.

---
- We then created a pairplot of key numerical variables
- <img width="984" height="749" alt="image" src="https://github.com/user-attachments/assets/af3b0b71-5627-4e3c-8842-36b74661a3c1" />
- <img width="983" height="286" alt="image" src="https://github.com/user-attachments/assets/63680834-da67-4a79-864c-defe4e9da65d" />
- 
## Pairwise Relationships between Key Numerical Features  
**Visualization Used:** Pairplot (Scatterplot Matrix) of `price`, `freight_value`, `payment_value`, and `profit_margin`.

### Purpose:
- To explore relationships, correlations, and distributions among multiple numerical features.  
- To identify potential patterns, clusters, or outliers.

### Detailed Insights:
- **Distributions (Diagonal Histograms):**  
  - **Price:** Skewed with a peak at lower prices, long tail toward high prices.  
  - **Freight Value:** Positively skewed; higher freight costs are less frequent.  
  - **Payment Value:** Similar distribution to price; likely positively skewed.  
  - **Profit Margin:** Bounded between 0 and 1, with possible skewness based on profit strategies.

- **Pairwise Relationships:**  
  - **Price vs. Freight Value:** Positive correlation; expensive items often have higher freight costs.  
  - **Price vs. Payment Value:** Strong positive correlation; payment value rises with price.  
  - **Price vs. Profit Margin:** Shows how profit margins vary with price.  
  - **Freight Value vs. Payment Value:** Reflects the relationship between shipping expenses and transaction size.

- **Outliers & Clusters:**  
  - Outliers indicate rare high-value transactions or potential anomalies.  
  - Clusters may suggest distinct customer segments or product groupings.

### Implication:
These relationships help in feature engineering, guiding predictive modeling, and understanding underlying data structure.
---

-3. **Group-wise Aggregation: Average Price per Category per State**
- This shows how product prices vary by product category and by customer state.
- its code
- <img width="853" height="279" alt="image" src="https://github.com/user-attachments/assets/fed36a1b-1410-48e6-91ba-bee81d5cb691" />
- the output is
- <img width="1075" height="884" alt="image" src="https://github.com/user-attachments/assets/81697726-f831-4b16-98e8-695837a33d0b" />
- ##  Average Price per Product Category per Top 5 Customer States  
**Visualization Used:** Grouped Bar Chart (Average Price by Product Category & State)

###  Purpose:
- To compare how product prices vary across different states.  
- To uncover regional differences in demand and pricing.

###  Detailed Insights:
- **Regional Variations:**  
  - States like **pr**, **rs**, and **sp** exhibit higher average prices for certain categories.  
  - Wealthier states may have a higher willingness to pay.
- **Product Category Trends:**  
  - Some categories (e.g., electronics, auto) show consistent pricing across states.  
  - Others (e.g., garden_tools, books_imported) vary greatly by region.
- **Customer Preferences:**  
  - Regional differences suggest certain states favor specific categories, influencing demand.
###  Business Implications:
- Helps tailor regional pricing and marketing strategies.  
- Supports inventory planning by understanding geographic purchasing patterns.
---

## ***Summary of Multivariate Analysis***
- **Pairplot:** Revealed fundamental relationships guiding feature selection.  
- **Scatter Plot:** Showed how freight relates to price, highlighting logistical challenges.  
- **Regional Analysis:** Emphasized the impact of geography on pricing and demand.  
***These insights provide a strong foundation for the next steps: **Feature Engineering*****
---

##  Feature Engineering

### What is Feature Engineering?
Feature engineering is the process of creating new input features or transforming existing ones to improve the performance of machine learning models. This step involves leveraging domain knowledge and data patterns to make the dataset more informative for modeling.

### Why Are We Doing This?
- **Improve Model Performance**: Well-engineered features help algorithms capture underlying relationships more effectively.
- **Reduce Noise**: By transforming or aggregating features, we can remove irrelevant variations in the data.
- **Capture Nonlinear Relationships**: Creating interaction terms or polynomial features can reveal complex relationships between variables.
- **Handle Data Limitations**: Sometimes, raw data lacks meaningful indicators, so new features can fill this gap.

### Typical Steps in Feature Engineering
1. **Feature Creation**: Creating new variables from existing ones (e.g., profit ratio, days taken for delivery, price per weight).
2. **Feature Transformation**: Applying log scaling, standardization, or encoding to prepare data for algorithms.
3. **Feature Encoding**: Converting categorical variables into numerical representations (e.g., one-hot encoding, label encoding).
4. **Feature Selection**: Choosing the most relevant features to avoid multicollinearity and reduce dimensionality.

### Why It Matters in This Project?
For this dataset, feature engineering can:
- Extract time-based features (e.g., delivery delays, approval times).
- Create ratios like `freight_value/price` to understand cost efficiency.
- Encode categorical variables like product categories and states for modeling.
- Aggregate or normalize features to capture meaningful patterns.

## Step 1. Extracting Date-Time Features
- We start by extracting useful components (year, month, day, hour) from the order_purchase_timestamp column.

**Why?**

- Time-based features help uncover seasonality, trends, and purchase behavior patterns, which can improve prediction and insights.
- <img width="965" height="472" alt="image" src="https://github.com/user-attachments/assets/0284098b-1b39-4b90-bd5d-610e78289d8c" />

## Step 2. Creating a Delivery Delay Indicator

- Next, we create a binary feature indicating whether an order was delivered after the estimated delivery date.

**Why?**

- Late deliveries often impact customer reviews and can be a critical business KPI.
- <img width="909" height="411" alt="image" src="https://github.com/user-attachments/assets/da3e7d2f-16ef-4e44-b733-ad04e8e851fd" />
## Step 5.Log Transformation of Skewed Variables

- Finally, we reduce skewness in variables with long-tailed distributions (e.g., price, freight_value, payment_value).

**Why?**

- Log transformation helps stabilize variance and makes data more normal, improving model performance.
- <img width="627" height="376" alt="image" src="https://github.com/user-attachments/assets/c621d995-76ad-4bee-8f0f-6d5a7b0127a2" />
| **Feature Name**       | **Type**                | **Description**                                                                  |
| ---------------------- | ----------------------- | -------------------------------------------------------------------------------- |
| `purchase_year`        | Numerical               | Extracted year of purchase from the timestamp.                                   |
| `purchase_month`       | Numerical               | Extracted month of purchase to analyze seasonality.                              |
| `purchase_day`         | Numerical               | Day of the month when the purchase occurred.                                     |
| `purchase_hour`        | Numerical               | Hour of purchase to identify peak purchase times.                                |
| `actual_delivery_days` | Numerical               | Number of days taken to deliver the order.                                       |
| `is_delayed`           | Binary (0/1)            | Indicator whether the order was delivered after the estimated delivery date.     |
| `price_per_gram`       | Numerical               | Ratio of product price to product weight, useful for freight and pricing models. |
| `log_price`            | Numerical (Transformed) | Log-transformed version of product price to reduce skewness.                     |
| `log_freight_value`    | Numerical (Transformed) | Log-transformed freight cost for better model stability.                         |
| `log_payment_value`    | Numerical (Transformed) | Log-transformed payment value to normalize data distribution.                    |


 ### Key Insights & Business Implications
 
-Customer Satisfaction: High review scores, but late deliveries can impact this.
-Pricing & Shipping: Wide range, with outliers. Shipping costs are linked to product type and geography.
-Regional Focus: São Paulo dominates; opportunity to expand in other states.
-Product Mix: Some categories are premium, others are low-cost; inventory and marketing should reflect this.
-Feature Engineering: New features (time, delay, log transforms) will improve model performance.


## Data Mining
# Student Responsible: Angela


























---
