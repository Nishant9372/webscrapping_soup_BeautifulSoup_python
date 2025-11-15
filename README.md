# 🕸️ Web Scraping Project — Extracting Data from Wikipedia using Python

## 📘 Project Overview  
This project demonstrates how to **scrape tabular data from a real-world website** (Wikipedia) using **Python**, **BeautifulSoup**, and **pandas**.  
The dataset extracted contains the **largest companies in the United States by revenue**, sourced from Wikipedia.  

The project aims to showcase **data extraction, cleaning, and structuring** — essential skills for a **Data Analyst**.

---

## 🎯 Objectives  
- Scrape data from a live website (Wikipedia).  
- Parse and extract table data using **BeautifulSoup**.  
- Clean and organize the scraped data using **pandas**.  
- Prepare the data for further analysis or visualization.

---

## 🧰 Technologies Used  

| Library | Purpose |
|----------|----------|
| `requests` | Send HTTP requests to fetch web page data |
| `BeautifulSoup` (`bs4`) | Parse and extract HTML content |
| `pandas` | Create structured DataFrames for analysis |

---

## 🧑‍💻 Code Walkthrough  

### 1. Import Required Libraries
```python
from bs4 import BeautifulSoup
import requests
import pandas as pd


2️⃣ Fetch the Web Page

url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'
page = requests.get(url)
soup = BeautifulSoup(page.text, 'html')
print(soup)  # (Optional) To view the page structure

3️⃣ Extract Table Headers

table = soup.find_all('table')[0]  # Locate the first table on the page
world_titles = table.find_all('th')
world_table_titles = [title.text.strip() for title in world_titles]
print(world_table_titles)


4️⃣ Create a DataFrame

df = pd.DataFrame(columns=world_table_titles)

5️⃣ Extract and Append Table Rows

column_data = table.find_all('tr')

for row in column_data[1:]:
    row_data = row.find_all('td')
    individual_row_data = [data.text.strip() for data in row_data]
    print(individual_row_data)


🧹 Data Cleaning (Optional)

df.dropna(inplace=True)
df.reset_index(drop=True, inplace=True)

💾 Save Data to CSV
df.to_csv('US_Largest_Companies.csv', index=False)
print("Data saved successfully!")

📈 Key Takeaways

* Learned how to extract structured data from real websites.

* Practiced HTML parsing and DataFrame creation.

* Built a clean dataset ready for data analysis.

* Strengthened core data analyst skills: data collection, cleaning, and transformation.


### Exploratory Data Analysis (EDA)

This section explores the financial and structural characteristics of Indian companies listed in the Forbes Global 2000.

#### Data Cleaning
- Removed duplicate rows based on `Rank` and `Name`
- Converted financial columns (`Revenue`, `Profit`, `Assets`, `Value`) to numeric types
- Handled missing and inconsistent values

#### Summary Statistics
- Calculated mean, median, standard deviation for key financial metrics
- Identified outliers and skewed distributions, especially in `Profit` and `Value`

#### Key Visualizations
- Distribution plots for Revenue, Profit, Assets, and Market Value
- Top 10 companies by Market Value — led by Reliance Industries, TCS, and HDFC Bank
- Industry-wise average Profit and Revenue — Banking and Infotech sectors show strong performance
- Correlation heatmap — moderate positive correlation between Revenue and Market Value

