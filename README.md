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
  1 R-Recency
  2 F-Frequency
  3 M-Monetary





 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
