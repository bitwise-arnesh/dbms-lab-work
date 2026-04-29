# DBMS LAB – ASSIGNMENT 5

## Question 1

For every project located in 'Stafford', list the project number, the controlling department number, and the department manager's last name, address, and birth date.

### Answer

```sql
SELECT PNUMBER, DNUM, LNAME, ADDRESS, BDATE
FROM PROJECT_1000, DEPARTMENT_1000, EMPLOYEE_1000
WHERE DNUM = DNUMBER 
AND MGRSSN = SSN 
AND PLOCATION = 'Stafford';
```

---

## Question 2

Retrieve the name of each employee who works on all the projects controlled by department number 5.

### Answer

```sql
SELECT FNAME, LNAME 
FROM EMPLOYEE_1000 
WHERE NOT EXISTS 
((SELECT PNUMBER FROM PROJECT_1000 WHERE DNUM=5)
MINUS
(SELECT PNO FROM WORKS_ON_1000 WHERE SSN=ESSN));
```

---

## Question 3

Make a list of all project numbers for projects that involve an employee whose last name is 'Smith'.

### Answer

```sql
SELECT PNUMBER
FROM PROJECT_1000, DEPARTMENT_1000, EMPLOYEE_1000
WHERE DNUM = DNUMBER 
AND MGRSSN = SSN 
AND LNAME = 'Smith'

UNION

SELECT PNUMBER
FROM PROJECT_1000, WORKS_ON_1000, EMPLOYEE_1000
WHERE PNUMBER = PNO 
AND ESSN = SSN 
AND LNAME = 'Smith';
```

---

## Question 4

Retrieve the names of employees who have no dependents.

### Answer

```sql
SELECT FNAME, MINIT, LNAME 
FROM EMPLOYEE_1000 
WHERE SSN NOT IN 
(SELECT ESSN FROM DEPENDENT_1000);
```

---

## Question 5

List the names of managers who have at least one dependent.

### Answer

```sql
SELECT FNAME, MINIT, LNAME 
FROM EMPLOYEE_1000, DEPARTMENT_1000
WHERE SSN = MGRSSN 
AND SSN IN (SELECT ESSN FROM DEPENDENT_1000);
```

---

## Question 6

For each employee, retrieve the employee's first and last name and the first and last name of his or her immediate supervisor.

### Answer

```sql
SELECT E.FNAME, E.LNAME, S.FNAME, S.LNAME 
FROM EMPLOYEE E, EMPLOYEE S
WHERE E.SUPERSSN = S.SSN;
```

---

## Question 7

Show the resulting salaries if every employee working on the 'ProductX' project is given a 10 percent raise.

### Answer

```sql
SELECT 1.1 * SALARY
FROM EMPLOYEE, WORKS_ON, PROJECT
WHERE SSN = ESSN 
AND PNO = PNUMBER 
AND PNAME = 'ProductX';
```

---

## Question 8

Retrieve a list of employees and the projects they are working on, ordered by department and, within each department, ordered alphabetically by last name, first name.

### Answer

```sql
SELECT DNO, LNAME, FNAME, PNAME
FROM EMPLOYEE, WORKS_ON, PROJECT
WHERE SSN = ESSN 
AND PNO = PNUMBER
ORDER BY DNO, LNAME, FNAME;
```

---

## Question 9

Retrieve the names of all employees who do not have supervisors.

### Answer

```sql
SELECT FNAME, LNAME 
FROM EMPLOYEE
WHERE SUPERSSN IS NULL;
```

---

## Question 10

Retrieve the name of each employee who has a dependent with the same last name as the employee.

### Answer

```sql
SELECT FNAME, LNAME 
FROM EMPLOYEE, DEPENDENT
WHERE SSN = ESSN 
AND LNAME = DEPENDENT_NAME;
```

---

## Question 11

Retrieve the social security numbers of all employees who work on project numbers 1 and 2.

### Answer

```sql
SELECT DISTINCT ESSN 
FROM WORKS_ON
WHERE PNO IN (1,2);
```

---

## Question 12

Return the names of employees whose salary is greater than the salary of all the employees in department 5.

### Answer

```sql
SELECT FNAME, LNAME 
FROM EMPLOYEE
WHERE SALARY > ALL 
(SELECT SALARY FROM EMPLOYEE WHERE DNO = 5);
```

---

## Question 13

Find the sum of the salaries of all employees, the maximum salary, the minimum salary, and the average salary.

### Answer

```sql
SELECT SUM(SALARY), MAX(SALARY), MIN(SALARY), ROUND(AVG(SALARY),2)
FROM EMPLOYEE;
```

---

## Question 14

Find the sum of the salaries of all employees of the 'Research' department, as well as the maximum salary, the minimum salary, and the average salary in this department.

### Answer

```sql
SELECT SUM(SALARY), MAX(SALARY), MIN(SALARY), AVG(SALARY)
FROM EMPLOYEE, DEPARTMENT
WHERE DNO = DNUMBER 
AND DNAME = 'Research';
```

---

## Question 15

Retrieve the names of all employees who have two or more dependents.

### Answer

```sql
SELECT FNAME, LNAME 
FROM EMPLOYEE_1000 
WHERE SSN IN 
(SELECT ESSN 
 FROM DEPENDENT_1000 
 GROUP BY ESSN 
 HAVING COUNT(*) > 2);
```

---

## Question 16

Count the total number of employees whose salaries exceed 20000 in each department, but only for departments where more than two employees work.

### Answer

```sql
SELECT COUNT(*) 
FROM EMPLOYEE_1000 
WHERE SALARY > 20000
GROUP BY DNO 
HAVING COUNT(SSN) > 2;
```

---

## Question 17

For each project, retrieve the project number, the project name, and the number of employees who work on that project.

### Answer

```sql
SELECT PNUMBER, PNAME, COUNT(*)
FROM PROJECT_1000, WORKS_ON_1000
WHERE PNUMBER = PNO
GROUP BY PNUMBER, PNAME;
```

---

## Question 18

For each project on which more than two employees work, retrieve the project number, the project name, and the number of employees who work on that project.

### Answer

```sql
SELECT PNUMBER, PNAME, COUNT(*)
FROM PROJECT_1000, WORKS_ON_1000
WHERE PNUMBER = PNO
GROUP BY PNUMBER, PNAME
HAVING COUNT(*) > 2;
```

---

## Question 19

For each project, retrieve the project number, the project name, and the number of employees from department 5 who work on that project.

### Answer

```sql
SELECT PNUMBER, PNAME, COUNT(*)
FROM PROJECT_1000, WORKS_ON_1000
WHERE PNUMBER = PNO 
AND DNUM = 5
GROUP BY PNUMBER, PNAME;
```

---

## Question 20

For each department that has more than five employees, retrieve the department number and the number of its employees who are making more than 40000.

### Answer

```sql
SELECT DNO, COUNT(*)
FROM EMPLOYEE
WHERE SALARY > 40000
GROUP BY DNO
HAVING COUNT(*) > 5;
```

---
