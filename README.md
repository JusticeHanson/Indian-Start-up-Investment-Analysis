# Indian-Start-up-Investment-Analysis :chart_with_upwards_trend:
------------------------------------------------
### :link:Azubi Africa: Data Analytic Project (LP1)

# 1. Project Overview
In this project, I explore the dynamic landscape of start-up funding in India from 2018 to 2021. My goal is to uncover key patterns, trends, and insights that characterize the investment ecosystem during these years. The dataset for this analysis was gathered from three different sources:

*First Dataset:* The data for 2020 and 2021 were stored in Microsoft SQL Server.

*Second Dataset:* The data for 2019 were stored in a OneDrive.

*Third Dataset:* The data for 2018 were hosted in a GitHub repository.

# 2. Case Study
**Scenario:**

Your team is trying to venture into the Indian start-up ecosystem. As the data expert of the team you are to investigate the ecosystem and propose the best course of action.

## 2.1 Ask

In this phase, I define the business objectives, develop hypotheses, and raise questions to either support or reject these hypotheses. Additionally, I aim to gain general insights into the data.

## 2.2 Business Task

## Business Task

As the data expert for my team, my task is to analyze Indian start-up data to provide valuable insights and answers for me team seeking to venture into the Indian start-up ecosystem. My goal is to highlight key metrics and considerations that will inform and guide their decisions before entering this dynamic market.

# 3. Hypothesis

**Null Hypothesis (H0):**
There is no significant difference in the average funding amounts received across different sectors within the Indian startup ecosystem from 2018 to 2021.

**Alternative Hypothesis (H1):**
There is a significant difference in the average funding amounts received across different sectors within the Indian startup ecosystem from 2018 to 2021.

4. # Business Questions

(4.1)  Analyze the growth trajectory of startups over the past four years from 2018 to 2021. Investigate if there is an increase in the number of startups being funded and the average size companies of funded annually.

 (4.2)  Investigate the financial landscape for Indian startups over the four years. Has the average funding amount increased, indicating growing investor confidence, or has it plateaued or decreased overtime?
 
 (4.3) Identify the booming sectors withing the ecosystem and which top city serves as the industrial hub in India.
 
 (4.4) Determine the top investors within the startup ecosystem and identify the proportion of investment by the first 3 investors that have funded different sectors from 2018 - 2021 
 
 (4.5) Explore which stages of startups (e.g., Seed, Series A, Series B) are receiving the majority of investments. What are the predominant stages funded, and which cities are the identified stages of business situated. 

 # 5. Deliverables
- A hypothesis.

- Questions to help gain insights into the data.
A summary of the Analysis.

- Visualizations to communicate findings.

- Recommendations based on the analysis.

# 6. Data Preparation and Quality Check

In this phase I retrieved data from multiple sources for the analysis.

#  7. Infomation on Data
The data for the project was provided by Azubi Africa (Trainers).
The data contains 4 csv files: data_2018.csv, data_20192.csv, data_2020 (*from SQL server*) and data_2021 (*also from SQL server*)

### 7.1 The columns in the data are:

- Company Name: The name of the company.
- Founded: The year the company was founded.
- Sector: The sector the company operates in.
- Stage: The funding stage of the company.
- Location: The location of the company’s headquarters.
- Amount: The amount of funding the company received.
- Description: The ‘The About of company’.
- Investor: The investor who funded the company.
- Founder: The founders of the company.

### 7.2Limitations of Data

The 2018 start-up data lacks two columns (Founders, Founded) that are present in the 2019, 2020, and 2021 datasets. It is important to note that the source of the 2018 dataset is unknown, and therefore, this data cannot be considered reliable for making real-life recommendations for entrepreneurs.

# 8. Data Selection
All four dataset (2018 -2021 ) was retrived from ther respective source for the purpose of this analysis. 

# 9. Tools for Analysis
 I will utilize the following tools:

- **Python's:**

- Pandas: For data manipulation and cleaning.
- NumPy: For numerical operations.
- Matplotlib and Seaborn: For data visualization.
- SQL: For querying and managing the 2020 and 2021 data stored in Microsoft SQL Server.
- GitHub: To access the 2018 dataset and manage version control for any scripts or notebooks used in the analysis.
- Jupyter Notebook: For interactive data analysis and sharing insights through well-documented notebooks.

# 10. Process
In this face, I preview all the 4 dataset to understand the structure

### 10.1 Import relevant libraries
```python
import pyodbc
from dotenv import dotenv_values
import pandas as pd
import warnings
import numpy as np

warnings.filterwarnings('ignore')
```
### 10.2 Establish a connection to server
![Image of connection to server](/Screenshots/Server%20Connection.png)

![Select tables of interest](/Screenshots/SQL%20Query.png)

![Output](/Screenshots/Tables%20output.png)

### 10.3 Preview Data_2020
```python
query= "SELECT * FROM dbo.LP1_startup_funding2020"
data_2020 =pd.read_sql(query, connection)

data_2020.head()
```
![output data_2020](/Screenshots/2020.png)

#### 10.4 data_2021
```python
query= "SELECT * FROM dbo.LP1_startup_funding2021"
data_2021 =pd.read_sql(query, connection)

data_2021.head()
```

![output data_2021](/Screenshots/2021.png)

data_2019
```python
data_2019=pd.read_csv("D:\\JHanson\\Justice Hanson\\DS Career Accelerator\Project 1\\Indian-Start-up-Investment-Analysis\\CSV Data\\startup_funding2019.csv")

data_2019.head(5)
```
![output data_2019](/Screenshots/2019.png)

data_2018
![output data_2018](/Screenshots/2018.png)

# 11. For consistency, rename all columns befor merged 

```python
data_2018.rename(columns={
    'Company Name': 'company_name',
    'Industry': 'sector',
    'Round/Series': 'stage',
    'Amount': 'funding_amount',
    'Location': 'location',
    'About Company': 'description'
}, inplace=True)

# 2019 column mapping
data_2019.rename(columns={
    'Company/Brand': 'company_name',
    'HeadQuarter': 'location',
    'Sector': 'sector',
    'What it does': 'description',
    'Amount($)': 'funding_amount'
}, inplace=True)

# 2020 column mapping
data_2020.rename(columns={
    'Company_Brand': 'company_name',
    'What_it_does': 'description',
    'Amount': 'funding_amount'
}, inplace=True)

# 2021 column mapping
data_2021.rename(columns={
    'Company_Brand': 'company_name',
    'What_it_does': 'description',
    'Amount': 'funding_amount'
}, inplace=True)

# Merge datasets using the standardized column names
merged_data = pd.concat([data_2018, data_2019, data_2020, data_2021], ignore_index=True)

merged_data.head(5)
```
This helped me to have consistent column names for the merged dataset

#### 11.1 created new column 'Year'
purposely to identify each of the 4 datasets withing the merged_data

#### 11.2 check data info to understand data structure
![info on merged_data](/Screenshots/merged.info.png)

