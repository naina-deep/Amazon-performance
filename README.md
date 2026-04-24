# Amazon-performance

>Amazon Data Analysis using PySpark

>>>Project Description

This project focuses on analyzing an e-commerce dataset using PySpark to extract meaningful insights related to product performance, pricing trends, and customer behavior.

The dataset contains information such as product category, price, stock availability, ratings, reviews, brand, and date of addition. Using PySpark, the data is processed efficiently to perform various analytical operations including aggregation, filtering, sorting, and window functions.

Key operations performed in this project include:

* Category-wise analysis of pricing and product distribution
* Identification of high-demand products using a custom demand score (Rating × Reviews)
* Brand performance evaluation based on customer ratings and reviews
* Stock and inventory analysis
* Monthly trend analysis using date-based transformations
* Ranking of products within categories using window functions

The project demonstrates how PySpark can be used to handle structured datasets and generate business insights that can help in decision-making for e-commerce platforms.

Overall, this analysis highlights patterns in customer preferences, product demand, and pricing strategies, showcasing the practical application of big data tools in real-world scenarios.



>>>>>>Queries and Functions Used

>The analysis was performed using PySpark DataFrame operations. The following queries and transformations were implemented on the dataset:

>> Data Preparation

* Loaded CSV dataset using `spark.read.csv()` with header and schema inference
* Converted date column using `to_date()` function
* Created new columns using `withColumn()`

### Feature Engineering

* Created a custom metric:

  * **Demand Score = Rating × Reviews**
  * Implemented using:

    ```
    withColumn("Demand_Score", col("Rating") * col("Reviews"))
    ```

### Aggregation and Grouping

* Category-wise average price:

  ```
  groupBy("Category").avg("Price")
  ```
* Category-wise product count:

  ```
  groupBy("Category").count()
  ```
* Brand-wise average rating:

  ```
  groupBy("Brand").avg("Rating")
  ```
* Total reviews per brand:

  ```
  groupBy("Brand").sum("Reviews")
  ```

### Sorting and Ranking

* Top products based on demand:

  ```
  orderBy(desc("Demand_Score"))
  ```
* Most expensive and least expensive products:

  ```
  orderBy(desc("Price"))
  orderBy("Price")
  ```

### Filtering

* High demand products:

  ```
  filter(col("Demand_Score") > 1000)
  ```

### Time-Based Analysis

* Extracted month from date:

  ```
  withColumn("Month", month("Date_Added"))
  ```
* Monthly average pricing:

  ```
  groupBy("Month").avg("Price")
  ```
* Monthly product count:

  ```
  groupBy("Month").count()
  ```

### Window Functions (Advanced)

* Ranking products within each category:

  ```
  Window.partitionBy("Category").orderBy(desc("Rating"))
  ```
* Assigning rank:

  ```
  withColumn("Rank", rank().over(windowSpec))
  ```
* Identifying top product per category:

  ```
  row_number().over(windowSpec)
  ```

### Column Selection and Display

* Selected relevant columns for analysis:

  ```
  select("Category","Price","Rating","Reviews")
  ```
* Displayed results using:

  ```
  show()
  ```

These queries demonstrate the use of PySpark for data transformation, aggregation, filtering, and advanced analytical operations.
