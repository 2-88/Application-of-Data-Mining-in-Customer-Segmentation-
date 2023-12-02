# Multinational-E-commerce- Retail-Customer-Segmentation-with-Association-Rule-Mining-(RFM Analysis)-and-Data-Mining-(K-Means Clustering)-using-SQL-and-Python
In this project I used RFM Analysis with SQL and K-Means Clustering with Python to segment the customers of an e-commerce retail store. Marketing strategies were developed to increase customer lifetime value based on the purchasing beviour of customer segments identified. 

## Abstract
Online enterprises strive to achieve a competitive advantage and improve customer satisfaction by employing market segmentation. This strategy enables them to customize their marketing efforts and provide individualized experiences to different customer groups who share common characteristics. With the expansion of e-commerce, handling substantial customer data and dealing with the lack of face-to-face interaction present distinctive obstacles, underscoring the importance of advanced segmentation methods in thriving within the digital environment.
The objective of this project analyzes the lifetime value of customers of a multinational e-commerce retail store by employing RFM Analysis and K-Means clustering techniques. 

## Description of the dataset
The dataset has nine columns namely Invoice, StockCode, Description, Quantity, InvoiceDate, Price, Customer ID, Country, and Amount. The Customer ID is Nominal with a 5-digit integral number that uniquely identifies each customer. The Date is Numeric and shows the day, month, year, and time when each transaction was recorded. The Description shows the name of the product.

## Data Pre-processing
### Content of the dataset
The dataset had 541910 rows and nine columns as visualized in the table below. 
![](https://github.com/2-88/Application-of-Data-Mining-in-Customer-Segmentation-/blob/main/Screenshot%20(12).png)
 

### Visualization of the dataset
Twenty most sold products of the business are shown in the chart below. White Hanging Heart-Light holder was the most sold product and Alarm Clock Bakelike Green was the least sold product.
 ![](https://github.com/2-88/Application-of-Data-Mining-in-Customer-Segmentation-/blob/main/Screenshot%20(13).png)

### Missing values
To prepare the dataset for customer segmentation, an initial step involved data cleaning. During this initial cleaning process, the dataset was examined for missing values, and it revealed that there were 136,534 missing values in the dataset, as displayed in the output below.

![](https://github.com/2-88/Application-of-Data-Mining-in-Customer-Segmentation-/blob/main/Screenshot%20(14).png)

 
### Checking data types
The data types were also checked as shown below

![](https://github.com/2-88/Application-of-Data-Mining-in-Customer-Segmentation-/blob/main/Screenshot%20(15).png) 

### Data Transformation
 All invoices without a customer ID were dropped. Invoices with zero prices as well as ones with invoice numbers containing the letter "C", showing a cancelled transaction were also dropped. Data was then aggregated by most recent date and grouped by customer using customer ID.

![]( https://github.com/2-88/Application-of-Data-Mining-in-Customer-Segmentation-/blob/main/Screenshot%202023-11-05%20at%2015-04-05%20Google%20Colaboratory(1).png) 

The ouput of the above query is shown below.

![](https://github.com/2-88/Application-of-Data-Mining-in-E-Commerce-Customer-Segmentation-/blob/main/Picture3.png).


## RFM Analysis
RFM analysis requires the creation of three measures or scores namely recency, frequency, and monetary value, which together show the value of a customer. The customers are then segmented based on their scores for recency, frequency, and monetary value.
Recency measures how recent the transaction was, and the most recent date was stored as the value of Recency. Frequency measures how many times a customer has transacted, and Monetary value measures the value of the item the customer acquires.

### Creation of RFM variables- Recency, Frequency and Monetary value and Aggregating data by customer
The SQL query below was used to create the variables Recency, Frequency and Monetary Value
 
![](https://github.com/2-88/Application-of-Data-Mining-in-Customer-Segmentation-/blob/main/Screenshot%202023-11-05%20at%2015-11-07%20Google%20Colaboratory.png) 


### Changing Recency from object datatype to date-time format and creating a date variable that records recency, a snapshot date and the estimation of the days passed
The Recency values were changed to date format. There is also a requirement to transform them into numeric values that express the time gap between the transaction's initiation date and the date designated for analysis. To accomplish this, we introduce a reference date known as the "snapshot date," which aligns with the date meant for the analysis. By subtracting the initiation date from the snapshot date, we can calculate the number of days that have passed within the dataset's analysis period. The snapshot date is provided below for your reference.  

![](https://github.com/2-88/Application-of-Data-Mining-in-E-Commerce-Customer-Segmentation-/blob/main/Picture1.png)

### Aggregating data by each customer
Data is aggregated by each customer after obtaining the time passed. This is shown in the table below.

![](https://github.com/2-88/Application-of-Data-Mining-in-E-Commerce-Customer-Segmentation-/blob/main/Picture2.png).
 


## K-MEANS Clustering
The algorithm operates by assigning data points to clusters, grouping together data points that are near one another. To initiate the process, the algorithm necessitates the determination of the required number of clusters. It begins by selecting data points equal to the specified number of clusters as centroids and subsequently adds nearby data points to these centroids, forming clusters.
Following this, the centroids are recalculated, and this iterative process continues until the data points can no longer be repositioned. Throughout this process, the algorithm considers both the distances between data points and the distances between clusters. This consideration ensures that there is no overlap or ambiguity in the assignment of data points to clusters. One advantage of the K-Means algorithm is that it is a data mining technique that explores the patterns in a data without necessarily knowing its labels. The RFM values were then used to perform the K-Means clustering to have the customers partitioned into different segments.
K-Means clustering works if the dataset is normally distributed and has a mean 0 and variance 1. The algorithm also requires all missing values to be dropped. 

#Checking for Mean and Standard Deviation of the dataset
The dataset was standardized using the standardscaler function scaler = StandardScaler (). After the standardization it is asserted that it has a mean of 0 and a variance of 1 and the result is shown below.
 
##Checking the distribution of the dataset
###Distribution of the dataset before normalization
From the Distribution Analysis below, the Recency and Monetary Value have longer tail on the right side and the Frequency has longer tail on the left, which showed they were not normally distributed. The distribution of Monetary Value showed the distribution was skewed to the left which means customers with lower Monetary Value were the majority. The distribution of the Recency showed most of the customers were new and the distribution of Frequency showed most of the customers do not make purchases frequently.
  
 	
### Normalization of the dataset
Because K-Means clustering works with only normally distributed data and the non-linear data will require normalization, the SciPy.stats.boxcox() function is used to transform the non-linear distribution to achieve a normal distribution. The normal distribution follows the Pareto Principle which assumes that 80% of the output comes from the 20% of all causes. That is, the best comes from the top 20%. The transformation after the boxcox makes the data now look bell-shaped and normally distributed as shown below.

 

### Determining the number of clusters for K-Means
The Elbow method was used to determine the optimal number of clusters for the K-Means. The optimal number of clusters is arrived at where the graph forms an elbow. The number of clusters obtained using this method was 3 as shown below. Hence, K=3.
 

### The outcome of the K-Means Clustering and the Analysis of the Clusters
Cluster 1 had the highest number of customers followed by Cluster 0 and Cluster 2 as shown below.
In summary, Cluster 0 had 293 Customer 1Ds, Cluster 1 had 358 Customer IDs and Cluster 2 had 279 Customer ID as visualized in figure 7 below.  The mean values of the recency, frequency, and monetary value for each of the clusters are also shown below.

 
 
Mean:
Table 7
 

### List of customers and their segments based on their recency, frequency, and monetary value
Table 8 below is the outcome of the customer segmentation showing Customer IDs and their segments/ clusters and the table can be queried for which segment an individual customer belongs to.
Table 8
 


## Customer Lifetime Value
 
Figure 7

The snake plot in figure 5 above is used to show the value of customers in the three clusters identified with the K-Means across Recency of transactions, Frequency of purchases and the Monetary Value. From the snake plot, customers in Cluster 0 had the highest Recency, the second highest Monetary Value and a very low frequency. Customers in Cluster 1 had the second highest Recency, the highest Monetary Value, and the highest Frequency. Customers in Cluster 2 had the lowest Recency and Monetary Value as well as a very low Frequency.
### Proposed marketing strategy based on K-Means Clustering/ Segmentation
The behavioral pattern of customers in cluster/ segment 0 shows they are new customers. They had purchased a lot of products recently and they are moderately high spenders and the number of times they have transacted with the business was low. For this segment the Marketing Department must come up with customer retention strategies like promotions in the form of a membership card with discounts, after-sales delivery and sending the adverts for new products or ones they have not bought yet. Market basket analysis could be used to identify the products such segment of customers buys together.
Customers in cluster 1 had low recency, very high monetary value, and very high frequency. Per the behavioral pattern of these customers, they have not been purchasing a lot of products like they use to do although this group of customers use to be the business’ largest spender group. They used to make a lot of purchases in the past. The Marketing Department must be concerned about this group of customers because the business has been losing them recently. They are either unhappy with the services or have found a better offer from a competitor. There is the need for the Marketing Department to carry out a competitor survey, especially about pricing of products and offers from the competitors.
Customers in cluster 2 had the lowest recency, monetary value, and frequency. This means their purchase of products is declining recently, they are a low-income group or spender and have not purchased a lot of products from the business. This behavior is best suited for a risky customer. The Marketing Department must not spend a lot of resources to attract more such customers and should not have to sell on credit to them or a hire purchase because they are low-income group and do not want to spend much on those types of products.

