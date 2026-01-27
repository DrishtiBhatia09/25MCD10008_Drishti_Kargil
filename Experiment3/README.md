

# **DBMS Lab – Experiment 3**  
## **Implementation of Conditional Logic using IF–ELSE and CASE Statements in PostgreSQL**

---

## 👨‍🎓 **Student Details**  
**Name:** Drishti Bhatia  
**UID:** 25MCD10008      
**Branch:** MCA (Data Science)    
**Semester:** 2nd  
**Section/Group:** 1/A  
**Subject:** Technical Training-I Lab       
**Date of Performance:** 27/01/2026  

---

## 🎯 **Aim of the Practical**  
To implement conditional decision-making logic in PostgreSQL using IF–ELSE constructs and CASE expressions for classification, validation, and rule-based data processing


---

## 💻 **Tools Used**
PostgreSQL

## 📌 **Objective of the Practical**  
-	To understand conditional execution in SQL
-	To implement decision-making logic using CASE expressions
-	To simulate real-world rule validation scenarios
-	To classify data based on multiple conditions
-	To strengthen SQL logic skills required in interviews and backend systems
  
## 🛠️ **Theory** 
In real-world database systems, data often needs to be validated, categorized, or transformed based on business rules. Conditional logic allows the database to make decisions dynamically instead of relying solely on application-layer logic.

PostgreSQL supports conditional logic mainly through:
-	CASE Expressions (used inside SELECT, UPDATE, INSERT)
-	IF–ELSE constructs (used inside PL/pgSQL blocks such as functions and procedures)
	
CASE Expression
-	Evaluates conditions sequentially
-	Returns a value based on the first true condition
-	Can be used in SELECT, UPDATE, ORDER BY, and WHERE clauses

Types of CASE
-	Simple CASE → compares expressions
-	Searched CASE → evaluates boolean conditions

Conditional logic is heavily used in:
-	Data classification (grades, salary slabs)
- Violation detection
-	Status mapping
-	Business rule enforcement

Companies like Amazon, SAP, Oracle, and Adobe frequently test CASE-based logic in SQL interviews.

## 🛠️ **Practical / Experiment Steps**  
Prerequisite Understanding      
Students should first create a table that stores:
-	A unique identifier
-	A schema or entity name
-	A numeric count representing violations or issues
Populate the table with multiple records having different violation counts.

Step 1: Classifying Data Using CASE Expression
Task for Students:
-	Retrieve schema names and their violation counts.
-	Use conditional logic to classify each schema into categories such as:
o	No Violation
o	Minor Violation
o	Moderate Violation
o	Critical Violation

Learning Focus:
-	Using searched CASE
-	Sequential condition checking
-	Real-world compliance reporting logic

Step 2: Applying CASE Logic in Data Updates
Task for Students:
-	Add a new column to store approval status.
-	Update this column based on violation count using conditional rules such as:
o	Approved
o	Needs Review
o	Rejected
Learning Focus:
-	Automating decisions inside the database
-	Reducing application-side logic
-	Using CASE inside UPDATE statements


Step 3: Implementing IF–ELSE Logic Using PL/pgSQL

Task for Students:
-	Use a procedural block instead of a SELECT statement.
-	Declare a variable representing violation count.
-	Display different messages based on the value of the variable using IF–ELSE logic.

Learning Focus:
-	Understanding procedural SQL
-	ELSE-IF ladder execution
-	Backend validation logic in stored procedures

Step 4: Real-World Classification Scenario (Grading System)
Task for Students:
-	Create a table to store student names and marks.
-	Classify students into grades based on their marks using conditional logic.

Learning Focus:
-	Common interview use case
-	Data categorization
-	Rule-based evaluation

Step 5: Using CASE for Custom Sorting
Task for Students:
-	Retrieve schema details.
-	Apply conditional priority while sorting records based on violation severity.

Learning Focus:
-	Advanced CASE usage
-	Custom ordering logic
-	Dashboard and reporting scenarios


# ⚙️ **Code**


```sql
CREATE TABLE schema_violations (
    id SERIAL PRIMARY KEY,
    schema_name VARCHAR(50),
    violation_count INT
);
```
---

```sql
INSERT INTO schema_violations (schema_name, violation_count) VALUES
('sales', 0),
('finance', 2),
('hr', 5),
('inventory', 9),
('audit', 15);

```
---
## **Step 1**
```sql
SELECT schema_name,violation_count,
    CASE
        WHEN violation_count = 0 THEN 'No Violation'
        WHEN violation_count BETWEEN 1 AND 3 THEN 'Minor Violation'
        WHEN violation_count BETWEEN 4 AND 7 THEN 'Moderate Violation'
        ELSE 'Critical Violation'
    END AS violation_status
FROM schema_violations;
```
<img width="552" height="200" alt="1" src="https://github.com/user-attachments/assets/bffb9e69-7ef2-4d12-901c-89715ee933aa" />

## **Step 2**

```sql
ALTER TABLE schema_violations
ADD COLUMN approval_status VARCHAR(20);

UPDATE schema_violations
SET approval_status =
    CASE
        WHEN violation_count = 0 THEN 'Approved'
        WHEN violation_count BETWEEN 1 AND 5 THEN 'Needs Review'
        ELSE 'Rejected'
    END;

Select * from schema_violations;
```

<img width="667" height="202" alt="2" src="https://github.com/user-attachments/assets/3ac9d113-f19b-4e3b-a499-e228090b1246" />

## **Step 3:**

```sql
DO $$
DECLARE
    v_count INT := 6;
BEGIN
    IF v_count = 0 THEN
        RAISE NOTICE 'No violations found.';
    ELSIF v_count BETWEEN 1 AND 5 THEN
        RAISE NOTICE 'Minor issues detected. Review required.';
    ELSE
        RAISE NOTICE 'Critical violations! Immediate action needed.';
    END IF;
END $$;
```
<img width="546" height="145" alt="3" src="https://github.com/user-attachments/assets/f5147a69-a84a-4d5e-a739-797b9ec7028c" />



## **Step 4:**
```sql
CREATE TABLE student (
    student_name VARCHAR(50),
    marks INT
);

INSERT INTO student VALUES
('Amit', 92),
('Riya', 78),
('Neha', 65),
('Rahul', 48),
('Karan', 33);

SELECT student_name,marks,
    CASE
        WHEN marks >= 90 THEN 'A'
        WHEN marks >= 75 THEN 'B'
        WHEN marks >= 60 THEN 'C'
        WHEN marks >= 40 THEN 'D'
        ELSE 'Fail'
    END AS grade
FROM student;
```
<img width="391" height="197" alt="4" src="https://github.com/user-attachments/assets/1d81b887-062c-482c-ae4f-ea92f90c0e5b" />

## **Step 5:**

```sql
SELECT
    schema_name,
    violation_count
FROM schema_violations
ORDER BY
    CASE
        WHEN violation_count = 0 THEN 1
        WHEN violation_count BETWEEN 1 AND 3 THEN 2
        WHEN violation_count BETWEEN 4 AND 7 THEN 3
        ELSE 4
    END,
    violation_count DESC ;
```

<img width="376" height="200" alt="5" src="https://github.com/user-attachments/assets/4af9652f-aa7c-4b4f-b451-5940d7a60ef2" />

## 📘 **Learning Outcomes**  
This experiment demonstrates how conditional logic is implemented in PostgreSQL using CASE expressions and IF–ELSE constructs.
 Students gain strong command over rule-based SQL logic, which is essential for:
-	Backend systems
-	Analytics
-	Compliance reporting
-	Placement and technical interviews

