
# **DBMS Lab – Experiment 2**  
## **Implementation of SELECT Queries with Filtering, Grouping and Sorting in PostgreSQL**

---

## 👨‍🎓 **Student Details**  
**Name:** Drishti Bhatia  
**UID:** 25MCD10008      
**Branch:** MCA (Data Science)    
**Semester:** 2nd  
**Section/Group:** 1/A  
**Subject:** Technical Training-I Lab       
**Date of Performance:** 21/01/2026  

---

## 🎯 **Aim of the Practical**  
To implement and analyze SQL SELECT queries using filtering, sorting, grouping, and aggregation concepts in PostgreSQL for efficient data retrieval and analytical reporting.

---

## 💻 **Software Requirements**

- Oracle Database Express Edition  
- pgAdmin

---

## 📌 **Objective of the Practical**  
- To retrieve specific data using filtering conditions  
- To sort query results using single and multiple attributes  
- To perform aggregation using grouping techniques  
- To apply conditions on aggregated data using HAVING clause  
- To understand real-world analytical queries commonly asked in placement interviews  

---

## 🛠️ **Practical / Experiment Steps**  
Step 1: Database and Table Preparation
-	Start the PostgreSQL server.
-	Open the PostgreSQL client tool.
-	Create a database for the experiment.
- Prepare a sample table representing customer orders containing details such as customer name, product, quantity, price, and order date.
-	Insert sufficient sample records to allow meaningful analysis.
-	Purpose: To create a realistic dataset for performing analytical queries.
	 	
	
Step 2: Filtering Data Using Conditions
-	Execute data retrieval operations to display only those records that satisfy specific conditions, such as higher‑priced orders.
-	Observe how filtering limits the number of rows returned.
- Observation: Filtering reduces unnecessary data processing and improves query efficiency.	

Step 3: Sorting Query Results
- Retrieve selected columns from the table and arrange the output based on numerical values such as price.
- Perform sorting using both ascending and descending order.
- Apply sorting on more than one attribute to understand priority‑based ordering.
- Observation: Sorting is essential for reports, rankings, and ordered displays.

Step 4: Grouping Data for Aggregation
- Group records based on a common attribute such as product.
- Calculate aggregate values like total sales for each group.
- Analyze how multiple rows are combined into summarized results.
- Observation: Grouping transforms transactional data into analytical insights.

 
Step 5: Applying Conditions on Aggregated Data
- Apply conditions on grouped results to retrieve only those groups that satisfy specific aggregate criteria.
- Compare the difference between row‑level filtering and group‑level filtering.
- Observation: Conditions applied after grouping allow refined analytical reporting.

Step 6: Conceptual Understanding of Filtering vs Aggregation Conditions
- Analyze scenarios where conditions are incorrectly applied before grouping.
- Correctly apply conditions after grouping to avoid logical errors.
- Observation: Understanding execution order prevents common SQL mistakes frequently tested in interviews.


---

# ⚙️ **Procedure of the Practical**

## **Step 1: Table Creation**

```sql
CREATE TABLE customer_orders 
(
    order_id INT PRIMARY KEY,
    customer_name VARCHAR(50),
    product VARCHAR(50),
    quantity INT,
    price DECIMAL(10,2),
    order_date DATE
);

```

---

## **Step 2: Insert Records (DML)**

```sql
INSERT INTO customer_orders (order_id,customer_name, product, quantity, price, order_date) VALUES
(101,'Aman', 'Laptop', 1, 55000, '2024-01-10'),
(102,'Ridhi', 'Mobile', 2, 30000, '2024-01-12'),
(103,'Mohan', 'Laptop', 1, 60000, '2024-01-15'),
(104,'Sakshi', 'Tablet', 3, 15000, '2024-01-18'),
(105,'Gaurav', 'Mobile', 1, 25000, '2024-01-20'),
(106,'Pihu', 'Laptop', 2, 52000, '2024-01-22');

```

---

## **Step 3: Display All Records**

```sql
select * from customer_orders;
```
<img width="876" height="235" alt="1" src="https://github.com/user-attachments/assets/1f567698-d53a-4432-b73c-9ab6ae352c15" />

## **Step 4: Filtering Data Using WHERE Clause**

```sql
SELECT * 
FROM customer_orders
WHERE price > 30000;
```
<img width="872" height="140" alt="2" src="https://github.com/user-attachments/assets/8c661dcd-bac0-41a0-aad5-9103958bad1a" />```

```sql
SELECT customer_name, product, price
FROM customer_orders
WHERE product = 'Laptop' AND price > 55000

```
<img width="553" height="80" alt="3" src="https://github.com/user-attachments/assets/33c1ee43-e049-41f2-a061-3ad2476136fe" />

---


## **Step 5: Sorting Query Results**

### **Ascending Order**
```sql
SELECT customer_name, product, price
FROM customer_orders
ORDER BY price ASC
```
<img width="562" height="236" alt="4" src="https://github.com/user-attachments/assets/eb509330-98b1-45d5-b826-1f2b88774532" />


### **Descending Order**

```sql
SELECT customer_name, product, price
FROM customer_orders
ORDER BY price DESC
```
<img width="562" height="226" alt="5" src="https://github.com/user-attachments/assets/b3b519c4-ac67-4389-aa67-9b1160946497" />


### **Ascending and Descending Order**
```sql

SELECT customer_name, product, price
FROM customer_orders
ORDER BY product ASC, price DESC;
```
<img width="547" height="272" alt="6" src="https://github.com/user-attachments/assets/9c040763-2bd6-4b2a-9639-3d4075321a3b" />

## **Step 6: Grouping Data for Aggregation**

```sql

SELECT product, SUM(quantity * price) AS total_sales
FROM customer_orders
GROUP BY product;
```
<img width="347" height="142" alt="7" src="https://github.com/user-attachments/assets/e28d544b-c575-4aee-a774-5eda5a6eeab1" />

```sql
SELECT product, AVG(price) AS avg_price
FROM customer_orders
GROUP BY product;
```
<img width="450" height="146" alt="8" src="https://github.com/user-attachments/assets/92a6df55-aea4-45cc-97c9-39075381c22b" />

## **Step 7: Applying Conditions on Aggregated Data (HAVING)**

```sql
SELECT product, SUM(quantity * price) AS total_sales
FROM customer_orders
GROUP BY product
HAVING SUM(quantity * price) > 100000;

```
<img width="348" height="77" alt="9" src="https://github.com/user-attachments/assets/5e06534f-5e20-4608-9973-5c125d5faa6f" />


---

## **Step 8: Using WHERE and HAVING Together**

```sql
SELECT product, SUM(quantity * price) AS total_sales
FROM customer_orders
WHERE order_date >= '2024-01-15'
GROUP BY product
HAVING SUM(quantity * price) > 50000;
```
<img width="352" height="83" alt="10" src="https://github.com/user-attachments/assets/28dbafb8-16f7-4596-b0d0-40f3c6b0ccf2" />



## 📥📤 **I/O Analysis (Input / Output)**

### **Input**
- Customer order details  
- Filtering, sorting, grouping, and aggregation queries  

### **Output**
- Filtered customer records  
- Sorted result sets  
- Group-wise sales summary  
- Aggregated revenue reports  

📸 Screenshots of output are attached .

---

## 📘 **Learning Outcomes**  
- We understood how data can be filtered to retrieve only relevant records from a database.
-	We learned how sorting improves readability and usefulness of query results in reports.
-	We gained the ability to group data for analytical purposes.
-	We can clearly differentiate between row-level conditions and group-level conditions.
-	We developed confidence in writing analytical SQL queries used in real-world scenarios.
-	We are better prepared to answer SQL-based placement and interview questions related to filtering, grouping, and aggregation.

---

