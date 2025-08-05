#  DSA2040A_DataMining_Group-6

##  Overview
This project is an **end-to-end data analytics and mining pipeline** applied to the **Olist E-commerce dataset**.  
The workflow spans from **data extraction and transformation (ETL)** to **exploratory analysis**, **interactive dashboards**, and **data mining** to uncover meaningful patterns and insights.

---

##  Team & Responsibilities  
- **ETL Phase Lead:** Hana Gashaw
- **EDA Phase leads:** Trizzah Nzioka & Ted Korir
- **Data Mining leads:** Selmah Tzindori & Hana Gashaw
- **Dashboard lead:** Hana Gashaw 
- **Documentation:** Levin Ekuam &Angela Irungu
 

---

## Project Workflow
1. **ETL Process** – Data extraction, cleaning, and transformation.  
2. **Exploratory Data Analysis (EDA)** – Identifying trends and relationships.  
3. **Dashboards** – Building interactive dashboards for visualization.  
4. **Data Mining** – Discovering hidden patterns using analytical techniques.  

---

## Olist E-commerce Dataset

The Olist dataset represents real-world data from **Brazil’s largest e-commerce platform**.  
It consists of **relational CSV files** capturing transactions, customer behavior, and seller performance.

### Dataset Overview
- **Source**: Olist (public dataset)  
- **Focus**: Last 3 months of sales  
- **Structure**: Multiple tables linked via keys like `order_id`, `product_id`, and `customer_id`.

---


### Key Files Used

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


##  Section by Hana – ETL Process: Olist Brazilian E-commerce Dataset

Olist is one of **Brazil’s largest online marketplaces**, enabling small and medium-sized businesses to sell products through a central platform.  
The Olist dataset contains multiple **relational CSV files**, where each file captures a different aspect of the order lifecycle — customers, sellers, products, payments, and reviews.

---
## Extraction 
-Data was extracted from the nine datasets

<img width="1090" height="289" alt="Image" src="https://github.com/user-attachments/assets/efb5e29d-9ce7-4e55-a0ad-958d2116ee69" />

---

###  *A. Initial Data Inspection*
-The first step in the ETL process was to **inspect the raw data** to understand its structure, completeness, and potential issues
-It was then inspected for the first time, displaying the first few rows of each dataset.

---

####  Orders Table

**Output:**  

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>order_id</th>
      <th>customer_id</th>
      <th>order_status</th>
      <th>order_purchase_timestamp</th>
      <th>order_approved_at</th>
      <th>order_delivered_carrier_date</th>
      <th>order_delivered_customer_date</th>
      <th>order_estimated_delivery_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>e481f51cbdc54678b7cc49136f2d6af7</td>
      <td>9ef432eb6251297304e76186b10a928d</td>
      <td>delivered</td>
      <td>2017-10-02 10:56:33</td>
      <td>2017-10-02 11:07:15</td>
      <td>2017-10-04 19:55:00</td>
      <td>2017-10-10 21:25:13</td>
      <td>2017-10-18 00:00:00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>53cdb2fc8bc7dce0b6741e2150273451</td>
      <td>b0830fb4747a6c6d20dea0b8c802d7ef</td>
      <td>delivered</td>
      <td>2018-07-24 20:41:37</td>
      <td>2018-07-26 03:24:27</td>
      <td>2018-07-26 14:31:00</td>
      <td>2018-08-07 15:27:45</td>
      <td>2018-08-13 00:00:00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>47770eb9100c2d0c44946d9cf07ec65d</td>
      <td>41ce2a54c0b03bf3443c3d931a367089</td>
      <td>delivered</td>
      <td>2018-08-08 08:38:49</td>
      <td>2018-08-08 08:55:23</td>
      <td>2018-08-08 13:50:00</td>
      <td>2018-08-17 18:06:29</td>
      <td>2018-09-04 00:00:00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>949d5b44dbf5de918fe9c16f97b45f8a</td>
      <td>f88197465ea7920adcdbec7375364d82</td>
      <td>delivered</td>
      <td>2017-11-18 19:28:06</td>
      <td>2017-11-18 19:45:59</td>
      <td>2017-11-22 13:39:59</td>
      <td>2017-12-02 00:28:42</td>
      <td>2017-12-15 00:00:00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ad21c59c0840e6cb83a9ceb5573f8159</td>
      <td>8ab97904e6daea8866dbdbc4fb7aad2c</td>
      <td>delivered</td>
      <td>2018-02-13 21:18:39</td>
      <td>2018-02-13 22:20:29</td>
      <td>2018-02-14 19:46:34</td>
      <td>2018-02-16 18:17:02</td>
      <td>2018-02-26 00:00:00</td>
    </tr>
  </tbody>
</table>
</div>

**Interpretation of the Output:**  

| Column Name                   | Description                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| order_id                      | Unique identifier for each order.                                           |
| customer_id                   | Links each order to a customer from the customers table.                   |
| order_status                  | Current status of the order (e.g., delivered, shipped, canceled).          |
| order_purchase_timestamp      | When the order was placed by the customer.                                 |
| order_approved_at             | When the payment was approved.                                             |
| order_delivered_carrier_date  | When the seller handed the package to the carrier.                         |
| order_delivered_customer_date | When the customer received the order.                                      |
| order_estimated_delivery_date | Estimated delivery date given at the time of purchase.                     |

---

####  order_items Table

**Output:**  
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>order_id</th>
      <th>order_item_id</th>
      <th>product_id</th>
      <th>seller_id</th>
      <th>shipping_limit_date</th>
      <th>price</th>
      <th>freight_value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>00010242fe8c5a6d1ba2dd792cb16214</td>
      <td>1</td>
      <td>4244733e06e7ecb4970a6e2683c13e61</td>
      <td>48436dade18ac8b2bce089ec2a041202</td>
      <td>2017-09-19 09:45:35</td>
      <td>58.90</td>
      <td>13.29</td>
    </tr>
    <tr>
      <th>1</th>
      <td>00018f77f2f0320c557190d7a144bdd3</td>
      <td>1</td>
      <td>e5f2d52b802189ee658865ca93d83a8f</td>
      <td>dd7ddc04e1b6c2c614352b383efe2d36</td>
      <td>2017-05-03 11:05:13</td>
      <td>239.90</td>
      <td>19.93</td>
    </tr>
    <tr>
      <th>2</th>
      <td>000229ec398224ef6ca0657da4fc703e</td>
      <td>1</td>
      <td>c777355d18b72b67abbeef9df44fd0fd</td>
      <td>5b51032eddd242adc84c38acab88f23d</td>
      <td>2018-01-18 14:48:30</td>
      <td>199.00</td>
      <td>17.87</td>
    </tr>
    <tr>
      <th>3</th>
      <td>00024acbcdf0a6daa1e931b038114c75</td>
      <td>1</td>
      <td>7634da152a4610f1595efa32f14722fc</td>
      <td>9d7a1d34a5052409006425275ba1c2b4</td>
      <td>2018-08-15 10:10:18</td>
      <td>12.99</td>
      <td>12.79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>00042b26cf59d7ce69dfabb4e55b4fd9</td>
      <td>1</td>
      <td>ac6c3623068f30de03045865e4e10089</td>
      <td>df560393f3a51e74553ab94004ba5c87</td>
      <td>2017-02-13 13:57:51</td>
      <td>199.90</td>
      <td>18.14</td>
    </tr>
  </tbody>
</table>
</div>

**Interpretation of the Output:**  
| Column Name         | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| order_id            | Unique identifier for each order (links to orders table).                   |
| order_item_id       | The item number within the order (1 for the first item, 2 for the second…). |
| product_id          | Unique ID for the purchased product (links to products table).              |
| seller_id           | Unique ID of the seller responsible for this item (links to sellers table). |
| shipping_limit_date | Deadline for the seller to ship the item.                                   |
| price               | Price paid for the item (excluding shipping).                               |
| freight_value       | Shipping fee charged for the item.                                          |

---

####  products Table

**Output:**

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>product_id</th>
      <th>product_category_name</th>
      <th>product_name_lenght</th>
      <th>product_description_lenght</th>
      <th>product_photos_qty</th>
      <th>product_weight_g</th>
      <th>product_length_cm</th>
      <th>product_height_cm</th>
      <th>product_width_cm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1e9e8ef04dbcff4541ed26657ea517e5</td>
      <td>perfumaria</td>
      <td>40.0</td>
      <td>287.0</td>
      <td>1.0</td>
      <td>225.0</td>
      <td>16.0</td>
      <td>10.0</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3aa071139cb16b67ca9e5dea641aaa2f</td>
      <td>artes</td>
      <td>44.0</td>
      <td>276.0</td>
      <td>1.0</td>
      <td>1000.0</td>
      <td>30.0</td>
      <td>18.0</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>96bd76ec8810374ed1b65e291975717f</td>
      <td>esporte_lazer</td>
      <td>46.0</td>
      <td>250.0</td>
      <td>1.0</td>
      <td>154.0</td>
      <td>18.0</td>
      <td>9.0</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>cef67bcfe19066a932b7673e239eb23d</td>
      <td>bebes</td>
      <td>27.0</td>
      <td>261.0</td>
      <td>1.0</td>
      <td>371.0</td>
      <td>26.0</td>
      <td>4.0</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9dc1a7de274444849c219cff195d0b71</td>
      <td>utilidades_domesticas</td>
      <td>37.0</td>
      <td>402.0</td>
      <td>4.0</td>
      <td>625.0</td>
      <td>20.0</td>
      <td>17.0</td>
      <td>13.0</td>
    </tr>
  </tbody>
</table>
</div>

**Interpretation of the Output:**  
| Column Name                    | Description                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| `product_id`                  | Unique identifier for each product.                                        |
| `product_category_name`       | Category name of the product (e.g., `perfumaria`, `moveis_decoracao`).    |
| `product_name_lenght`         | Number of characters in the product's name.                                |
| `product_description_lenght`  | Number of characters in the product's description.                         |
| `product_photos_qty`          | Number of photos provided for the product.                                 |
| `product_weight_g`            | Weight of the product in grams.                                            |
| `product_length_cm`           | Length of the product in centimeters.                                      |
| `product_height_cm`           | Height of the product in centimeters.                                      |
| `product_width_cm`            | Width of the product in centimeters.                                       |

---

####  payments Table

**Output:**
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>order_id</th>
      <th>payment_sequential</th>
      <th>payment_type</th>
      <th>payment_installments</th>
      <th>payment_value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b81ef226f3fe1789b1e8b2acac839d17</td>
      <td>1</td>
      <td>credit_card</td>
      <td>8</td>
      <td>99.33</td>
    </tr>
    <tr>
      <th>1</th>
      <td>a9810da82917af2d9aefd1278f1dcfa0</td>
      <td>1</td>
      <td>credit_card</td>
      <td>1</td>
      <td>24.39</td>
    </tr>
    <tr>
      <th>2</th>
      <td>25e8ea4e93396b6fa0d3dd708e76c1bd</td>
      <td>1</td>
      <td>credit_card</td>
      <td>1</td>
      <td>65.71</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ba78997921bbcdc1373bb41e913ab953</td>
      <td>1</td>
      <td>credit_card</td>
      <td>8</td>
      <td>107.78</td>
    </tr>
    <tr>
      <th>4</th>
      <td>42fdf880ba16b47b59251dd489d4441a</td>
      <td>1</td>
      <td>credit_card</td>
      <td>2</td>
      <td>128.45</td>
    </tr>
  </tbody>
</table>
</div>

**Interpretation of the Output:** 
| Column Name            | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| `order_id`             | Unique identifier linking to the `orders` table.                            |
| `payment_sequential`   | tells us how many payment types were used for a single order. |
| `payment_type`         | Type of payment used (e.g., `credit_card`, `boleto`, `voucher`, `debit_card`). |
| `payment_installments` | tells us how many times a payment is split, like "3 monthly payments. |
| `payment_value`        | Amount paid by the customer (in BRL – Brazilian Real).(price + freight_value)|

---

####  reviews Table

**Output:**
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>review_id</th>
      <th>order_id</th>
      <th>review_score</th>
      <th>review_comment_title</th>
      <th>review_comment_message</th>
      <th>review_creation_date</th>
      <th>review_answer_timestamp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7bc2406110b926393aa56f80a40eba40</td>
      <td>73fc7af87114b39712e6da79b0a377eb</td>
      <td>4</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2018-01-18 00:00:00</td>
      <td>2018-01-18 21:46:59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>80e641a11e56f04c1ad469d5645fdfde</td>
      <td>a548910a1c6147796b98fdf73dbeba33</td>
      <td>5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2018-03-10 00:00:00</td>
      <td>2018-03-11 03:05:13</td>
    </tr>
    <tr>
      <th>2</th>
      <td>228ce5500dc1d8e020d8d1322874b6f0</td>
      <td>f9e4b658b201a9f2ecdecbb34bed034b</td>
      <td>5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2018-02-17 00:00:00</td>
      <td>2018-02-18 14:36:24</td>
    </tr>
    <tr>
      <th>3</th>
      <td>e64fb393e7b32834bb789ff8bb30750e</td>
      <td>658677c97b385a9be170737859d3511b</td>
      <td>5</td>
      <td>NaN</td>
      <td>Recebi bem antes do prazo estipulado.</td>
      <td>2017-04-21 00:00:00</td>
      <td>2017-04-21 22:02:06</td>
    </tr>
    <tr>
      <th>4</th>
      <td>f7c4243c7fe1938f181bec41a392bdeb</td>
      <td>8e6bfb81e283fa7e4f11123a3fb894f1</td>
      <td>5</td>
      <td>NaN</td>
      <td>Parabéns lojas lannister adorei comprar pela I...</td>
      <td>2018-03-01 00:00:00</td>
      <td>2018-03-02 10:26:53</td>
    </tr>
  </tbody>
</table>
</div>

**Interpretation of the Output:**

| Column Name              | Description                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| `review_id`              | Unique identifier for the review                                            |
| `order_id`               | ID of the order being reviewed (connects to orders table)                   |
| `review_score`           | Score given by the customer (1 to 5 stars)                                  |
| `review_comment_title`   | Optional title for the review (short summary)                |
| `review_comment_message` | Detailed review message provided by the customer                            |
| `review_creation_date`   | Date when the customer submitted the review                                 |
| `review_answer_timestamp`| Timestamp when Olist responded or processed the review                      |

---

####  Customers Table

**Output:**

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>customer_id</th>
      <th>customer_unique_id</th>
      <th>customer_zip_code_prefix</th>
      <th>customer_city</th>
      <th>customer_state</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>06b8999e2fba1a1fbc88172c00ba8bc7</td>
      <td>861eff4711a542e4b93843c6dd7febb0</td>
      <td>14409</td>
      <td>franca</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>1</th>
      <td>18955e83d337fd6b2def6b18a428ac77</td>
      <td>290c77bc529b7ac935b93aa66c333dc3</td>
      <td>9790</td>
      <td>sao bernardo do campo</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4e7b3e00288586ebd08712fdd0374a03</td>
      <td>060e732b5b29e8181a18229c7b0b2b5e</td>
      <td>1151</td>
      <td>sao paulo</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>3</th>
      <td>b2b6027bc5c5109e529d4dc6358b12c3</td>
      <td>259dac757896d24d7702b9acbbff3f3c</td>
      <td>8775</td>
      <td>mogi das cruzes</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4f2d8ab171c80ec8364f7c12e35b23ad</td>
      <td>345ecd01c38d18a9036ed96c73b8d066</td>
      <td>13056</td>
      <td>campinas</td>
      <td>SP</td>
    </tr>
  </tbody>
</table>
</div>

**Interpretation of the Output:**

| Column Name                | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| `customer_id`              | A unique identifier for a **customer account**, consistent across orders.   |
| `customer_unique_id`       | A hashed version of a real person’s ID, consistent across duplicate accounts
|                             | or email  changes.|
| `customer_zip_code_prefix` | First digits of the customer's ZIP code                                     |
| `customer_city`            | City of the customer                                                        |
| `customer_state`           | State abbreviation where the customer resides (e.g., SP, RJ)               |

---
####  Sellers Table

**Output:**

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>seller_id</th>
      <th>seller_zip_code_prefix</th>
      <th>seller_city</th>
      <th>seller_state</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3442f8959a84dea7ee197c632cb2df15</td>
      <td>13023</td>
      <td>campinas</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>1</th>
      <td>d1b65fc7debc3361ea86b5f14c68d2e2</td>
      <td>13844</td>
      <td>mogi guacu</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ce3ad9de960102d0677a81f5d0bb7b2d</td>
      <td>20031</td>
      <td>rio de janeiro</td>
      <td>RJ</td>
    </tr>
    <tr>
      <th>3</th>
      <td>c0f3eea2e14555b6faeea3dd58c1b1c3</td>
      <td>4195</td>
      <td>sao paulo</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>4</th>
      <td>51a04a8a6bdcb23deccc82b0b80742cf</td>
      <td>12914</td>
      <td>braganca paulista</td>
      <td>SP</td>
    </tr>
  </tbody>
</table>
</div>

**Interpretation of the Output:**

| Column Name             | Description                                                                 |
|-------------------------|-----------------------------------------------------------------------------|
| `seller_id`             | Unique identifier for each seller.                                          |
| `seller_zip_code_prefix`| First 5 digits of the seller's ZIP code, used for regional grouping.        |
| `seller_city`           | City where the seller is located.                                           |
| `seller_state`          | Two-letter abbreviation of the seller's state (e.g., SP = São Paulo).       |

---
####  Geo Table

**Output:**

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>geolocation_zip_code_prefix</th>
      <th>geolocation_lat</th>
      <th>geolocation_lng</th>
      <th>geolocation_city</th>
      <th>geolocation_state</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1037</td>
      <td>-23.545621</td>
      <td>-46.639292</td>
      <td>sao paulo</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1046</td>
      <td>-23.546081</td>
      <td>-46.644820</td>
      <td>sao paulo</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1046</td>
      <td>-23.546129</td>
      <td>-46.642951</td>
      <td>sao paulo</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1041</td>
      <td>-23.544392</td>
      <td>-46.639499</td>
      <td>sao paulo</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1035</td>
      <td>-23.541578</td>
      <td>-46.641607</td>
      <td>sao paulo</td>
      <td>SP</td>
    </tr>
  </tbody>
</table>
</div>

**Interpretation of the Output:**
| Column Name                 | Description                                                                 |
|-----------------------------|-----------------------------------------------------------------------------|
| `geolocation_zip_code_prefix` | First 5 digits of the ZIP code, used to group geographic locations.       |
| `geolocation_lat`           | Latitude coordinate of the location.                                       |
| `geolocation_lng`           | Longitude coordinate of the location.                                      |
| `geolocation_city`          | City of the geographic location.                                           |
| `geolocation_state`         | Two-letter state abbreviation of the geographic location (e.g., SP, RJ).  |

---

####  Categories Table

**Output:**

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>product_category_name</th>
      <th>product_category_name_english</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>beleza_saude</td>
      <td>health_beauty</td>
    </tr>
    <tr>
      <th>1</th>
      <td>informatica_acessorios</td>
      <td>computers_accessories</td>
    </tr>
    <tr>
      <th>2</th>
      <td>automotivo</td>
      <td>auto</td>
    </tr>
    <tr>
      <th>3</th>
      <td>cama_mesa_banho</td>
      <td>bed_bath_table</td>
    </tr>
    <tr>
      <th>4</th>
      <td>moveis_decoracao</td>
      <td>furniture_decor</td>
    </tr>
  </tbody>
</table>
</div>

**Interpretation of the Output:**
| product_category_name             | product_category_name_english     |
|----------------------------------|-----------------------------------|
| beleza_saude                     | health_beauty                     |
| informatica_acessorios           | computers_accessories             |
| automotivo                       | auto                              |
| cama_mesa_banho                  | bed_bath_table                    |
| moveis_decoracao                 | furniture_decor                   |
| ...                              | ...                               |

---

Its structure was then inspected in the same way as creating a dictionary, first looping through it as the structure is inspected and printed

**Code Used**

<img width="676" height="304" alt="Image" src="https://github.com/user-attachments/assets/8ed133d2-2756-4f8f-8814-460c19ffa910" />

**Output**
###  Summary of Raw Dataset (Before Cleaning)

| Dataset               | Rows      | Columns | Key Fields | Missing Values / Observations |
|-----------------------|-----------|---------|------------|--------------------------------|
| **Orders**            | 99,441    | 8       | `order_id`, `customer_id` | Missing timestamps (`approved_at`, `delivered_carrier_date`, `delivered_customer_date`); includes canceled orders |
| **Order Items**       | 112,650   | 7       | `order_id`, `product_id`, `seller_id` | No missing values; some products not found in products table |
| **Products**          | 32,951    | 9       | `product_id`, `product_category_name` | Missing category names and some dimension values |
| **Payments**          | 103,886   | 5       | `order_id`, `payment_type` | No nulls in order_id; some multiple payments per order |
| **Reviews**           | 99,224    | 7       | `review_id`, `order_id` | Most comments missing; duplicate reviews for some orders |
| **Customers**         | 99,441    | 5       | `customer_id`, `customer_unique_id` | No missing values; duplicates in unique IDs possible |
| **Sellers**           | 3,095     | 4       | `seller_id`, `seller_zip_code_prefix` | No missing values; duplicates in seller entries |
| **Geolocation**       | 1,000,163 | 5       | `geolocation_zip_code_prefix`, `lat`, `lng` | Duplicates for many ZIP codes; coordinates inconsistent |
| **Category Translation** | 71     | 2       | `product_category_name`, `product_category_name_english` | No missing values; redundant entries |

---

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

---

## Transformation
- This part entails changing the datasets into the required formats so as to be able to draw meaningful insights from them.
- We started by converting the date time columns into datetime type to enable filtering
 
<img width="1130" height="886" alt="image" src="https://github.com/user-attachments/assets/0c28018d-5c85-4533-8491-1e8aa1fb6021" />

- This was first done by checking if the columns actually appear in the several datasets and then changing them into the datetime format

- Since we wanted to look at only the sales of the last 3 months, we had to do some filtering
  
<img width="975" height="853" alt="image" src="https://github.com/user-attachments/assets/7d70915d-c225-4865-878c-1aa1d3399155" />
 
<img width="802" height="272" alt="image" src="https://github.com/user-attachments/assets/9362fde7-7e2b-4903-9298-2f7e885321f6" />

- We started by first finding the **latest date** in the orders table, calculating the date **three months before that**, and filtering the orders to keep only those within this period.  
- Using the `order_id`s from these recent orders, we filtered the related tables to retain only records linked to these orders:
  - Order Items – only items belonging to recent orders.  
  - Payments – only payments associated with recent orders.  
  - Reviews – only reviews tied to recent orders.  
  - Customers – only customers who placed recent orders.  
  - Products – only products appearing in recent order items.  
  - Sellers – only sellers involved in recent order items.  
  - Category Translation – only categories present in recent products.  
  - Geolocation – only ZIP codes for the filtered customers and sellers.  

This filtering ensured that all tables were **temporally consistent**, included only relevant records, reduced noise, and improved processing performance while maintaining **relational integrity** across the dataset.  

After filtering, we **merged the datasets** into a single unified DataFrame containing all relevant information for each recent order.  
This prepared the data for **analysis, modeling, and visualization** by consolidating all features in one place.

<img width="964" height="890" alt="image" src="https://github.com/user-attachments/assets/7176bfb5-07ec-4c4f-bf8e-5317eecb51a6" />

As a result, we created a **unified dataset** with **11,777 entries** and **44 columns**, containing detailed transaction-level information suitable for in-depth analysis.  
The temporal coverage of this final dataset spans from **2018-07-17** to **2018-10-17**.  
Missing values in some columns reflect **real-world data gaps**, such as unreviewed orders or incomplete delivery records.

### Cleaning the merged datasets

<img width="1139" height="869" alt="image" src="https://github.com/user-attachments/assets/43d64841-6281-418e-8af9-7f2635df4786" />

- We checked if there are any duplicates and found none, but we were able to find that there were several missing values, and we were able to get the percentage of missing values in each column
- We then removed columns with more than 50 % missing values
  
<img width="499" height="110" alt="image" src="https://github.com/user-attachments/assets/77f5a260-31f2-4ca7-8733-5f4c47231b94" />

We then proceeded to handle the remaining missing values:  
- **Datetime columns** were filled using related datetime columns where possible; otherwise, a forward fill method was applied.  
- **Numeric columns** with missing values were imputed using either the mean or median, depending on the skewness of the data.

<img width="893" height="661" alt="image" src="https://github.com/user-attachments/assets/0e48fe04-3bcd-467b-ad66-11112eba1343" />

We also filled in the missing categorical values with the mode

<img width="852" height="295" alt="image" src="https://github.com/user-attachments/assets/399e8861-3e8d-4869-b3cf-b48617a28cc9" />

We were also able to add more columns to enable us to derive more insights from the data

- We  added the purchase frequency per customer, which shows how often a customer makes a purchase

<img width="1161" height="353" alt="image" src="https://github.com/user-attachments/assets/a5ea9be9-9500-4e08-827d-593bd6c80d8f" />

- We also handled outliers in the dataset to reduce noise in the dataset and keep extreme values from skewing models and visualizations
 
<img width="1017" height="809" alt="image" src="https://github.com/user-attachments/assets/81e7a8fb-2ea7-43a7-85b5-5de4df20e183" />

- It was done by calculating every percentile in the dataset and then capping any value below the lower bound to the lower bound, and any value above the upper bound to the upper bound

- We also standardized formats so that the dataset will have consistent formats throughout
  
<img width="935" height="812" alt="image" src="https://github.com/user-attachments/assets/a49a0e3b-6a5b-49b0-b03d-da4ce9b84810" />

- This prevents errors in merging, filtering, and grouping

## Loading
  
We then were able to load the cleaned dataset into its own Parquet file and then preview it to know if it was a success
  
<img width="1166" height="782" alt="image" src="https://github.com/user-attachments/assets/d08d3774-377f-4aef-8118-d3f560440e9a" />

#### Saving as Parquet:

We created a new directory called `data/final/` if it didn't already exist using `os.makedirs()` with `exist_ok=True`.

The DataFrame was then saved as a Parquet file (`loaded_data.parquet`) using `df.to_parquet()`. This format is preferred for analytics workflows due to its:

- Smaller file size (compared to CSV)  
- Faster read/write times
- Schema support and optimized columnar storage


 # Section by Ted Korir & Trizzah Nzioka: Exploratory Data Analysis
 - We started by loading the data and inspecting it
   
 <img width="1138" height="579" alt="image" src="https://github.com/user-attachments/assets/26b06c9e-a535-4f20-b27c-16e70464441f" />
 
 - We then went forward to cleaning the data to check the data types, detect missing values, and identify any potential data quality issues, but we had already done this in the ETL process
  
<img width="665" height="827" alt="image" src="https://github.com/user-attachments/assets/1b00b53f-1368-459f-940b-cd1ff33b09ac" />

 - We then went forward to interpret the summary, where we were able to find that

<img width="1071" height="671" alt="image" src="https://github.com/user-attachments/assets/4d3b473f-0d5e-4f6f-83b5-f1ee1743c67e" />
 
 ### Descriptive statistics for the numerical features to understand the central tendency, spread, and distribution of numerical variables
 
<img width="1132" height="720" alt="image" src="https://github.com/user-attachments/assets/53c14345-ae41-4bcc-afa3-42614d6b0550" />

 - Through this, we can see the output and insights drawn, such as the  range of values of the different columns
 - We then went forward to visualize the data to help us understand the data better through histograms and boxplots
 - We focused on the key numerical features which are the `price`, `freight_value`, `payment_value`, `review_score`, and ` profit_margin`
   
<img width="967" height="549" alt="image" src="https://github.com/user-attachments/assets/0ebd90aa-3d8a-4cc6-9e53-b241c5a6bd99" />

 - Through this, we have created histograms and boxplots of each numerical variable to show us the distribution of the data
   
<img width="1102" height="808" alt="image" src="https://github.com/user-attachments/assets/c5ff2d7a-308f-4f2f-92e6-1f48d0e61256" />
<img width="1107" height="686" alt="image" src="https://github.com/user-attachments/assets/5b147275-66e8-4dee-b3f7-85f65fb881e0" />

- Through these visualizations, we were able to draw insights such as :
 
<img width="1167" height="867" alt="image" src="https://github.com/user-attachments/assets/5f17af2c-6c0d-46af-b6e6-ae11a12600be" />

- The overall insights are that:
   1. Pricing, payments, and shipping costs show diversity and clear outliers
   2. Customer satisfaction is high
   3. Profit margins are consistently strong

### Analysis of categorical variables 
- This include `order_status`, `payment_type`, `customer_state`, `seller_state` and `product_category_name_english`
- These categorical variables help us understand distribution patterns, dominant categories, and potential relationships

<img width="827" height="435" alt="image" src="https://github.com/user-attachments/assets/d1ef33a3-8699-4ac8-8136-0b59f35aa416" />

- We decided to create count plots for each categorical variable
  
<img width="1072" height="897" alt="image" src="https://github.com/user-attachments/assets/3396af30-342f-4732-9bc5-14279cae5b16" />
<img width="674" height="489" alt="image" src="https://github.com/user-attachments/assets/f7441b12-1c65-4f6e-97ac-478704fe70e5" />

- Through this, we were able to draw some insights which include:
  
<img width="1161" height="446" alt="image" src="https://github.com/user-attachments/assets/873bbc00-c204-4381-b778-5471e8a3badc" />

Overall insights are that :
  1. Order Status: Most orders delivered, few canceled.
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
<img width="770" height="324" alt="image" src="https://github.com/user-attachments/assets/37a7fd67-4324-4ab3-96c4-1c145c5e3d99" />
<img width="1071" height="886" alt="image" src="https://github.com/user-attachments/assets/fb041818-6bed-4297-90a5-a7b0756efb23" />

- We were able to draw some insights from this, which are
 
<img width="1175" height="711" alt="image" src="https://github.com/user-attachments/assets/245e8d6d-3f21-471b-b0cb-407265acf98a" />

Overall insights are :
  1. Some features are highly correlated (may need to drop/reduce for modeling).
  2. Price and freight are linked.

### Categorical vs Numerical variables
-This helps identify **how categories influence numerical metrics** such as price, freight value, payment value, and review scores.

<img width="942" height="799" alt="image" src="https://github.com/user-attachments/assets/528b3422-8090-49ee-ac07-730a14cb2eaf" />
- We created boxplots for price/freight value by category and state
- This was the output of the boxplots
 
<img width="1007" height="601" alt="image" src="https://github.com/user-attachments/assets/7448ddba-e323-4076-9855-4785c762dea8" />

The boxplot for **Price vs Product Category** provides insights into how prices vary across the top 15 product categories.

**Key Observations:**
- Categories like **watches_gifts** and **industry_commerce_and_business** exhibit **higher median prices**, suggesting they are premium or specialized products.
- **Computers** and **home_appliances_2** also show relatively high prices, along with several outliers indicating a few extremely expensive items.
- **Cool_stuff** and **office_furniture** have **lower median prices**, highlighting these categories as more affordable.
- The **presence of many outliers** across categories implies significant price diversity within the same category.

<img width="999" height="616" alt="image" src="https://github.com/user-attachments/assets/87b8dc07-bad5-45fe-8aa1-43dcb8c01087" />

The boxplot for **Freight Value vs Product Category** reveals shipping cost variations among product categories.

**Key Observations:**
- Categories like **kitchen_dining_laundry_garden_furniture**, **garden_tools**, and **furniture_living_room** have **higher median freight costs**, possibly due to larger or heavier items.
- **Fashion_male_clothing** and **books_imported** tend to have **lower freight costs**, reflecting smaller and lighter products.
- Outliers with **very high freight values** suggest occasional special shipping requirements or long-distance deliveries.
    
<img width="1034" height="624" alt="image" src="https://github.com/user-attachments/assets/ef6fa699-32c6-4b04-90c2-4964bcd08018" />

The boxplot for **Freight Value vs Customer States** helps to understand regional differences in shipping costs.

**Key Observations:**
- States like **ce**, **m**, **to**, and **pa** have **higher median freight values**, suggesting that deliveries to these areas are costlier—likely due to distance or logistics.
- Most states cluster around **freight values between 20 and 30**, indicating stable shipping costs for the majority of customers.
- Several **outliers** reflect shipments with abnormally high costs.

<img width="1007" height="637" alt="image" src="https://github.com/user-attachments/assets/4c4846f1-462c-432e-91bb-ba4cc2b641f4" />

The boxplot for **Freight Value vs Seller States** examines shipping costs from different seller regions.

**Key Observations:**
- Sellers in **pe**, **es**, and **ce** incur **higher median freight values**, which may indicate these locations are farther from major customer bases or involve higher handling costs.
- Most seller states have freight costs within a narrow range (20–35), showing general uniformity in shipping rates.
- Some states like **se** and **pi** display **outliers** with extremely high freight costs, possibly for large shipments or distant deliveries.
 
  The boxplot for **Freight Value vs Seller States** examines shipping costs from different seller regions.

**Key Observations:**
- Sellers in **pe**, **es**, and **ce** incur **higher median freight values**, which may indicate these locations are farther from major customer bases or involve higher handling costs.
- Most seller states have freight costs within a narrow range (20–35), showing general uniformity in shipping rates.
- Some states like **se** and **pi** display **outliers** with extremely high freight costs, possibly for large shipments or distant deliveries.

### Multivariate analysis
- This helps us understand the interactions between multiple variables to help in decision-making making
- We first decided to create a scatter plot of price vs Freight value by product category
- This plot examines how product prices relate to freight value and whether this relationship varies across top product categories.

<img width="969" height="893" alt="image" src="https://github.com/user-attachments/assets/47de78d3-40ec-4ae0-abed-a7381f26cd6f" />

##  Price vs. Freight Value by Top 5 Product Categories  
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
<img width="984" height="749" alt="image" src="https://github.com/user-attachments/assets/af3b0b71-5627-4e3c-8842-36b74661a3c1" />

<img width="983" height="286" alt="image" src="https://github.com/user-attachments/assets/63680834-da67-4a79-864c-defe4e9da65d" />

---- 

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

---

# Section by Hana Gashaw & Selmah Tzindori  Data Mining & Modeling Process

After preparing and cleaning the dataset through the ETL pipeline, we proceeded to the **data mining and modeling phase**.  
This stage aimed to uncover **hidden patterns**, **group similar entities**, and **predict outcomes** using machine learning techniques.  

We applied a combination of:
- **Unsupervised Learning** (for discovering natural groupings and patterns)  
- **Supervised Learning** (for predictive modeling tasks)  

The process involved:
1. **Feature Selection & Engineering** – choosing relevant numerical and categorical attributes.  
2. **Data Scaling & Encoding** – ensuring variables were properly normalized and encoded.  
3. **Model Training & Evaluation** – applying algorithms, tuning parameters, and assessing performance.  

The following sections outline the **algorithms used**, their **working principles**, and **how they were applied** to our dataset to generate meaningful insights.

---

###  K-Means Clustering

K-Means is an **unsupervised algorithm** that groups data into **K clusters** by minimizing differences within clusters and maximizing differences between them.  
It works by repeatedly assigning points to the nearest centroid and updating centroid positions until stable clusters are formed.



####  Application in This Project
We applied K-Means to segment customers/orders based on attributes such as:
- `payment_value`  
- `purchase_frequency`  
- `product_weight_g`  

The clustering revealed distinct patterns, including:
- **High-value customers**  
- **Bulk buyers**  
- **Frequent buyers**  

These segments provided insights into customer behavior, supporting better decision-making.

---

We started by importing the required libraries for data manipulation, scaling, clustering, and visualization as shown below:

<img width="1086" height="446" alt="Image" src="https://github.com/user-attachments/assets/5cc47d21-744d-49d6-ad6c-20b7bb0d0277" />

We then load the cleaned and transformed dataset from the ETL step. 

<img width="946" height="316" alt="Image" src="https://github.com/user-attachments/assets/a4df0648-5d87-4b0a-88b2-9963a06ef398" />

**Output**

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>order_id</th>
      <th>customer_id</th>
      <th>order_status</th>
      <th>order_purchase_timestamp</th>
      <th>order_approved_at</th>
      <th>order_delivered_carrier_date</th>
      <th>order_delivered_customer_date</th>
      <th>order_estimated_delivery_date</th>
      <th>order_item_id</th>
      <th>product_id</th>
      <th>...</th>
      <th>product_width_cm</th>
      <th>seller_zip_code_prefix</th>
      <th>seller_city</th>
      <th>seller_state</th>
      <th>product_category_name_english</th>
      <th>customer_lat</th>
      <th>customer_lng</th>
      <th>seller_lat</th>
      <th>seller_lng</th>
      <th>purchase_frequency</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>53cdb2fc8bc7dce0b6741e2150273451</td>
      <td>b0830fb4747a6c6d20dea0b8c802d7ef</td>
      <td>delivered</td>
      <td>2018-07-24 20:41:37</td>
      <td>2018-07-26 03:24:27</td>
      <td>2018-07-26 14:31:00</td>
      <td>2018-08-07 15:27:45</td>
      <td>2018-08-13</td>
      <td>1.0</td>
      <td>595fac2a385ac33a80bd5114aec74eb8</td>
      <td>...</td>
      <td>19.0</td>
      <td>31570.0</td>
      <td>belo horizonte</td>
      <td>sp</td>
      <td>perfumery</td>
      <td>-16.515006</td>
      <td>-44.660711</td>
      <td>-19.902360</td>
      <td>-43.980427</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>47770eb9100c2d0c44946d9cf07ec65d</td>
      <td>41ce2a54c0b03bf3443c3d931a367089</td>
      <td>delivered</td>
      <td>2018-08-08 08:38:49</td>
      <td>2018-08-08 08:55:23</td>
      <td>2018-08-08 13:50:00</td>
      <td>2018-08-17 18:06:29</td>
      <td>2018-09-04</td>
      <td>1.0</td>
      <td>aa4383b373c6aca5d8797843e5594415</td>
      <td>...</td>
      <td>21.0</td>
      <td>14840.0</td>
      <td>guariba</td>
      <td>sp</td>
      <td>auto</td>
      <td>-16.745150</td>
      <td>-48.514783</td>
      <td>-21.363502</td>
      <td>-48.229601</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>5ff96c15d0b717ac6ad1f3d77225a350</td>
      <td>19402a48fe860416adf93348aba37740</td>
      <td>delivered</td>
      <td>2018-07-25 17:44:10</td>
      <td>2018-07-25 17:55:14</td>
      <td>2018-07-26 13:16:00</td>
      <td>2018-07-30 15:52:25</td>
      <td>2018-08-08</td>
      <td>1.0</td>
      <td>10adb53d8faa890ca7c2f0cbcb68d777</td>
      <td>...</td>
      <td>16.0</td>
      <td>14940.0</td>
      <td>ibitinga</td>
      <td>sp</td>
      <td>bed_bath_table</td>
      <td>-23.713190</td>
      <td>-46.687407</td>
      <td>-21.757321</td>
      <td>-48.829744</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>f3e7c359154d965827355f39d6b1fdac</td>
      <td>62b423aab58096ca514ba6aa06be2f98</td>
      <td>delivered</td>
      <td>2018-08-09 11:44:40</td>
      <td>2018-08-10 03:24:51</td>
      <td>2018-08-10 12:29:00</td>
      <td>2018-08-13 18:24:27</td>
      <td>2018-08-17</td>
      <td>1.0</td>
      <td>e99d69efe684efaa643f99805f7c81bc</td>
      <td>...</td>
      <td>25.0</td>
      <td>14910.0</td>
      <td>tabatinga</td>
      <td>sp</td>
      <td>stationery</td>
      <td>-23.531732</td>
      <td>-47.499804</td>
      <td>-21.737063</td>
      <td>-48.687601</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b276e4f8c0fb86bd82fce576f21713e0</td>
      <td>cf8ffeddf027932e51e4eae73b384059</td>
      <td>delivered</td>
      <td>2018-07-29 23:34:51</td>
      <td>2018-07-29 23:45:15</td>
      <td>2018-07-30 14:43:00</td>
      <td>2018-07-31 22:48:50</td>
      <td>2018-08-06</td>
      <td>1.0</td>
      <td>c6c1f263e076bd9c1f1640250a5d0c29</td>
      <td>...</td>
      <td>16.0</td>
      <td>13030.0</td>
      <td>campinas</td>
      <td>sp</td>
      <td>perfumery</td>
      <td>-22.740602</td>
      <td>-47.375821</td>
      <td>-22.924970</td>
      <td>-47.074284</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 43 columns</p>
</div>

---

We then selected key numeric features that best describe customer behavior and product characteristics—`payment_value`, `purchase_frequency`, and `product_weight_g`.  
These variables capture spending patterns, buying frequency, and product attributes, forming the basis for meaningful clustering.

<img width="1033" height="373" alt="Image" src="https://github.com/user-attachments/assets/4bed4a85-49ca-4252-8c1e-afb654afb7fb" />

<img width="905" height="455" alt="Image" src="https://github.com/user-attachments/assets/e3401cb2-692b-4df3-82a0-64594fb3e99a" />

---
Since K-Means is distance-based, we standardized the selected features using `StandardScaler` to ensure all variables contribute equally to clustering.  
After scaling, we verified that the transformed data had a mean of 0 and standard deviation of 1.

<img width="991" height="358" alt="image" src="https://github.com/user-attachments/assets/ddaa91e6-5106-4d84-a9ec-f134c73f685e" />

---

<img width="1045" height="458" alt="image" src="https://github.com/user-attachments/assets/9eef940a-550d-4de4-94f6-7873c0644539" />

---

## Step 5. Determining the Optimal Number of Clusters (K)

### Why do we need to determine K?

K-Means requires us to specify the number of clusters (`K`) in advance. Choosing the wrong `K` can lead to poor or misleading results. We use the **Elbow Method** to find the optimal `K`.

### The Elbow Method

The Elbow Method plots the **Within-Cluster Sum of Squares (WCSS)** against the number of clusters (`K`). The WCSS measures the compactness of the clusters; a smaller WCSS is better. As `K` increases, WCSS will always decrease, but at some point, the rate of decrease slows down, forming an "elbow" in the plot. This elbow point often represents the optimal number of clusters.

```python
# Calculate WCSS for different values of K
wcss = []
for i in range(1, 11):
    kmeans = KMeans(n_clusters=i, init='k-means++', random_state=42)
    kmeans.fit(X_scaled)
    wcss.append(kmeans.inertia_)

# Plot the Elbow Method graph
plt.figure(figsize=(10, 6))
plt.plot(range(1, 11), wcss, marker='o', linestyle='--')
plt.title('Elbow Method to Determine Optimal K')
plt.xlabel('Number of Clusters (K)')
plt.ylabel('WCSS (Inertia)')
plt.xticks(range(1, 11))
plt.grid(True)
plt.show()
```
<img width="958" height="503" alt="Screenshot 2025-08-05 104803" src="https://github.com/user-attachments/assets/966ca51f-437b-4718-a539-5d3650a5ebf8" />

## Step 6. Applying K-Means with the Optimal K

### Why this step?

Once we have determined the optimal `K` (in this case, 3 from the Elbow Method), we apply the K-Means algorithm to segment the data.

```python
# Apply K-Means with the optimal number of clusters (e.g., K=3)
kmeans = KMeans(n_clusters=3, init='k-means++', random_state=42)
df['cluster_label'] = kmeans.fit_predict(X_scaled)

# Display the first few rows with the new cluster labels
print(df.head())
```

## Step 7. Visualizing the Clusters

### Why Visualize?

Visualizing the clusters helps us understand the segmentation. We can use a 3D scatter plot to show how the data points are grouped in the feature space. This provides a clear, intuitive view of the clusters.

```python
# Example of 3D visualization of the clusters
from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure(figsize=(12, 10))
ax = fig.add_subplot(111, projection='3d')

# Scatter plot for each cluster
ax.scatter(df[df['cluster_label'] == 0]['payment_value'],
           df[df['cluster_label'] == 0]['purchase_frequency'],
           df[df['cluster_label'] == 0]['product_weight_g'],
           c='red', label='Cluster 0')
ax.scatter(df[df['cluster_label'] == 1]['payment_value'],
           df[df['cluster_label'] == 1]['purchase_frequency'],
           df[df['cluster_label'] == 1]['product_weight_g'],
           c='blue', label='Cluster 1')
ax.scatter(df[df['cluster_label'] == 2]['payment_value'],
           df[df['cluster_label'] == 2]['purchase_frequency'],
           df[df['cluster_label'] == 2]['product_weight_g'],
           c='green', label='Cluster 2')

ax.set_xlabel('Payment Value')
ax.set_ylabel('Purchase Frequency')
ax.set_zlabel('Product Weight')
ax.set_title('K-Means Clustering Results')
ax.legend()
plt.show()
```
<img width="749" height="491" alt="Screenshot 2025-08-05 105132" src="https://github.com/user-attachments/assets/13147f01-1137-4925-aea2-ce90f33025b7" />

## Step 8. Interpreting the Clusters

### Why interpret the clusters?

Once the clusters are created, we need to understand what each cluster represents. We analyze the characteristics of each cluster by looking at the mean values of the features.

```python
# Analyze the cluster characteristics
cluster_summary = df.groupby('cluster_label')[['payment_value', 'purchase_frequency', 'product_weight_g']].mean()
print(cluster_summary)
```

**Interpretation:**

  - **Cluster 0:** (Analysis based on the `cluster_summary` table)
  - **Cluster 1:** (Analysis based on the `cluster_summary` table)
  - **Cluster 2:** (Analysis based on the `cluster_summary` table)

This analysis helps us identify segments such as **high-value customers**, **frequent buyers**, or **bulk purchasers**, providing actionable insights for business strategy.

<img width="976" height="405" alt="k5" src="https://github.com/user-attachments/assets/9b4e63b5-5bc1-4539-a44c-6191e34acd6b" />

## Decision Trees for Classification: Theory & Working Principle

### What is a Decision Tree?

A Decision Tree is a **supervised machine learning algorithm** used for both **classification** and **regression** tasks. It works by creating a model that predicts the value of a target variable by learning simple decision rules inferred from the data features. The structure is tree-like, with each **internal node** representing a test on a feature, each **branch** representing the outcome of the test, and each **leaf node** representing a class label or a value.

-----

### **How It Works (Step-by-Step)**

1.  **Start with a Root Node**: The algorithm begins with a single node representing the entire dataset.
2.  **Find the Best Split**: The algorithm searches for the best feature to split the data into subsets. The "best" split is determined by a metric like **Gini Impurity** or **Entropy**.
3.  **Split the Data**: The root node is split into two or more sub-nodes based on the chosen feature.
4.  **Repeat Recursively**: The process is repeated for each sub-node until a stopping condition is met (e.g., maximum depth is reached, or a node contains too few data points). The final nodes are the **leaf nodes**, which contain the predicted class label.

-----

### **Mathematics Behind It**

The primary goal is to find splits that create the most **homogeneous** child nodes.

  - **Gini Impurity**: Measures the probability of a randomly chosen element being incorrectly classified. A Gini score of 0 means perfect purity.
    \[ \\text{Gini} = 1 - \\sum\_{i=1}^{C} (p\_i)^2 \]
    Where \\( p_i \\) is the probability of an item being classified into class \\( i \\).
  - **Entropy**: Measures the randomness or uncertainty in a dataset.
    \[ \\text{Entropy} = - \\sum\_{i=1}^{C} p\_i \\log\_2(p\_i) \]
    The algorithm aims to minimize Entropy, or maximize **Information Gain**.

-----

### Why Use Decision Trees?

  - **Easy to Understand**: The logic is simple to follow and visualize.
  - **Requires Little Data Preparation**: No need for feature scaling or normalization.
  - **Handles Both Numerical & Categorical Data**: Can be used with different types of data.
  - **Useful for Feature Selection**: Helps in identifying the most important features.

-----

### **Limitations**

  - **Overfitting**: Prone to creating overly complex trees that don't generalize well to new data.
  - **Bias**: Small changes in data can lead to a very different tree structure.
  - **Complexity**: Can be computationally expensive to train on large datasets with many features.

-----

### **Application to Our Project**

We will use a Decision Tree to predict `review_score` based on other features like `payment_value` and `freight_value`. This will help us understand what factors influence a customer's review, which is crucial for improving customer satisfaction and service.

-----

## Step 1. Loading the Required Libraries

**Why?**
We need to import libraries for:

  - **Data manipulation** (pandas)
  - **Modeling** (DecisionTreeClassifier from scikit-learn)
  - **Model evaluation** (accuracy\_score)
  - **Data splitting** (train\_test\_split)

<!-- end list -->

```python
# Import required libraries
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score
```

## Step 2. Loading the Transformed Dataset

**Why?**
Similar to K-Means, we use the cleaned and transformed dataset to ensure our model is trained on quality data.

```python
# Load the transformed dataset
df = pd.read_csv('../data/transformed/transformed_data.csv')
```

## Step 3. Preparing the Data for the Model

### Why this step?

For a supervised learning model, we must define our **features (X)** and our **target variable (y)**. We will use `review_score` as our target (`y`), and `payment_value` and `freight_value` as our features (`X`).

```python
# Define features (X) and target (y)
X = df[['payment_value', 'freight_value']]
y = df['review_score']

# Display the features and target
print("Features (X):")
print(X.head())
print("\nTarget (y):")
print(y.head())
```

## Step 4. Splitting the Data

### Why split the data?

To evaluate how well our model performs on unseen data, we split the dataset into a **training set** and a **testing set**. This prevents the model from simply memorizing the training data and helps assess its ability to generalize. We use an 80/20 split, with 80% for training and 20% for testing.

```python
# Split data into training and testing sets (80% train, 20% test)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Print the shapes of the split data
print(f"Shape of X_train: {X_train.shape}")
print(f"Shape of X_test: {X_test.shape}")
print(f"Shape of y_train: {y_train.shape}")
print(f"Shape of y_test: {y_test.shape}")
```

## Step 5. Building and Training the Model

### Why this step?

We now instantiate the `DecisionTreeClassifier` and train it on our training data. The `fit` method is what performs the learning process, building the decision tree based on the provided features and target.

```python
# Initialize the Decision Tree classifier
dtree = DecisionTreeClassifier(random_state=42)

# Train the model
dtree.fit(X_train, y_train)
```

## Step 6. Making Predictions and Evaluating the Model

### Why this step?

After training the model, we use the `predict` method to make predictions on the unseen testing data. We then evaluate the model's performance by comparing its predictions (`y_pred`) to the actual test values (`y_test`) using a metric like `accuracy_score`.

```python
# Make predictions on the test set
y_pred = dtree.predict(X_test)

# Evaluate the model's accuracy
accuracy = accuracy_score(y_test, y_pred)
print(f"Model Accuracy: {accuracy:.2f}")
```
<img width="1024" height="467" alt="Screenshot 2025-08-05 110325" src="https://github.com/user-attachments/assets/3e6d829f-f7cf-4799-9245-2f05e299d1ff" />

### Step 7. Evaluating Model Performance with a Confusion Matrix

**Why this step?**
A confusion matrix is a powerful tool to evaluate a classification model. It provides a detailed breakdown of correct and incorrect predictions for each class, offering more insight than a simple accuracy score.

```python
# Import the required libraries
from sklearn.metrics import confusion_matrix
import seaborn as sns
import matplotlib.pyplot as plt

# Assuming 'y_test' and 'y_pred' are from your Decision Tree model's prediction step
cm = confusion_matrix(y_test, y_pred)

# Visualize the confusion matrix using a heatmap
plt.figure(figsize=(10, 7))
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues',
            xticklabels=dtree.classes_, yticklabels=dtree.classes_)
plt.xlabel('Predicted')
plt.ylabel('Actual')
plt.title('Decision Tree Confusion Matrix')
plt.show()
```

<img width="1025" height="437" alt="Screenshot 2025-08-05 110349" src="https://github.com/user-attachments/assets/94f2b17d-6a52-402c-8b88-f7948f6c05b1" />



## Random Forest Classifier: Theory & Working Principle

### What is a Random Forest?

A Random Forest is an **ensemble learning method** for classification and regression that operates by constructing a multitude of **decision trees** at training time. The "forest" is the collection of these trees. To make a prediction, it aggregates the predictions from all the individual trees. For classification, this is typically done through a **majority vote**, while for regression, it's done by averaging the outputs. This approach helps to overcome the problem of **overfitting** that individual decision trees are prone to.

-----

### **How It Works (Step-by-Step)**

1.  **Select Random Subsets of Data**: The algorithm uses a technique called **Bootstrap Aggregation (Bagging)** to create multiple subsets of the training data by sampling with replacement. Each subset is used to train a different tree.
2.  **Select Random Subsets of Features**: At each split in each tree, the algorithm only considers a random subset of features, not all features. This adds more randomness and helps to reduce the correlation between trees.
3.  **Build a Decision Tree**: A decision tree is built on each of the data and feature subsets. The trees are grown to their maximum depth without pruning.
4.  **Aggregate Predictions**: For a new data point, each tree in the forest makes a prediction. The final prediction is determined by a majority vote (for classification) or an average (for regression) of all tree predictions.

-----

### **Mathematics Behind It**

Random Forest reduces variance and bias by averaging multiple independent trees.

  - **Bagging**: Creates diversity in the training data, ensuring trees are not identical.
  - **Random Feature Selection**: Prevents any single feature from dominating the entire model, further decorrelating the trees.

The final prediction is based on the mode of the class predictions from all trees:
\[ \\hat{y} = \\text{mode}{ C\_1(\\mathbf{x}), C\_2(\\mathbf{x}), \\dots, C\_B(\\mathbf{x}) } \]
Where \\( C_b(\mathbf{x}) \\) is the prediction of the \\( b^{th} \\) tree.

-----

### Why Use Random Forest?

  - **High Accuracy**: Generally produces very good results and is more accurate than a single decision tree.
  - **Reduces Overfitting**: By averaging multiple trees, it reduces the risk of overfitting.
  - **Less Sensitive to Outliers**: The bagging approach makes it more robust to outliers.
  - **Feature Importance**: Provides a good measure of feature importance, indicating which features contributed most to the model's performance.

-----

### **Limitations**

  - **Less Interpretable**: It's a "black box" model, making it harder to interpret than a single decision tree.
  - **Computationally Intensive**: Can be slower to train than other models due to the large number of trees.
  - **Requires More Memory**: Needs to store multiple trees, which can take up a lot of memory.

-----

### **Application to Our Project**

We will use a Random Forest Classifier as an improved version of our Decision Tree model. It will also predict `review_score` but with higher accuracy and better generalization, providing a more reliable understanding of what factors influence customer satisfaction.

-----

## Step 1. Loading the Required Libraries

**Why?**
We need to import the `RandomForestClassifier` and other necessary libraries for data preparation and evaluation.

```python
# Import required libraries
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score
```

## Step 2. Loading the Transformed Dataset

**Why?**
We use the same cleaned dataset for a consistent comparison with the Decision Tree model.

```python
# Load the transformed dataset
df = pd.read_csv('../data/transformed/transformed_data.csv')
```

## Step 3. Preparing the Data for the Model

### Why this step?

We use the same features (`payment_value`, `freight_value`) and target (`review_score`) to ensure a direct comparison between the two models.

```python
# Define features (X) and target (y)
X = df[['payment_value', 'freight_value']]
y = df['review_score']
```

## Step 4. Splitting the Data

### Why split the data?

We use the same 80/20 split to train and test the Random Forest model, ensuring a fair evaluation of its performance on unseen data.

```python
# Split data into training and testing sets (80% train, 20% test)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

## Step 5. Building and Training the Model

### Why this step?

We instantiate the `RandomForestClassifier` with a specific number of trees (e.g., 100) and train it on our training data.

```python
# Initialize the Random Forest classifier
rf = RandomForestClassifier(n_estimators=100, random_state=42)

# Train the model
rf.fit(X_train, y_train)
```

## Step 6. Making Predictions and Evaluating the Model

### Why this step?

We make predictions on the test set and calculate the accuracy score to measure the model's performance. The accuracy of the Random Forest model is expected to be higher than the single Decision Tree model.

```python
# Make predictions on the test set
y_pred_rf = rf.predict(X_test)

# Evaluate the model's accuracy
accuracy_rf = accuracy_score(y_test, y_pred_rf)
print(f"Random Forest Model Accuracy: {accuracy_rf:.2f}")
```
<img width="1024" height="534" alt="Screenshot 2025-08-05 110407" src="https://github.com/user-attachments/assets/c33ade65-df0e-4c1e-a4f6-20ae6baa56d8" />

### Dashboards
Dashboard section done by: Hana Gashaw 
## Power BI Dashboard: Interactive Reports

### What is the purpose of this dashboard?
The Power BI dashboard serves as a central hub for interactive and comprehensive visualization of the key insights and findings from our **Exploratory Data Analysis (EDA)** and **Data Mining** processes. Designed to be accessible to both technical and non-technical stakeholders, this dashboard allows for a dynamic exploration of the data. It transforms raw data and complex model outputs into clear, actionable business intelligence, helping to inform strategic decisions across the business.

---

### **Dashboard Pages & Key Insights**

#### Page 1: Sales and Revenue Overview
This page provides a robust, high-level view of the company's financial performance. It's designed to give a quick yet detailed understanding of sales dynamics. It includes key performance indicators (KPIs) such as total revenue, total number of orders, and average order value, presented in a clean and easy-to-read format. Visualizations on this page include line charts that track sales and revenue trends over time, allowing users to quickly identify peak seasons, dips, and overall growth patterns. This is complemented by bar charts that break down sales by `product_category` and `customer_state`, providing geographical and product-based insights. Interactive filters allow for dynamic analysis by specific time periods, product categories, or customer locations, making it a valuable tool for understanding the company's financial health and market distribution.

<img width="1591" height="902" alt="Screenshot 2025-08-05 113151" src="https://github.com/user-attachments/assets/37a6f2ea-e02a-4474-8f98-e724ee19002e" />


#### Page 2: Customer Segmentation & Satisfaction
This page is the core of our data mining findings, combining the results of our unsupervised and supervised learning models. It is dedicated to visualizing both the customer segments identified and the factors driving customer satisfaction. The page presents scatter plots or bar charts showing the distinct customer clusters identified by the **K-Means algorithm**. These clusters are often labeled with descriptive titles like "high-value customers," "frequent buyers," and "budget shoppers," giving a clear picture of the different types of customers and their characteristics based on metrics such as `payment_value` and `purchase_frequency`.

Alongside this, the page features visualizations from the **Decision Tree** and **Random Forest** models. This includes a breakdown of `review_scores` (e.g., a pie chart showing the percentage of 5-star, 4-star, etc., reviews) to assess overall satisfaction. There are also charts that show the relationship between `review_score` and features like `freight_value` or `payment_value`. This helps to answer critical business questions like, "Do customers who pay more for freight give lower reviews?" This page provides a holistic view of who the customers are and what influences their satisfaction, directly linking our data mining efforts to actionable business insights.

<img width="1669" height="863" alt="Screenshot 2025-08-05 113224" src="https://github.com/user-attachments/assets/e0ca18a4-b7a7-485c-aebf-f0b21c461db9" />

