# 🧮 Task 7 – Data Analysis using Python, SQL, Pandas & Matplotlib

## 📘 Objective
The goal of this project is to perform data analysis using **SQL queries inside Python** and visualize the results.  
We analyze a small sales dataset to calculate total quantity and revenue for each product and visualize it using Matplotlib.

---

## 🧰 Tools & Technologies Used
- **Python 3**
- **SQLite3** → for creating and managing database tables
- **Pandas** → for data analysis and manipulation
- **Matplotlib** → for visualizing summarized data
- **Jupyter Notebook** → for step-by-step coding and documentation

---

## 📂 Project Structure

| File Name | Description |
|------------|-------------|
| `Task7_DataAnalysis.ipynb` | Main notebook containing code, analysis, and SQL integration |
| `sales_data.db` | SQLite database file containing sample sales records |
| `sales_summary.csv` | Output CSV file showing total quantity and revenue per product |
| `sales_chart.png` | Bar chart visualization of total revenue by product |
| `README.md` | Project documentation (this file) |

---

## ⚙️ Step-by-Step Process

### **1️⃣ Create Database and Table**
- Connected Python to SQLite using `sqlite3`.
- Created a table named **sales**.
- Inserted multiple product sales records.

```python
import sqlite3

# Create database connection
conn = sqlite3.connect('sales_data.db')
cursor = conn.cursor()

# Create sales table
cursor.execute('''
CREATE TABLE IF NOT EXISTS sales (
    id INTEGER PRIMARY KEY,
    sale_date TEXT,
    product TEXT,
    quantity INTEGER,
    price REAL
);
''')

# Insert sample records
records = [
    ('2025-10-01', 'Pen', 20, 0.5),
    ('2025-10-02', 'Pen', 30, 0.5),
    ('2025-10-01', 'Notebook', 10, 2.5),
    ('2025-10-03', 'Notebook', 5, 2.5),
    ('2025-10-04', 'Stapler', 5, 5.0)
]

cursor.executemany('INSERT INTO sales (sale_date, product, quantity, price) VALUES (?, ?, ?, ?)', records)
conn.commit()
conn.close()

2️⃣ Run SQL Queries in Python

Queried total quantity and revenue per product.

Fetched the results using pandas.read_sql_query().

import pandas as pd
import sqlite3

# Connect and execute query
conn = sqlite3.connect('sales_data.db')
query = '''
SELECT 
    product,
    SUM(quantity) AS total_quantity,
    SUM(quantity * price) AS total_revenue
FROM sales
GROUP BY product;
'''
df = pd.read_sql_query(query, conn)
conn.close()

# Display result
print("✅ Sales Summary:")
display(df)

3️⃣ Export Results to CSV
df.to_csv('sales_summary.csv', index=False)
print("✅ Exported to sales_summary.csv")

4️⃣ Visualize Data using Matplotlib
import matplotlib.pyplot as plt

plt.figure(figsize=(6,4))
plt.bar(df["product"], df["total_revenue"], color="orange", edgecolor="black")
plt.xlabel("Product")
plt.ylabel("Total Revenue (₹)")
plt.title("Revenue by Product")
plt.tight_layout()
plt.savefig("sales_chart.png", dpi=150)
plt.show()

print("✅ Chart saved as sales_chart.png")

5️⃣ Verify and Display Saved Files
import os
print("📂 Files in your project folder:")
for file in os.listdir():
    print("-", file)

print("\n📁 Your files are saved in:", os.getcwd())


✅ Output:

Files saved successfully:
- sales_data.db (Database)
- sales_summary.csv (Table Output)
- sales_chart.png (Graph Image)

🧾 Sample Output
📊 Sales Summary (from SQL Query)
product	total_quantity	total_revenue
Pen	50	25.0
Notebook	15	37.5
Stapler	5	25.0
🖼 Visualization

Bar Chart – Revenue by Product

📁 Saved as sales_chart.png
Shows total revenue per product (Pen, Notebook, Stapler).

💡 Key Learnings

How to connect Python with SQLite database

How to run SQL queries from Python

How to fetch SQL results into Pandas

How to visualize results using Matplotlib

How to export results to CSV and image formats

🚀 How to Run This Project
🧭 Run Locally (Jupyter Notebook)

Clone the repository:

git clone https://github.com/YourUserName/Task7_DataAnalysis.git
cd Task7_DataAnalysis


Open the Jupyter Notebook:

jupyter notebook Task7_DataAnalysis.ipynb


Run each cell sequentially (Shift + Enter).

🧑‍💻 Author

Karnakanti Varsha
🎓 Data Analyst intern

📧 Email: karnakantivarsha@gmail.com

🏁 Conclusion

This project demonstrates the integration of SQL and Python for end-to-end data analysis.
From data creation to visualization, the workflow shows how to automate reporting and extract insights using open-source tools like SQLite, Pandas, and Matplotlib.
