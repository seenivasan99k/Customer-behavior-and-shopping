🛍️ Customer Behavior & Shopping Analysis

📌 Project Overview:

This project analyzes customer shopping behavior using Python (Jupyter Notebook), SQL (PostgreSQL), and Power BI.

The workflow includes:

Data cleaning and preprocessing in Python

Feature engineering and transformation

Loading cleaned data into PostgreSQL

Performing SQL-based analysis

Preparing dataset for dashboard visualization

This project demonstrates an end-to-end data analytics pipeline from raw CSV to structured database.

🎯 Project Objectives:

Clean and preprocess raw customer shopping data

Handle missing values intelligently

Create age segmentation for customer analysis

Convert purchase frequency into numerical format

Identify redundant columns

Load cleaned dataset into PostgreSQL

Enable SQL-based business insights

🛠️ Tools & Technologies:

Python (Pandas, NumPy)

Jupyter Notebook

PostgreSQL

SQLAlchemy & Psycopg2

Power BI (for visualization – optional dashboard layer)

📂 Dataset Information:

File: customer_shopping_behavior.csv
Total Records: 3,900
Columns: 18 (after cleaning: 19 engineered features before dropping redundant column)

Key Features:

Customer Id

Age

Gender

Item Purchased

Category

Purchase Amount (USD)

Location

Season

Review Rating

Subscription Status

Discount Applied

Previous Purchases

Payment Method

Frequency Of Purchases

🧹 Data Cleaning & Preprocessing (Python):
✅ 1. Handling Missing Values:

37 missing values in Review Rating

Filled using median rating grouped by Category

df['Review Rating'] = df.groupby('Category')['Review Rating'].transform(lambda x: x.fillna(x.median()))
✅ 2. Standardizing Column Names:

Converted to lowercase

Removed special characters

Standardized format using .str.title()

✅ 3. Feature Engineering:
🔹 Age Group Creation

Used quartile segmentation:

labels = ['Young Adult', 'Adult', 'Middle-aged', 'Senior']
df['age_group'] = pd.qcut(df['Age'], q=4, labels=labels)
🔹 Purchase Frequency Conversion

Converted categorical frequency into number of days:

Frequency	Days
Weekly	7
Fortnightly	14
Monthly	30
Quarterly	90
Annually	365
df['Purchase_Frequency_Days'] = df['Frequency Of Purchases'].map(frequency_mapping)
✅ 4. Redundant Column Removal

Since:

(df['Discount Applied'] == df['Promo Code Used']).all()

Returned True,
Promo Code Used was dropped because it duplicated Discount Applied.

🗄️ Database Integration (PostgreSQL):

Used SQLAlchemy to connect and load data:

engine = create_engine(f"postgresql+psycopg2://{username}:{password}@{host}:{port}/{database}")
df.to_sql("customer", engine, if_exists="replace", index=False)

📌 Database: customer_behavior
📌 Table: customer

Data successfully loaded into PostgreSQL.

🔍 SQL Analysis Possibilities:

Once loaded into SQL, analysis can include:

Revenue by Age Group

Subscription vs Non-subscription comparison

Repeat customer analysis

Category-wise sales

Average purchase amount by gender

Seasonal revenue trends

📊 Business Insights:

Median-based imputation improved rating reliability

Age segmentation enables customer targeting

Numeric purchase frequency allows behavioral modeling

Removing redundant columns improves database efficiency

Clean structured data enables advanced SQL analysis

📁 Project Structure:
customer-behavior-analysis/
│
├── data/
│   └── customer_shopping_behavior.csv
│
├── notebook/
│   └── data_cleaning_and_analysis.ipynb
│
├── sql/
│   └── analysis_queries.sql
│
├── dashboard/
│   └── powerbi_dashboard.pbix
│
└── README.md

👤 Author:

Seenivasan
Aspiring Data Analyst
Skilled in: Python | SQL | PostgreSQL | Power BI | Excel

📎 Conclusion:

This project demonstrates a complete real-world data analytics workflow:

Raw Data ➝ Data Cleaning (Python) ➝ Feature Engineering ➝ Database Integration ➝ SQL Analysis ➝ Business Insights

It highlights strong data preprocessing skills, database handling, and analytical thinking required for data analyst roles.
