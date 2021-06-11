# Amazon_Vine_Analysis

Module 16


Background
Since your work with Jennifer on the SellBy project was so successful, you’ve been tasked with another, larger project: analyzing Amazon reviews written by members of the paid Amazon Vine program. The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review.

In this project, you’ll have access to approximately 50 datasets. Each one contains reviews of a specific product, from clothing apparel to wireless products. You’ll need to pick one of these datasets and use PySpark to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. Next, you’ll use PySpark, Pandas, or SQL to determine if there is any bias toward favorable reviews from Vine members in your dataset. Then, you’ll write a summary of the analysis for Jennifer to submit to the SellBy stakeholders.

What You're Creating
This new assignment consists of two technical analysis deliverables and a written report. You will submit the following:

Deliverable 1: Perform ETL on Amazon Product Reviews
Deliverable 2: Determine Bias of Vine Reviews
Deliverable 3: A Written Report on the Analysis (README.md)
Files
Use the following links to download the Challenge starter codes.

Download the SQL table schema (Links to an external site.).

Download the Amazon ETL starter code (Links to an external site.).

Before You Start
Create a new GitHub repository entitled "Amazon_Vine_Analysis", and initialize the repository with a README.

IMPORTANT
Be sure to regularly monitor your AWS usage so you don’t go above the free tier. Consult Lessons 16.9.2 and 16.9.3 for more on shutting down your AWS instances and checking your AWS billing, respectively.

Deliverable 1: Perform ETL on Amazon Product Reviews (40 points)
Deliverable 1 Instructions
Using your knowledge of the cloud ETL process, you’ll create an AWS RDS database with tables in pgAdmin, pick a dataset from the Amazon Review datasets (Links to an external site.), and extract the dataset into a DataFrame. You'll transform the DataFrame into four separate DataFrames that match the table schema in pgAdmin. Then, you'll upload the transformed data into the appropriate tables and run queries in pgAdmin to confirm that the data has been uploaded.


From the following Amazon Review datasets (Links to an external site.), pick a dataset that you would like to analyze. All the datasets have the same schemata, as shown in this image:
The format and information of Amazon Review datasets columns.

Create a new database with Amazon RDS just as you did in this module.

In pgAdmin, create a new database in your Amazon RDS server that you just create.

Download the challenge_schema.sql file to your computer.

In pgAdmin, run a new query to create the tables for your new database using the code from the challenge_schema.sql file.

After you run the query, you should have the following four tables in your database: customers_table, products_table, review_id_table, and vine_table.
Download the Amazon_Reviews_ETL_starter_code.ipynb file, then upload the file as a Google Colab Notebook, and rename it Amazon_Reviews_ETL.


First extract one of the review datasets, then create a new DataFrame.
Next, follow the steps below to transform the dataset into four DataFrames that will match the schema in the pgAdmin tables:
NOTE
Some datasets have a large number of rows, which will affect the time it takes to complete the following steps.

The customers_table DataFrame
To create the customers_table, use the code in the Amazon_Reviews_ETL_starter_code.ipynb file and follow the steps below to aggregate the reviews by customer_id.

Use the groupby() function on the customer_id column of the DataFrame you created in Step 6.
Count all the customer ids using the agg() function by chaining it to the groupby() function. After you use this function, a new column will be created, count(customer_id).
Rename the count(customer_id) column using the withColumnRenamed() function so it matches the schema for the customers_table in pgAdmin.
The final customers_table DataFrame should look like this:
The customers_table DataFrame,

The products_table DataFrame
To create the products_table, use the select() function to select the product_id and product_title, then drop duplicates with the drop_duplicates() function to retrieve only unique product_ids. Refer to the code snippet provided in the Amazon_Reviews_ETL_starter_code.ipynb file for assistance.

The final products_table DataFrame should look like this:

The products_table DataFrame,

The review_id_table DataFrame
To create the review_id_table, use the select() function to select the columns that are in the review_id_table in pgAdmin (as shown in the following image), and convert the review_date column to a date using the code snippet provided in the Amazon_Reviews_ETL_starter_code.ipynb file.

The final review_id_table DataFrame should look like this:

The review_id_table DataFrame,

The vine_table DataFrame
To create the vine_table, use the select() function to select only the columns that are in the vine_table in pgAdmin (as shown in the following image).

The final vine_table DataFrame should look like this:

The vine_table DataFrame.

Load the DataFrames into pgAdmin
Make the connection to your AWS RDS instance.
Load the DataFrames that correspond to tables in pgAdmin.
In pgAdmin, run a query to check that the tables have been populated.
IMPORTANT
Before uploading anything to GitHub be sure to remove all sensitive information such as passwords and connection strings. If you have accidentally done so already see this link (Links to an external site.) for more information.

When you’re done, export your Amazon_Reviews_ETL Google Colab Notebook as an ipynb file, and save it to your Amazon_Vine_Analysis GitHub repository.
! https://github.com/Dybondzy/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL.ipynb

Deliverable 1 Requirements
You will earn a perfect score for Deliverable 1 by completing all requirements below:

The Amazon_Reviews_ETL.ipynb file does the following:
An Amazon Review dataset is extracted as a DataFrame (10 pt)
The extracted dataset is transformed into four DataFrames with the correct columns (20 pt)
All four DataFrames are loaded into their respective tables in pgAdmin (10 pt)
Deliverable 2: Determine Bias of Vine Reviews (40 points)
Deliverable 2 Instructions
Using your knowledge of PySpark, Pandas, or SQL, you’ll determine if there is any bias towards reviews that were written as part of the Vine program. For this analysis, you'll determine if having a paid Vine review makes a difference in the percentage of 5-star reviews.


Filter the data and create a new DataFrame or table to retrieve all the rows where the total_votes count is equal to or greater than 20 to pick reviews that are more likely to be helpful and to avoid having division by zero errors later on.

Filter the new DataFrame or table created in Step 1 and create a new DataFrame or table to retrieve all the rows where the number of helpful_votes divided by total_votes is equal to or greater than 50%.

If you use the SQL option below, you’ll need to cast your columns as floats using WHERE CAST(helpful_votes AS FLOAT)/CAST(total_votes AS FLOAT) >=0.5.
Filter the DataFrame or table created in Step 2, and create a new DataFrame or table that retrieves all the rows where a review was written as part of the Vine program (paid), vine == 'Y'.

Repeat Step 3, but this time retrieve all the rows where the review was not part of the Vine program (unpaid), vine == 'N'.

Determine the total number of reviews, the number of 5-star reviews, and the percentage of 5-star reviews for the two types of review (paid vs unpaid).


Using PySpark
Create a new Google Colab Notebook, and name it Vine_Review_Analysis.
Extract the dataset you used in Deliverable 1.
Recreate the vine_table, and perform your analysis using the steps above.
Export your Vine_Review_Analysis Google Colab Notebook as an ipynb file, and save it to your Amazon_Vine_Analysis GitHub repository.
Using Pandas
From pgAdmin, export the vine_table as a CSV file, and save it to your Amazon_Vine_Analysis GitHub repository.
Create a new Jupyter Notebook, and name it Vine_Review_Analysis.ipynb.
Read in the vine_table.csv file as a DataFrame, and perform your analysis using the steps above.
Save your Vine_Review_Analysis.ipynb file to your Amazon_Vine_Analysis GitHub repository.
Using SQL in pgAdmin
From your AWS database, export the vine_table as a CSV file and save it to your Amazon_Vine_Analysis GitHub repository.
In pgAdmin, create a new database that is not linked to your AWS RDS instance. This way, you don’t have to keep incurring charges while connected to your AWS RDS instance.
Create a new SQL file and name it Vine_Review_Analysis.sql.
Recreate the vine_table using the schema provided in the challenge_schema.sql file.
Import the vine_table.csv file into the table, and perform your analysis using the steps above.
Save all your SQL queries to the Vine_Review_Analysis.sql file, then add it to your Amazon_Vine_Analysis GitHub repository.
Deliverable 2 Requirements
You will earn a perfect score for Deliverable 2 by completing all requirements below:

The analysis does the following:
There is a DataFrame or table for the vine_table data using one of three methods above (5 pt)
The data is filtered to create a DataFrame or table where there are 20 or more total votes (5 pt)
The data is filtered to create a DataFrame or table where the percentage of helpful_votes is equal to or greater than 50% (5 pt)
The data is filtered to create a DataFrame or table where there is a Vine review (5 pt)
The data is filtered to create a DataFrame or table where there isn’t a Vine review (5 pt)
The total number of reviews, the number of 5-star reviews, and the percentage 5-star reviews are calculated for all Vine and non-Vine reviews (15 pt)

! https://github.com/Dybondzy/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL.ipynb

Deliverable 3: A Written Report on the Analysis (20 points)
Deliverable 3 Instructions
For this part of the Challenge, you’ll write a report that summarizes the analysis you performed in Deliverable 2.

The report should contain the following:

Overview of the analysis: Explain the purpose of this analysis.

Results: Using bulleted lists and images of DataFrames as support, address the following questions:

How many Vine reviews and non-Vine reviews were there?
How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?
What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?
Summary: In your summary, state if there is any positivity bias for reviews in the Vine program. Use the results of your analysis to support your statement. Then, provide one additional analysis that you could do with the dataset to support your statement.

Deliverable 3 Requirements
Structure, Organization, and Formatting (6 points)
The written analysis has the following structure, organization, and formatting:

There is a title, and there are multiple sections (2 pt)
Each section has a heading and subheading (2 pt)
Links to images are working, and code is formatted and displayed correctly (2 pt).
Analysis (14 points)
The written analysis has the following:

Overview of the analysis of the Vine program:

The purpose of this analysis is well defined (3 pt)
Results:

There is a bulleted list that addresses the three questions for unpaid and paid program reviews (7 pt)
Summary:

The summary states whether or not there is bias, and the results support this statement (2 pt)
An additional analysis is recommended to support the statement (2 pt)
Submission
Once you’re ready to submit, make sure to check your work against the rubric to ensure you are meeting the requirements for this Challenge one final time. It’s easy to overlook items when you’re in the zone!

As a reminder, the deliverables for this Challenge are as follows:

Deliverable 1: Perform ETL on Amazon Product Reviews
Deliverable 2: Determine Bias of Vine Reviews
Deliverable 3: A Written Report on the Analysis (README.md)
Upload the following to your Amazon_Vine_Analysis GitHub repository:
! https://github.com/Dybondzy/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL.ipynb

Your Amazon_Reviews_ETL.ipynb file.
! https://github.com/Dybondzy/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL.ipynb

Your Vine_Review_Analysis.ipynb or Vine_Review_Analysis.sql file.
An updated README.md that has your written analysis.
! https://github.com/Dybondzy/Amazon_Vine_Analysis/edit/main/README.md

To submit your challenge assignment in Canvas, click Submit, then provide the URL of your Amazon_Vine_Analysis GitHub repository for grading.
