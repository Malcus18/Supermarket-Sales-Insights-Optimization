# Supermarket-Sales-Insights-Optimization
## Project Overview
In this project, we analyze supermarket sales data to derive actionable insights and develop a strategic plan for optimizing sales. The dataset includes sales transactions from multiple departments, cities, and payment methods. We perform data cleaning, exploratory data analysis (EDA), and generate visualizations to understand sales trends across different dimensions all done using Python scripting.

## Key highlights of the analysis include:

Total and Average Sales by Department: Identifying top-performing departments and evaluating their average sales performance.
Seasonal Trends: Analyzing sales data across different months to determine peak sales periods.
Sales by City and Payment Method: Understanding the relationship between sales performance, city locations, and preferred payment methods.
Customer Types: Examining sales by customer type to tailor marketing efforts.
Based on these insights, a detailed sales strategy is developed for the highest-performing department, including promotional campaigns, marketing strategies, and expected outcomes.

### Data Source
Subscription data: The primary dataset used for this analysis is the "Suppermarket_data.cvs" file, containing deatailed information about country's subscription to the training.
### Tools Used
-Python for cleaning, analysis, creating insights and visualization. [Downlaod_here]([https://anacondanavigator.com](http://localhost:8888/notebooks/Py%20project.ipynb)

### Data Cleaning/ Preparation

In the initial data preparation phase, the following tasks were prformed:
1. The data was loaded and inspected.
2. Data Cleaning and formatting

### Exploratory Data Analysis
EDA Involved the training data to answer key questions, such as:

1. Which city has the highest sales by payment method?

2. What are the total monthly sales?

3. What are the sales destribution by product line?
   
4. What is the count of the customer destribution type by membership and normal purchases?
   
5. What is the average product rating by product line?
   
6. What are the total sales by gender and product line?

 ### Data analysis
 ``` Python(Jupiter Notebook)
!pip install pyforest
import pyforest
df= pd.read_excel(r"C:\users\HUSSEIN ODONGO\DESKTOP\Suppermarket.xlsx")
df
df.info
df['Tax 5%'] = df['Tax 5%'].astype(int)
print("\nDataFrame with Decimal Points Removed (Integer Conversion):")
print(df)
df
df['Rating'] = df['Rating'].astype(int)
print("\nDataFrame with Decimal Points Removed (Integer Conversion):")
print(df)
df['gross income'] = df['gross income'].astype(int)
print("\nDataFrame with Decimal Points Removed (Integer Conversion):")
print(df)
df
df['cogs'] = df['cogs'].astype(int)
print("\nDataFrame with Decimal Points Removed (Integer Conversion):")
print(df)
df
df['Total'] = df['Total'].astype(int)
print("\nDataFrame with Decimal Points Removed (Integer Conversion):")
print(df)
df
df['Unit price'] = df['Unit price'].astype(int)
print("\nDataFrame with Decimal Points Removed (Integer Conversion):")
print(df)
df
df['gross margin percentage'] = df['gross margin percentage'].astype(int)
print("\nDataFrame with Decimal Points Removed (Integer Conversion):")
print(df)
df
df = df.drop('gross margin percentage', axis=1)
print(df)
df
df['Total Sales'] = df['Unit price'] * df['Quantity']
print("\nDataFrame with Total Sales Column:")
print(df)
df
total_sales_per_department = df.groupby('Product line')['Total Sales'].sum()
print("\nTotal Sales per Department:")
print(total_sales_per_department)
df
total_sales_by_city_payment = df.groupby(['City', 'Payment'])['Total Sales'].sum().reset_index()
print("\nTotal Sales by City and Payment:")
print(total_sales_by_city_payment)
df
df['Total Sales by City and Payment'] = df.groupby(['City', 'Payment'])['Total Sales'].transform('sum')
print("\nDataFrame with Total Sales by City and Payment Column:")
print(df)
df
# Convert Date column to datetime format
df['Date'] = pd.to_datetime(df['Date'])

# Extract month and create a new column
df['Month'] = df['Date'].dt.month
print(df)
df

# Which city has the highest sales by payment method?
plt.figure(figsize=(10, 6))
sns.barplot(data=total_sales_by_city_payment, x='City', y='Total Sales', hue='Payment')
plt.title('Total Sales by City and Payment Method')
plt.xlabel('City')
plt.ylabel('Total Sales')
plt.show()

# What are the total monthly sales
# Group data by Month
monthly_sales = df.groupby('Month')['Total Sales'].sum().reset_index()
# Plotting
plt.figure(figsize=(10, 6))
sns.lineplot(data=monthly_sales, x='Month', y='Total Sales', marker='o')
plt.title('Monthly Sales Trend')
plt.xlabel('Month')
plt.ylabel('Total Sales')
plt.xticks(range(1, 13))  # Assuming months are represented as 1-12
plt.show()

# What are the sales destribution by product line?
# Plotting
plt.figure(figsize=(10, 6))
sns.barplot(data=df, x='Product line', y='Total Sales')
plt.title('Sales Distribution by Product Line')
plt.xlabel('Product Line')
plt.ylabel('Total Sales')
plt.xticks(rotation=45)
plt.show()

#  What is the count of the customer destribution type by membership and normal purchases?
plt.figure(figsize=(10, 6))
sns.countplot(data=df, x='Customer type')
plt.title('Customer Type Distribution')
plt.xlabel('Customer Type')
plt.ylabel('Count')
plt.show()

# What is the average product rating by product line?
avg_rating_by_product_line = df.groupby('Product line')['Rating'].mean().reset_index()
# Plotting
plt.figure(figsize=(10, 6))
sns.barplot(data=avg_rating_by_product_line, x='Product line', y='Rating')
plt.title('Average Rating by Product Line')
plt.xlabel('Product Line')
plt.ylabel('Average Rating')
plt.xticks(rotation=45)
plt.show()

# What are the total sales by gender and product line?
# Calculate total sales by gender and product line
total_sales_by_gender_product_line = df.groupby(['Gender', 'Product line'])['Total Sales'].sum().reset_index()

# Plot total sales by gender and product line
plt.figure(figsize=(12, 8))
sns.barplot(data=total_sales_by_gender_product_line, x='Product line', y='Total Sales', hue='Gender')
plt.title('Total Sales by Gender and Product Line')
plt.xlabel('Product Line')
plt.ylabel('Total Sales')
plt.xticks(rotation=45)
plt.show()

# Select a few relevant columns for the pair plot
pair_plot_columns = ['Unit price', 'Quantity', 'Tax 5%', 'Total', 'cogs', 'gross income', 'Rating', 'Total Sales']

# Plotting
sns.pairplot(df[pair_plot_columns])
plt.show()
```

![Untitled](https://github.com/user-attachments/assets/9a365766-deac-4393-8e19-c730a2a9e9a1)

![Untitled](https://github.com/user-attachments/assets/f789cb65-cbb8-4474-9909-21b273f46f14)

![Untitled](https://github.com/user-attachments/assets/e77f87ed-0c2b-455d-aef6-99f3f4fec27a)

![Untitled](https://github.com/user-attachments/assets/d11d39db-fe8a-47a5-b4f9-076253bd2376)

![Untitled](https://github.com/user-attachments/assets/fcd7229f-6c96-485e-90de-11ce0ae43870)

![Untitled](https://github.com/user-attachments/assets/82ee29d1-6712-4647-9194-e45ed9a36c5a)

![Untitled](https://github.com/user-attachments/assets/73fa2853-0a05-4ad2-a4e9-d231ec34248e)


### RESULTS AND FINDING
The analysis results are sumarised as follows:

1. It was foun out that Naypitaw has the highest sales with Cash payment method and lowest lowest payment by credit card. This means a few people like using credit cards in Napitaw city. However, Madalay the city with lowest sales, has the highest sales of credit payment method against other methods. This means people in Madalay prefer to use credit cards.

















