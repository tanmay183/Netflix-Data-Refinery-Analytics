
---

## **Netflix Data Engineering & Analytics**  
### **End-to-End ELT Project (Extract, Load, Transform & Analyze)**
![Architecture](https://github.com/user-attachments/assets/de0a9efb-1755-461a-bbe1-331c15b6fcbe)

---

### **📌 Overview**  
This project is a **complete ELT (Extract, Load, Transform) pipeline** designed for analyzing Netflix Movies and TV Shows using **SQL Server and Python**. The workflow involves:  

1. **Extracting data** from a CSV file.  
2. **Loading it into SQL Server** as raw data.  
3. **Transforming and cleaning the data** using SQL.  
4. **Performing analysis** to generate business insights.  

---

## **📂 Project Structure**
```
📁 Netflix-Data-Analysis
│-- 📄 netflix_data_extract.py         # Python script for extracting & loading data into SQL Server
│-- 📄 netflix_raw.sql                 # SQL script for raw data table creation
│-- 📄 netflix_data_analysis.sql       # SQL script for data cleaning & analysis
│-- 🖼 Architecture.png                # ELT project architecture diagram
│-- 📄 README.md                       # Project documentation
```

---

## **🚀 Workflow (ELT Architecture)**  

### **Step 1: Extract Data using Python**  
- The dataset **Netflix Movies and TV Shows** is downloaded as a CSV file.  
- Python (**Pandas, SQLAlchemy**) is used to read and **extract** the data.  

### **Step 2: Load Data into SQL Server (Raw Layer)**  
- Data is loaded into SQL Server in the **`netflix_raw`** table.  
- Ensured **data integrity** with constraints like primary keys.  

### **Step 3: Data Cleaning & Transformation**  
- **Handling missing values** (e.g., replacing NULL countries with `"Unknown"`).  
- **Removing duplicate records** based on `title` and `release_year`.  
- **Extracting useful insights**, such as content duration in minutes.  

### **Step 4: Data Analysis using SQL**  
- Performed **genre-based content analysis**.  
- Identified **top countries** producing Netflix content.  
- Extracted **recently added movies/shows**.  
- Answered **5 SQL-based business questions**.  

---

## **🛠️ Technologies Used**
| **Technology** | **Purpose** |
|--------------|-----------|
| **SQL Server (SSMS)** | Database for storing, cleaning, and analyzing Netflix data |
| **Python (Pandas, SQLAlchemy)** | Used for data extraction and loading into SQL |
| **SQL (T-SQL)** | For data cleaning, transformation, and analysis |
| **Jupyter Notebook (Optional)** | For testing Python scripts before execution |

---

## **📜 SQL Queries & Analysis**
### **1️⃣ Cleaning Raw Data**
```sql
UPDATE netflix_raw
SET country = 'Unknown'
WHERE country IS NULL;
```
- Replaces NULL values with `"Unknown"` in the `country` column.  

### **2️⃣ Removing Duplicates**
```sql
DELETE FROM netflix_raw
WHERE show_id NOT IN (
    SELECT MIN(show_id) FROM netflix_raw GROUP BY title, release_year
);
```
- Keeps only **one record per movie/show**.  

### **3️⃣ Identifying Popular Genres**
```sql
SELECT listed_in, COUNT(*) AS total_shows
FROM netflix_raw
GROUP BY listed_in
ORDER BY total_shows DESC;
```
- Determines **top-performing Netflix genres**.  

### **4️⃣ Finding Recently Added Shows**
```sql
SELECT title, date_added
FROM netflix_raw
ORDER BY date_added DESC
LIMIT 10;
```
- Lists the **latest 10 additions to Netflix**.  

### **5️⃣ Average Movie Duration**
```sql
SELECT type, AVG(CAST(SUBSTRING(duration, 1, CHARINDEX(' ', duration) - 1) AS INT)) AS avg_duration
FROM netflix_raw
WHERE type = 'Movie'
GROUP BY type;
```
- Extracts **average duration** of Netflix movies.  

---

## **📊 Business Insights Generated**
✅ **Top 5 genres on Netflix** based on number of titles.  
✅ **Country-wise distribution** of Netflix content.  
✅ **Most recent additions** to the Netflix library.  
✅ **Average duration of movies** available on Netflix.  

---

## **📌 How to Run the Project**
### **1️⃣ Prerequisites**
- Install **SQL Server** and **SSMS**.  
- Install Python and required libraries:  
  ```bash
  pip install pandas sqlalchemy pyodbc
  ```
- Clone the GitHub repository:  
  ```bash
  git clone https://github.com/yourusername/Netflix-Data-Analysis.git
  cd Netflix-Data-Analysis
  ```

### **2️⃣ Run Python Script to Extract & Load Data**
```bash
python netflix_data_extract.py
```
- This will **load the dataset into SQL Server**.  

### **3️⃣ Execute SQL Queries**
- Open `SSMS`, select the database, and **run the SQL scripts** in order:  
  1. `netflix_raw.sql` → Creates the database table.  
  2. `netflix_data_analysis.sql` → Cleans and analyzes the data.  

---

## **📌 Future Enhancements**
🔹 Automate the process using **Airflow** for scheduled ETL runs.  
🔹 Store **historical Netflix data** for trend analysis.  
🔹 Create an **interactive dashboard** using Power BI/Tableau.  

---
