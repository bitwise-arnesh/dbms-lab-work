## Question 1

Create a table `Student` with given structure.

### SQL Query

```sql
CREATE TABLE STUDENT_1003 (
    ROLL NUMBER(5),
    NAME VARCHAR2(30),
    AGE NUMBER(5),
    COURSE VARCHAR2(5),
    MATH NUMBER(6,2),
    PHYSICS NUMBER(6,2),
    COMPUTER NUMBER(6,2),
    BIRTHDAY DATE
);
```

---

## Question 2

Create table MSc from Student with same structure but no data.

### SQL Query

```sql
CREATE TABLE MSC_1003 AS 
SELECT * FROM STUDENT_1003 WHERE 1=2;
```

---

## Question 3

Display structure of MSc table.

### SQL Query

```sql
DESC MSC_1003;
```

---

## Question 4

Create table MCA from Student with same structure, rename Course → Department, Name → FirstName.

### SQL Query

```sql
CREATE TABLE MCA_1003 AS 
SELECT 
    ROLL,
    NAME AS FIRSTNAME,
    AGE,
    COURSE AS DEPARTMENT,
    MATH,
    PHYSICS,
    COMPUTER,
    BIRTHDAY
FROM STUDENT_1003
WHERE 1=2;
```

---

## Question 5

Display structure of MCA table.

### SQL Query

```sql
DESC MCA_1003;
```

---

## Question 6

Insert records into Student table.

### SQL Query

```sql
INSERT INTO STUDENT_1003 VALUES(1,'RAHUL',19,'BCA',79.5,67,89,'15-JUN-93');
INSERT INTO STUDENT_1003 VALUES(2,'KUNAL',21,'BCA',68,76,59.5,'16-AUG-91');
INSERT INTO STUDENT_1003 VALUES(3,'ADITI',20,'MSC',90,73,56,'20-SEP-92');
INSERT INTO STUDENT_1003 VALUES(4,'SUMIT',20,'MCA',57.5,78,81,'07-DEC-91');
INSERT INTO STUDENT_1003 VALUES(5,'ANIRBAN',22,'MCA',80,68,63,'15-SEP-94');
INSERT INTO STUDENT_1003 VALUES(6,'KUMKUM',21,'BCA',72,54.5,60,'08-FEB-95');
INSERT INTO STUDENT_1003 VALUES(7,'SUMAN',21,'BCA',91.5,32,61,'10-MAR-94');
INSERT INTO STUDENT_1003 VALUES(8,'ROHIT',22,'MSC',85,76,92,'19-APR-92');
```

---

## Question 7

Display all student details.

### SQL Query

```sql
SELECT * FROM STUDENT_1003;
```

---

## Question 8

Find details of student with Roll = 5.

### SQL Query

```sql
SELECT * FROM STUDENT_1003 WHERE ROLL=5;
```

---

## Question 9

Show roll, name, and marks.

### SQL Query

```sql
SELECT ROLL, NAME, MATH, PHYSICS, COMPUTER FROM STUDENT_1003;
```

---

## Question 10

Insert data into MCA table where course is MCA.

### SQL Query

```sql
INSERT INTO MCA_1003
SELECT * FROM STUDENT_1003 WHERE COURSE='MCA';
```

---

## Question 11

Display structure of Student and MCA tables.

### SQL Query

```sql
DESC STUDENT_1003;
DESC MCA_1003;
```

---

## Question 12

Update Math marks (Roll 7 → 95).

### SQL Query

```sql
UPDATE STUDENT_1003 
SET MATH=95 
WHERE ROLL=7;
```

---

## Question 13

Delete student with Roll = 2.

### SQL Query

```sql
DELETE FROM STUDENT_1003 
WHERE ROLL=2;
```
