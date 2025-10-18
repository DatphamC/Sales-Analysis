# 🛍️ Sales Data Analysis

This project analyzes the Sales Data.
It aims to clean, process, and visualize retail transaction data to uncover business insights about sales performance.

---

## 📁 Project Overview

The dataset contains monthly sales records of various electronic products sold in 2019.  
This notebook combines all monthly CSV files, cleans the data, and answers key business questions through data analysis and visualization.

---

## ⚙️ Tools & Libraries

- **Python 3**
- **Pandas** — data manipulation and cleaning  
- **Matplotlib** — visualization  
- **NumPy** — numerical operations  
- **Glob / re** — file management and regex processing  
- **Jupyter Notebook** — exploration and presentation  

---

## 🧩 Steps and Tasks

### **Task 1 – Import and Merge Data**
- Import all monthly CSV files (`sales2019_1.csv` to `sales2019_12.csv`)  
- Sort by month number using regex extraction  
- Concatenate all data into a single dataset: `sales2019_all.csv`

### **Task 2 – Clean and Preprocess Data**
- Remove missing values and erroneous headers  
- Convert numerical columns (`Quantity Ordered`, `Price Each`) to proper data types  
- Add derived columns such as:
  - `Month` — extracted from the `Order Date`
  - `Sales` = `Quantity Ordered * Price Each`
  - `City` — extracted from the `Purchase Address`

### **Task 3 – Exploratory Data Analysis**
Answer the following business questions:

1. **What was the best month for sales?**
   - Identify total revenue per month  
   - Visualize monthly sales using bar charts

2. **Which city had the highest sales?**
   - Group by `City` and sum sales  
   - Visualize results by city

3. **What time should advertisements be displayed to maximize sales?**
   - Extract hour from `Order Date`
   - Plot sales distribution by hour

4. **What products are most often sold together?**
   - Find orders with the same `Order ID`
   - Use combinations of products to determine common bundles

5. **Which product sold the most, and why?**
   - Analyze total quantity ordered per product
   - Compare with average price per product

---

## 📊 Example Visualizations
- Monthly revenue bar chart  
- City-wise sales comparison  
- Sales vs. time of day histogram  
- Product bundles frequency chart  
- Product vs. price scatter plot

---

## 🚀 How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/Sales_Data_2019.git
   cd Sales_Data_2019
   ```

2. Install dependencies:
   ```bash
   pip install pandas matplotlib numpy
   ```

3. Open Jupyter Notebook:
   ```bash
   jupyter notebook
   ```

4. Run the notebook `report.ipynb` step by step to reproduce the analysis.

---

## 📈 Key Insights
- December was the **best month for sales**, largely driven by holiday shopping.
- The **city of San Francisco** generated the highest revenue.
- Most orders occurred between **11 AM and 7 PM**, ideal for ad placement.
- Common product bundles included **iPhone + Lightning Cable** and **Laptop + USB-C Adapter**.
- Products with **lower price points** had significantly higher sales volumes.

---

## 🧠 Author
**Dat Pham**  
Data Analyst | Python, SQL, Excel  
[GitHub Profile](https://github.com/DatphamC)


