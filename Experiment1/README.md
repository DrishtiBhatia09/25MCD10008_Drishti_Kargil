


# **DBMS Lab – Experiment 1**  
## **Design and Implementation of Sample Database System using DDL, DML and DCL**-

## 👨‍🎓 **Student Details**  
**Name:** Drishti Bhatia    
**UID:** 25MCD10008     
**Branch:** MCA(Data Science)     
**Semester:** 2nd  
**Section/Group:** 1/A  
**Subject:** Technical Training-I Lab  
**Date of Performance:** 13/01/2026  

---

## 🎯 **Aim of the Practical**  
To design and implement a sample database system using DDL, DML, and DCL commands, including database creation, data manipulation, schema modification, and role-based access control to ensure data integrity and secure, read-only access for authorized users.

---
## 💻 **Software Requirements**

- PostgreSQL (Database Server)  
- pgAdmin


---
## 📌 **Objective of the Practical**    
To gain practical experience in implementing Data Definition Language (DDL), Data Manipulation Language (DML), and Data Control Language (DCL) operations in a real database environment. This will also include implementing role-based privileges to secure data.


## 🛠️ **Practical / Experiment Steps**  
- Design the database schema for Department, Employee, and Project tables.  
- Create tables using appropriate constraints.  
- Insert sample records into tables.  
- Perform update and delete operations.  
- Retrieve data using SELECT queries.  
- Create a role and grant and revoke privileges.  
- Alter and drop database objects.  

---

## 🗄️ **Database Design**  

The database is designed to manage Departments, Employees, and Projects within an organization.

### **Tables**  
- Department  
- Employee  
- Project  

### **Constraints Used**  
- PRIMARY KEY – to uniquely identify each record  
- FOREIGN KEY – to maintain relationships between tables  
- NOT NULL – to avoid missing important values  
- UNIQUE – to prevent duplicate entries  

---
 ## ⚙️ **Procedure of the Practical**

⚙️ **Step 1: Table Creation (DDL)**  

### **Department Table**
```sql
CREATE TABLE Department (
    Dept_ID INT PRIMARY KEY,
    Dept_Name VARCHAR(50) UNIQUE NOT NULL,
    Location VARCHAR(50) NOT NULL
);

```

### **Employee Table**
```sql
CREATE TABLE Employee (
    Emp_ID INT PRIMARY KEY,
    Emp_Name VARCHAR(50) NOT NULL,
    Salary INT CHECK (Salary > 0),
    Dept_ID INT REFERENCES Department(Dept_ID),
    Email VARCHAR(100) UNIQUE ); 

```

### **Project Table**
```sql
CREATE TABLE Project (
    Project_ID INT PRIMARY KEY,
    Project_Name VARCHAR(50) NOT NULL,
    Budget INT CHECK (Budget >= 10000),
    Dept_ID INT REFERENCES Department(Dept_ID)
       
);
```

**⚙️Step 2: Data Manipulation (DML)**
### **Insert into Department**
```sql
INSERT INTO Department VALUES
(1, 'HR', 'Mumbai'),
(2, 'IT', 'Pune'),
(3, 'Finance', 'Delhi');

```

### **Insert into Employee**
```sql
INSERT INTO Employee VALUES
(101, 'Alice', 50000, 2, 'alice@org.com'),
(102, 'Bob', 45000, 1, 'bob@org.com'),
(103, 'Charlie', 60000, 2, 'charlie@org.com');

```

### **Insert into Project**
```sql
INSERT INTO Project VALUES
(201, 'Payroll System', 200000, 1),
(202, 'Web Application', 500000, 2);

```

### **Select queries**
```sql
Select * from Department;
Select * from Employee;
Select * from Project;


```
 ✏️ **Step 3: UPDATE Operation**  
```sql
UPDATE Employee
SET Salary = 55000
WHERE Emp_ID = 101
```

 🗑️ **Step 4: DELETE Operations**  

```sql
DELETE FROM Department
WHERE Dept_ID = 3;
```

 🔐 **Step 5: Create Role and Assign Privileges**

### **Create Role**
```sql
CREATE ROLE Analyst
With LOGIN PASSWORD 'analyst111'
```

### **Grant SELECT Privileges**
```sql
GRANT SELECT ON Department TO Analyst;
GRANT SELECT ON Employee TO Analyst;
GRANT SELECT ON Project TO Analyst;

```

### **Revoke Privilege**
```sql
REVOKE CREATE ON DATABASE tpp FROM Analyst;
```

🏗️ **Step 6: Schema Modification**

### **Add Column**
```sql
ALTER TABLE Employee
ADD Phone_No VARCHAR(15);

ALTER TABLE Employee
ALTER COLUMN Emp_Name TYPE VARCHAR(100);

```
### **Drop Table**
```sql
DROP TABLE Project;
```
## 🗄️ **Output** 

##  **Step2 -Select query** 
<img width="527" height="147" alt="1" src="https://github.com/user-attachments/assets/3a5dc127-c9ee-4fd5-b0b5-b48f690280f7" />
<img width="712" height="142" alt="2" src="https://github.com/user-attachments/assets/6c30eabd-87c5-4268-a16e-628b0c6acdf3" />
<img width="520" height="110" alt="3" src="https://github.com/user-attachments/assets/b77cb037-7429-484b-955c-f56499e02d62" />

##  **Step3 -update** 
<img width="712" height="132" alt="4" src="https://github.com/user-attachments/assets/f9b61c52-6591-47e5-906e-da8dab430e7d" />


##  **Step4- delete** 
<img width="537" height="110" alt="5" src="https://github.com/user-attachments/assets/e125a389-c6c7-4b6a-9cb4-2f837314a5da" />

##  **Step5 revoke permission** 
<img width="452" height="162" alt="Screenshot 2026-01-12 223704" src="https://github.com/user-attachments/assets/c6ede2a3-3eb7-47d5-af1c-881764093add" />

##  **Step6- alter** 

<img width="912" height="137" alt="6" src="https://github.com/user-attachments/assets/e145c4a3-ec18-4635-8f9d-0a09ea61c9a3" />

## 📥📤 I/O Analysis (Input / Output)

### 🔹 Input
- Department, Employee, and Project table creation queries  
- Records inserted into all tables using INSERT commands  
- Update query to modify employee department  
- Delete queries to remove project and employee records  
- Role creation and privilege assignment queries  
- ALTER and DROP table commands  

### 🔹 Output
- Department, Employee, and Project tables created successfully  
- Records inserted, updated, and deleted correctly  
- Referential integrity maintained between tables  
- Data displayed correctly using SELECT queries  
- Role-based access verified using GRANT and REVOKE
  Table structure modified and Project table dropped successfully     
📸 Screenshots of obtained results are attached.


## 📘 **Learning Outcomes**  
-	Understand how to design a relational database using multiple tables with proper relationships.
-	Learn to apply constraints to maintain data integrity and consistency.
- Perform basic data manipulation operations such as INSERT, UPDATE, and DELETE.
-	Implement database security by managing users, roles, and access privileges


