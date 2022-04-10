# Amazon Reviews: Paid vs Unpaid

## Overview
The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products in exchange of incentives. We have access to approximately 50 such Amazon Review datasets each containing reviews of a specific product ranging from clothing apparel to electronics.

## Purpose
The purpose of this analyses are two folds. First, **ETL** will be performed to access the data from AWS, process using PySpark and load to pgAdmin. Second, reviews from the Vine program will be compared to the unpaid reviews to detect **bias**, if any.

As an example, reviews dataset on **Watches** will be used.

## Resources
- Data Source: Amazon Review datasets
- Software: Google Colab Notebook, PostgreSQL 13.5, pgAdmin 4, AWS

## Results
Four different datafames were created from the Watch Review dataset by removing duplicates and null values. The dataframes are shown below:

- **Customers_df**, with unique customer IDs

![customers_df](https://github.com/Nusratnimme/Amazon_Vine_Analysis/blob/main/Images/customers_df.png)

- **Products_df**, with unique product IDs and titles

![Products_df](https://github.com/Nusratnimme/Amazon_Vine_Analysis/blob/main/Images/products_df.png)

- **Review_id_df**

![review_id_df](https://github.com/Nusratnimme/Amazon_Vine_Analysis/blob/main/Images/review_id_df.png)

- **Vine_df**, containing data on ratings and whether they come from the Vine program

![vine_table_df](https://github.com/Nusratnimme/Amazon_Vine_Analysis/blob/main/Images/vine_df.png)

These dataframes are then loaded into **pgAdmin** by connecting to an **AWS RDS instance**.

For the analyses on Vine program reviews bias, vine table dataframe was filtered to keep records with a total votes count of 20 or more, and again to only keep records where the proportion of helpful_votes to total_votes is 50% or more. Finally the dataframe was split into paid and unpaid reviews.

Below are the key findings:

- There are a total of 8390 reviews for watches with 47 paid and 8,343 unpaid ones.

![Total_reviews](https://github.com/Nusratnimme/Amazon_Vine_Analysis/blob/main/Images/Total_reviews.png)

- 15 of the 47 paid reviews are 5-stars compared to 4,318 of 8,343 unpaid reviews.

![Total_paid_vs_unpaid_reviews](https://github.com/Nusratnimme/Amazon_Vine_Analysis/blob/main/Images/Toatal_paid_vs_unpaid_reviews.png)

- Therefore, about 32% of paid Vine reviews are 5-stars compared with 52% of the unpaid reviews with 5-stars.

![Percentage_paid_vs_unpaid_reviews](https://github.com/Nusratnimme/Amazon_Vine_Analysis/blob/main/Images/Percentage_paid_vs_unpaid_reviews.png)

## Summary

### Conclusion
From our data, we can conclude that there was no bias in the paid reviews compared to the unpaid ones. If anything, paid reviewers were more conservative in giving a 5-stars review.

### Recommendation
Below are a couple of recommendations to improve the analyses:
- We could use reviews from only **verified purchasers**. This would increase reliability of our data;
- Instead of looking at only 5-starts reviews, we could look at the **distribution** of the reviews. For example, although we found no bias in paid reviews for 5-starts ratings, could the paid reviews be more likely to give a 4-stars rating compared to unpaid ones? How would the average or weighted average (helpful votes as weights) ratings between paid and unpaid compare?
