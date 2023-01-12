# customer-segmentation

In this project, your task is to identify major customer segments on a transnational data set which contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based and registered non-store online retail.The company mainly sells unique all-occasion gifts. Many customers of the company are wholesalers.

# Problem description : 

In this project, your task is to identify major customer segments on a transnational data set which contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based and registered non-store online retail.The company mainly sells unique all-occasion gifts. Many customers of the company are wholesalers.


# Data description :

1. InvoiceNo: Invoice number. Nominal, a 6-digit integral number uniquely assigned to each transaction. If this code starts with letter 'c', it indicates a cancellation.
2. StockCode: Product (item) code. Nominal, a 5-digit integral number uniquely assigned to each distinct product.
3. Description: Product (item) name. Nominal.
4. Quantity: The quantities of each product (item) per transaction. Numeric.
5. InvoiceDate: Invice Date and time. Numeric, the day and time when each transaction was generated.
6. UnitPrice: Unit price. Numeric, Product price per unit in sterling.
7. CustomerID: Customer number. Nominal, a 5-digit integral number uniquely assigned to each customer.
8. Country: Country name. Nominal, the name of the country where each customer resides.


Checking first 5 and last 5 rows of dataset.

![Screenshot (77)](https://user-images.githubusercontent.com/67784512/212009851-f5ae031a-8577-4179-999c-59b6ac306f7d.png)

Checking duplicates in our dataset,
  We have 5268 duplicates values in our dataset we as to drop it before starting analysis.
  
Checking the missing values present in dataset,
 we have missing values in 'Description' and 'CustomerID'. And, count of missing values are 1454 and 135037, so we has to drop the rows where CustomerID column contain missing values.
 
 
# Feature engineering

AS we seen dataset contains one datetime column we take new columns from that like date, month, year, hour.

Creating one more feature called 'TotalAmount' by using 'Quantity' and 'UnitPrice'.

Above we created 'hour' column', for further analysis we divid time into 3 zone morning, afternoon and evening.

Checking cancellation using InvoiceNo. We have total 401604 InvoiceNo in that we have 8872 cancellations data, so we has to drop it.

Drop the rows which contain 'C' in our main dataset.


# EDA = Exploratory Data Analysis

Visualizing the variables using bar plot, on it we observed some below points.

1. WHITE HANGING HEART T-LIGHT HOLDER, REGENCY CAKESTAND 3 TIER, JUMBO BAG RED RETROSPOT are the most ordered products,
2. 2011 is our high selling year and 2010 is least,
3. Most Customers are from United Kingdom. Considerable number of customers are also from Germany, France, EIRE and Spain. Whereas Saudi Arabia, Bahrain, Czech Republic, Brazil and Lithuania has least number of customers.
4. Most of the customers have purchased the gifts in the month of November, October, December and September, Less number of customers have purchased the gifts in the month of April, January and February.
5. Thursday is high selling day according to data and There are no orders placed on Saturdays. Looks like it's a non working day for the retailer.
6. Most of the customers have purchased the items in Afternoon, moderate numbers of customers have purchased the items in Morning and the least in Evening.


Plot 'Quantity','UnitPrice' aand 'TotalAmount' variable using displot to understand it's distribution.

It shows a positively skewed distribution because most of the values are clustered around the left side of the distribution while the right tail of the distribution is longer, which means mean>median>mode.

For symmetric graph mean=median=mode.

So we use log transformation method to make symmetric graph.

we group by Country variable and rename variable 'InvoiceNo' to 'Invoice_count'.

And, we observed that United Kingdom is making most of the purchases as compared to other countries.

Visualizing top and bottom 10 countries based on average item purchase.

Visualizing top and bottom 10 countries based on total customers. 

Countrywise average item purchases - We group by 'Country' variable and taking mean from Quantity to find large quantity order over Country, 
Netherlands has ordered large quantity of orders.

Visualizing top and bottom 10 countries based on average item purchases.

quantity wise item purchases.

Visualizing top and bottom 10 products based on purchase quantity.

Amount wise item purchases.

Visualizing top and bottom 10 products based on amount.

customer wise item purchases.

Visualizing top and bottom 10 products based on customers.

Checking the number of cancellations by each customer. 

Visualizing top and bottom 10 customers based on cancellations.

Checking the number of cancellations countrywise.

Visualizing top and bottom 10 countries based on cancellations.

# RFM Modeling

1. Since most of the customers are wholesalers we cannot group customers based on the demographic group like age, gender, income and behavioral and psycho-graphic group Because Our Customers purchase bunch of goods from us and sell it to individual customers.
2. We only need to deal issues and make clusters related to B2B Business to Business instead of B2C i.e. Direct from Business to Customers WHY BECAUSE PEOPLE WHO PURCHASE PRODUCTS FROM US DO NOT UTILIZE IT They sell it to individual customers(B2C) or sell all products to another stores (B2B).
3. Due to all these reasons we need to cluster customers according to there activities i.e
  1. R-Recency
  2. F-Frequency
  3. M-Monetary
  
  
Adding 1 date to the last invoice date to set as latest date for reference.

Creating a new dataframe to calculate Recency, Frequency and Monetary scores for each customer.

Remaining the columns 'InvoiceDate' to 'Recency', 'InvoiceNo' to 'Frequency', 'TotalAmount' to 'Monetary'.
                    
Interpretation:
1. Recency: How recent a customer made a purchase.
2. Frequency: How often a customer makes a purchase.
3. Monetary: How much money a customer spends.                    

Calculating R, F and M scores by splitting Recency, Frequency	and Monetary based on quantiles.

1.  If the RFM of any customer is 444. His Recency is good, frequency is more and Monetary is more. So, he is the best customer.
2. If the RFM of any customer is 111. His Recency is low, frequency is low and Monetary is low. So, he is the churning customer.
3. If the RFM of any customer is 144. He purchased a long time ago but buys frequently and spends more. And so on.
4. Like this we can come up with number of segments for all combinations of R,F and M base on our usecase. Higher the RFM score, more valuable the customer is.

Handling the zeros in the dataframe to avoid error in transformations.

Applying log transformation on columns for smoothening the distribution.

Visualizing the correlation heatmap on RFM dataset.


![Screenshot (78)](https://user-images.githubusercontent.com/67784512/212060239-3ac6ca6f-f16b-4c20-bf0e-97c351d9f858.png)

Initializing an empty dictinory to store stats and summary of all the cluster.

Define a function to remove outliers.

Function for displaying the stats of Recency, Frequency and Monetary for each group.

Storing mean median and count of recency, Frequency and Monetary for each group.

Storing 0.25 and 0.75 quantile of Recency, Frequency and Monetary for each group.

Changing name for the columns.

Defining a function for plotting clusterfor visualization.

defining viualizing part

Part1 : Visyualizing the scatter plots for all clusters.

Part2 : Plotting the distribution.

Part3 : Displaying the stats and summary.

We started with Binning RFM Score, Quantile Based Clustering, K-Means Clustering for finding value k we use elbow method. And, next move to Hierarchical Clustering here we use dendogram to find value of k. And, we end with DBScan Clusters algorithm.

# Conclusion

1. We started with a simple binning and quantile based simple segmentation model first then moved to more complex models because simple implementation helps having a first glance at the data and know where/how to exploit it better.
2. Then we moved to k-means clustering and visualized the results with different number of clusters. As we know there is no assurance that k-means will lead to the global best solution. We moved forward and tried Hierarchical Clustering and DBSCAN clusterer as well.
3. We created several useful clusters of customers on the basis of different metrics and methods to cateorize the customers on the basis of their beavioural attributes to define their valuability, loyality, profitability etc for the business. Though significantly separated clusters are not visible in the plots, but the clusters obtained is fairly valid and useful as per the algorithms and the statistics extracted from the data.
4. Segments depends on how the business plans to use the results, and the level of granularity they want to see in the clusters. Keeping these points in view we clustered the major segments based on our understanding as per diffrent criteria as shown in the summary dataframe.

We also ploted helper function to understand easy way how each algorithms are working.


 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
