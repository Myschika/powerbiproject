# Shopify App Analysis

## Project Overview
This project aimed to analyze the landscape of apps on the Shopify platform using data scraped from publicly available Shopify websites. The goal is to identify key factors contributing to the success of a Shopify app by leveraging Power BI for data visualization and insights.

## Dataset
The dataset (`shopify.xlsx`) consists of four tables:
- **apps**: Contains details of apps available on the Shopify App Store.
- **apps_categories**: A join table connecting apps with their respective categories.
- **categories**: Lists the different categories of apps.
- **reviews**: Stores user reviews, ratings, comments, and developer responses.

## Analysis Breakdown

### Part 1: App Landscape
**Objective:** Identify key statistics and trends in Shopify apps.

1. **KPI Card**: Displays the unique number of apps in the dataset.
   ![Image_Alt](https://github.com/Myschika/powerbiproject/blob/b961e584735f79572e5356addffdca579eb6b2ef/Screenshot%201.png)
2. **Line Chart**: Plots the sum of `review_count` over time (`lastmod` date) to visualize review trends.
    ![Image_Alt](https://github.com/Myschika/powerbiproject/blob/3f7aa8e880c1242df7ba2ca55d244840b573f483/Screenshot%202.png) 
3. **Scatterplot**: Shows the relationship between `reviews_count` (X-axis) and `average rating` (Y-axis), with an annotation summarizing insights.
   ![Image_Alt](https://github.com/Myschika/powerbiproject/blob/3f7aa8e880c1242df7ba2ca55d244840b573f483/Screenshot%203-%20not%20summarised.png)

### Part 2: Reviews
**Objective:** Analyze the impact of user reviews and developer responses.

1. **Helpful Reviews Calculation**:
   - Create a new column `helpful_reviews` using the DAX formula:  
     ```DAX
     helpful_reviews = rating * (1 + helpful_count)
     ```
   - Display the average `helpful_reviews` value using a KPI Card.
   -  ![Image_Alt](https://github.com/Myschika/powerbiproject/blob/3f7aa8e880c1242df7ba2ca55d244840b573f483/Screenshot%204.png)
     
2. **Developer Response Impact**:
   - Create a new column `developer_answered`:  
     ```DAX
     developer_answered = IF(ISBLANK(developer_reply), 0, 1)
     ```
   - Generate a scatterplot comparing `average rating` (Y-axis) with `developer_answered` (X-axis).
   - ![Image_Alt](https://github.com/Myschika/powerbiproject/blob/3f7aa8e880c1242df7ba2ca55d244840b573f483/Screenshot%205.png)

### Part 3: App Reviews
**Objective:** Investigate relationships between reviews and app developers.

1. **Data Model Relationship**:
   - Create a **many-to-one** relationship between `Reviews` (`app_id`) and `Apps` (`id`).
   - ![Image_Alt](https://github.com/Myschika/powerbiproject/blob/3f7aa8e880c1242df7ba2ca55d244840b573f483/Screenshot%206.png)
2. **Developer Performance Analysis**:
   - **Bar Chart 1**: Developer (X-axis) vs. Sum of Ratings (Y-axis).
   - **Bar Chart 2**: Developer (X-axis) vs. Average Helpful Review Score (Y-axis), correcting for misleading high rating sums.
   - ![Image_Alt](https://github.com/Myschika/powerbiproject/blob/3f7aa8e880c1242df7ba2ca55d244840b573f483/Screenshot%207.png)
3. **Developer Responsiveness**:
   - **Bar Chart 3**: Developer (X-axis) vs. `developer_answered` count.
   - Apply a filter to include only apps with `reviews_count > 500`.
   - ![Image_Alt](https://github.com/Myschika/powerbiproject/blob/3f7aa8e880c1242df7ba2ca55d244840b573f483/Screenshot%208.png)

## Conclusion
This analysis provided insights into the Shopify app ecosystem by evaluating review trends, developer responsiveness, and rating distributions. Power BI's visualization capabilities help uncover patterns that influence app success, assisting in data-driven decision-making for app developers and stakeholders.
