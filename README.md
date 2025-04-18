# SimpleSales_tinysqLite
import sqlite3         # To work with SQLite database
 import pandas as pd    # For loading and manipulating SQL results
 import matplotlib.pyplot as plt  # For charts
 # Step 1: Connect to the SQLite database file (will be created if it doesn't exi
 conn = sqlite3.connect("sales_data.db")
 cursor = conn.cursor()
 # Step 2: Create a 'sales' table
 cursor.execute("""
 CREATE TABLE IF NOT EXISTS sales (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    product TEXT,
    quantity INTEGER,
    price REAL
 )
 """)
 conn.commit()
 # Step 3: Insert sample data into the sales table
 sales_data = [
    ('Pen', 10, 1.5),
    ('Notebook', 5, 3.0),
    ('Pencil', 20, 0.5),
    ('Eraser', 8, 0.75),
    ('Pen', 15, 1.5),
    ('Notebook', 7, 3.0)
 ]
 cursor.executemany("INSERT INTO sales (product, quantity, price) VALUES (?, ?, ?
 conn.commit()
 query = """
 SELECT 
    product, 
    SUM(quantity) AS total_qty, 
    SUM(quantity * price) AS revenue
 FROM sales
 GROUP BY product
 """
 df = pd.read_sql_query(query, conn)
 print("Sales Summary:")
 print(df)
 [sales_sql_Python_doc.pdf](https://github.com/user-attachments/files/19811870/sales_sql_Python_doc.pdf)

 Sales Summary:
    product  total_qty  revenue
 0    Eraser          8      6.0
 1  Notebook         12     36.0
 2       Pen         25     37.5
 3    Pencil         20     10.0
 df.plot(kind='bar', x='product', y='revenue', color='skyblue', legend=False)
 plt.title("Revenue by Product")
 plt.ylabel("Revenue ($)")
 plt.tight_layout()
 In [1]:
 In [3]:
 In [5]:
 In [8]:
 In [10]:
 In [12]:
 
 # Save the chart as an image (optional)
 plt.savefig("sales_chart.png")
 plt.show()
 
 conn.close()
 
