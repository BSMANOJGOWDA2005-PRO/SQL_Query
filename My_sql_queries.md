# SQL Fundamentals Notes (Part 1)

## SQL Categories

### DDL (Data Definition Language)
- CREATE
- ALTER
- DROP
- TRUNCATE

### DML (Data Manipulation Language)
- INSERT
- UPDATE
- DELETE

### DQL (Data Query Language)
- SELECT

### TCL (Transaction Control Language)
- COMMIT
- ROLLBACK
- SAVEPOINT

### DCL (Data Control Language)
- GRANT
- REVOKE

---

# Database Commands

## Create Database

```sql
CREATE DATABASE school;
```

```sql
CREATE DATABASE IF NOT EXISTS school;
```

---

## Use Database

```sql
USE school;
```

---

## Show Databases

```sql
SHOW DATABASES;
```

---

## Drop Database

```sql
DROP DATABASE school;
```

```sql
DROP DATABASE IF EXISTS school;
```

---

# Table Commands

## Create Table

```sql
CREATE TABLE student(
student_id INT AUTO_INCREMENT PRIMARY KEY,
student_name VARCHAR(50) NOT NULL,
student_age TINYINT UNSIGNED,
student_email VARCHAR(50) UNIQUE,
student_address VARCHAR(50) DEFAULT 'Bannur',
student_gender ENUM('male','female'),
student_fees INT CHECK(student_fees BETWEEN 15000 AND 35000)
);
```

---

## Show Tables

```sql
SHOW TABLES;
```

---

## Describe Table

```sql
DESC student;
```

```sql
DESCRIBE student;
```

---

# Data Types

## Numeric

- INT
- TINYINT
- SMALLINT
- BIGINT
- DECIMAL
- FLOAT
- DOUBLE

## String

- CHAR
- VARCHAR
- TEXT

## Date

- DATE
- DATETIME
- TIMESTAMP

## Boolean

- BOOLEAN

---

# Constraints

- PRIMARY KEY
- FOREIGN KEY
- UNIQUE
- NOT NULL
- DEFAULT
- CHECK
- AUTO_INCREMENT

---

# INSERT

## Insert Single Row

```sql
INSERT INTO student
VALUES(1,'Manoj',22,'manoj@gmail.com','Mysuru','male',25000);
```

## Insert Multiple Rows

```sql
INSERT INTO student(student_name,student_age)
VALUES
('Rahul',20),
('Ravi',21),
('Sneha',19);
```

## Insert Selected Columns

```sql
INSERT INTO student(student_name,student_age)
VALUES('Kiran',22);
```

---

# SELECT

## All Columns

```sql
SELECT * FROM student;
```

## Selected Columns

```sql
SELECT student_name,student_age
FROM student;
```

## DISTINCT

```sql
SELECT DISTINCT student_address
FROM student;
```

## Alias

```sql
SELECT student_name AS Name
FROM student;
```

---

# WHERE Clause

## Comparison Operators

Equal

```sql
WHERE student_id = 1;
```

Not Equal

```sql
WHERE student_gender <> 'male';
```

```sql
WHERE student_gender != 'male';
```

Greater Than

```sql
WHERE student_fees > 20000;
```

Less Than

```sql
WHERE student_age < 20;
```

Greater Than Equal

```sql
WHERE student_age >= 20;
```

Less Than Equal

```sql
WHERE student_age <= 20;
```

---

## BETWEEN

```sql
WHERE student_fees BETWEEN 15000 AND 25000;
```

```sql
WHERE student_age BETWEEN 18 AND 25;
```

---

## IN

```sql
WHERE student_address IN ('Mysuru','Bannur');
```

```sql
WHERE student_gender IN ('male','female');
```

---

## NOT IN

```sql
WHERE student_address NOT IN ('Mysuru','Bannur');
```

---

## LIKE

Starts With

```sql
WHERE student_name LIKE 'M%';
```

Ends With

```sql
WHERE student_name LIKE '%j';
```

Contains

```sql
WHERE student_name LIKE '%an%';
```

Second Letter

```sql
WHERE student_name LIKE '_a%';
```

Exactly 5 Characters

```sql
WHERE student_name LIKE '_____';
```

Starts with A Ends with N

```sql
WHERE student_name LIKE 'A%n';
```

---

## NOT LIKE

```sql
WHERE student_name NOT LIKE 'A%';
```

---

## NULL

```sql
WHERE student_email IS NULL;
```

```sql
WHERE student_email IS NOT NULL;
```

---

## Logical Operators

### AND

```sql
WHERE student_age > 18
AND student_gender='male';
```

```sql
WHERE student_age>18
AND student_fees>20000;
```

---

### OR

```sql
WHERE student_age<20
OR student_fees<18000;
```

```sql
WHERE student_gender='male'
OR student_address='Mysuru';
```

---

### NOT

```sql
WHERE NOT student_gender='female';
```

```sql
WHERE NOT student_address='Bannur';
```

---

# ORDER BY

Ascending

```sql
ORDER BY student_age ASC;
```

Descending

```sql
ORDER BY student_age DESC;
```

Multiple Columns

```sql
ORDER BY student_address ASC,
student_age DESC;
```

---

# LIMIT

First 5 Rows

```sql
LIMIT 5;
```

First 3 Rows

```sql
LIMIT 3;
```

Offset

```sql
LIMIT 5 OFFSET 10;
```

---

# Aggregate Functions

COUNT

```sql
SELECT COUNT(*) FROM student;
```

SUM

```sql
SELECT SUM(student_fees)
FROM student;
```

AVG

```sql
SELECT AVG(student_fees)
FROM student;
```

MAX

```sql
SELECT MAX(student_age)
FROM student;
```

MIN

```sql
SELECT MIN(student_age)
FROM student;
```

---

# GROUP BY

Count Students

```sql
SELECT student_address,
COUNT(*) AS Total
FROM student
GROUP BY student_address;
```

Average Fees

```sql
SELECT student_address,
AVG(student_fees)
FROM student
GROUP BY student_address;
```

Maximum Fees

```sql
SELECT student_address,
MAX(student_fees)
FROM student
GROUP BY student_address;
```

Minimum Fees

```sql
SELECT student_address,
MIN(student_fees)
FROM student
GROUP BY student_address;
```

Sum Fees

```sql
SELECT student_address,
SUM(student_fees)
FROM student
GROUP BY student_address;
```

---

# HAVING

```sql
SELECT student_address,
COUNT(*) AS Total
FROM student
GROUP BY student_address
HAVING COUNT(*)>=2;
```

```sql
HAVING AVG(student_fees)>20000;
```

```sql
HAVING SUM(student_fees)>50000;
```

---

# UPDATE

Single Column

```sql
UPDATE student
SET student_age=21
WHERE student_id=1;
```

Multiple Columns

```sql
UPDATE student
SET student_age=21,
student_address='Bangalore'
WHERE student_id=1;
```

Using IN

```sql
UPDATE student
SET student_address='Mysuru'
WHERE student_id IN(1,2,3);
```

Using BETWEEN

```sql
UPDATE student
SET student_fees=25000
WHERE student_id BETWEEN 1 AND 5;
```

---

# DELETE

Single Row

```sql
DELETE FROM student
WHERE student_id=1;
```

Using IN

```sql
DELETE FROM student
WHERE student_id IN(2,3,4);
```

Using BETWEEN

```sql
DELETE FROM student
WHERE student_id BETWEEN 5 AND 10;
```

Delete All

```sql
DELETE FROM student;
```

---

# ALTER TABLE

Add Column

```sql
ALTER TABLE student
ADD student_grade VARCHAR(20);
```

Drop Column

```sql
ALTER TABLE student
DROP COLUMN student_grade;
```

Modify Column

```sql
ALTER TABLE student
MODIFY student_age INT;
```

Change Column

```sql
ALTER TABLE student
CHANGE student_age age INT;
```

Rename Column

```sql
ALTER TABLE student
RENAME COLUMN age TO student_age;
```

Rename Table

```sql
ALTER TABLE student
RENAME TO students;
```

---

# TRUNCATE

```sql
TRUNCATE TABLE student;
```

---

# DROP

```sql
DROP TABLE student;
```

```sql
DROP DATABASE school;
```

---

# Foreign Key

```sql
FOREIGN KEY(class_id)
REFERENCES classes(class_id)
ON UPDATE CASCADE
ON DELETE CASCADE;
```

---

# Quick Revision

✔ CREATE DATABASE

✔ USE DATABASE

✔ DROP DATABASE

✔ SHOW DATABASES

✔ CREATE TABLE

✔ SHOW TABLES

✔ DESC

✔ INSERT

✔ SELECT

✔ DISTINCT

✔ WHERE

✔ BETWEEN

✔ IN

✔ NOT IN

✔ LIKE

✔ NOT LIKE

✔ IS NULL

✔ IS NOT NULL

✔ AND

✔ OR

✔ NOT

✔ ORDER BY

✔ LIMIT

✔ COUNT

✔ SUM

✔ AVG

✔ MAX

✔ MIN

✔ GROUP BY

✔ HAVING

✔ UPDATE

✔ DELETE

✔ ALTER TABLE

✔ TRUNCATE

✔ DROP

✔ FOREIGN KEY

✔ PRIMARY KEY

✔ UNIQUE

✔ CHECK

✔ DEFAULT

✔ AUTO_INCREMENT