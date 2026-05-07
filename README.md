# DBMS Lab Work

<p align="center">
  <img src="https://img.shields.io/badge/Oracle-SQL-red" />
  <img src="https://img.shields.io/badge/DBMS-Laboratory-blue" />
  <img src="https://img.shields.io/badge/PLSQL-Programming-green" />
</p>

A curated collection of SQL and PL/SQL assignments focused on relational database concepts, query writing, and procedural database programming using Oracle SQL.

---

## Overview

This repository contains practical implementations of:

* SQL Queries
* Database Design
* Constraints & Relationships
* Joins & Subqueries
* Aggregate Functions
* Sequences
* PL/SQL Programs
* String Manipulation
* Record Handling
* Real-world Database Queries

---

## Repository Structure

```text id="bbjlwm"
DBMS-Lab-Work/
│
├── Assignment-1/
├── Assignment-2/
├── Assignment-3/
├── Assignment-4/
├── Assignment-5/
├── Assignment-6/
├── Assignment-7/
└── README.md
```

---

# Assignments

## Assignment 1 — SQL Basics

* Basic SQL Queries
* Table Creation
* Constraints

---

## Assignment 2 — Constraints & Insert Operations

* ALTER TABLE
* Primary Key
* Foreign Key
* CHECK Constraints
* INSERT Queries

---

## Assignment 3 — Joins & Aggregate Functions

* Joins
* GROUP BY
* HAVING Clause
* Aggregate Functions

---

## Assignment 4 — Subqueries

* Nested Queries
* Correlated Subqueries
* EXISTS & IN Operators

---

## Assignment 5 — Advanced SQL Concepts

* Set Operations
* Views
* Sequences
* Indexes

---

## Assignment 6 — Cricket Database Management System

A cricket database system implemented using Oracle SQL.

### Features

* Sequence Creation
* Relational Table Design
* Foreign Key Constraints
* Data Insertion
* Complex SQL Queries
* Aggregate Operations
* Nested Queries

### Tables Included

* Match
* Player
* Bowling
* Batting

### Sample Query

```sql id="t1ux2r"
SELECT P.Fname, P.Lname, M.Ground
FROM Player P, Bowling B, Match M
WHERE P.Player_Id = B.Player_Id
AND B.Match_Id = M.Match_Id;
```

---

## Assignment 7 — PL/SQL Programming

Collection of PL/SQL programs demonstrating procedural database programming concepts.

### Programs Included

* Largest of Two Numbers
* Even/Odd Check
* Factorial Program
* Leap Year Check
* Reverse String
* String Processing
* Record Variables
* Table Update Operations

### Concepts Covered

* Conditional Statements
* Loops
* DBMS_OUTPUT
* String Manipulation
* Record Handling
* Table Operations

### Sample Program

```sql id="7kttsr"
DECLARE
    N NUMBER;
    I NUMBER;
    FACT NUMBER := 1;
BEGIN
    N := :N;

    FOR I IN 1..N LOOP
        FACT := FACT * I;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE(FACT);
END;
/
```

---

# Technologies Used

* Oracle SQL
* PL/SQL
* Oracle SQL Developer
* Relational Database Concepts

---

# Author

**Arnesh Bera**

GitHub: https://github.com/bitwise-arnesh
