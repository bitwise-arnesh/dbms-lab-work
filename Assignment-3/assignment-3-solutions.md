# Assignment 3

## 1. Retrieve the Name of Book and Cost who has Maximum cost.

```sql
SELECT BOOK_NAME, COST 
FROM BOOKS 
WHERE COST = (SELECT MAX(COST) FROM BOOKS);
```

---

## 2. Calculate the Minimum cost, Average cost and Total cost value in BOOKS table and Rename the resulting attributes.

```sql
SELECT MIN(COST) AS MIN_COST,
       AVG(COST) AS AVG_COST,
       SUM(COST) AS TOTAL_COST
FROM BOOKS;
```

---

## 3. Retrieve the Name and ID of Members who’s issued book between 26th January 2011 and 14th April 2011.

```sql
SELECT DISTINCT M.MEMBER_ID, M.MEMBER_NAME
FROM MEMBER M, ISSUE I
WHERE M.MEMBER_ID = I.MEMBER_ID
AND ISSUE_DATE BETWEEN DATE '2011-01-26' AND DATE '2011-04-14';
```

---

## 4. Retrieve Book Name, Author Name and Category whose Category is not ‘OTHERS’.

```sql
SELECT BOOK_NAME, AUTHOR_NAME, CATEGORY
FROM BOOKS
WHERE CATEGORY <> 'OTHERS';
```

---

## 5. A. Retrieve the Book name and Author Name where –

### a. 5th letter of the Author name is ‘t’.

```sql
SELECT BOOK_NAME, AUTHOR_NAME
FROM BOOKS
WHERE AUTHOR_NAME LIKE '____T%';
```

### b. Author name starts with ‘S’.

```sql
SELECT BOOK_NAME, AUTHOR_NAME
FROM BOOKS
WHERE AUTHOR_NAME LIKE 'S%';
```

### c. Author name starts with ‘S’ and contains at least one letter after that.

```sql
SELECT BOOK_NAME, AUTHOR_NAME
FROM BOOKS
WHERE AUTHOR_NAME LIKE 'S_%';
```

### d. Author name ends with the letter ‘a’.

```sql
SELECT BOOK_NAME, AUTHOR_NAME
FROM BOOKS
WHERE AUTHOR_NAME LIKE '%A';
```

### e. 3rd and 5th letters of the Author name is ‘a’.

```sql
SELECT BOOK_NAME, AUTHOR_NAME
FROM BOOKS
WHERE SUBSTR(AUTHOR_NAME,3,1)='A'
AND SUBSTR(AUTHOR_NAME,5,1)='A';
```

### f. 2nd last letter of the author name is ‘a’.

```sql
SELECT BOOK_NAME, AUTHOR_NAME
FROM BOOKS
WHERE SUBSTR(AUTHOR_NAME,-2,1)='A';
```

### g. Author name starts with ‘D’ and ends with ‘e’.

```sql
SELECT BOOK_NAME, AUTHOR_NAME
FROM BOOKS
WHERE AUTHOR_NAME LIKE 'D%E';
```

---

## 5. B. List all the Members whose name –

### h. Starts with S.

```sql
SELECT MEMBER_NAME FROM MEMBER WHERE MEMBER_NAME LIKE 'S%';
```

### i. Starts with S or A and contains letter T in it.

```sql
SELECT MEMBER_NAME 
FROM MEMBER 
WHERE (MEMBER_NAME LIKE 'S%' OR MEMBER_NAME LIKE 'A%')
AND MEMBER_NAME LIKE '%T%';
```

---

## 5. C. List all the books that contain the word ‘SQL’ in the name of the book.

```sql
SELECT BOOK_NAME FROM BOOKS WHERE BOOK_NAME LIKE '%SQL%';
```

---

## 6. How many Books are available whose Cost is greater than 350.

```sql
SELECT COUNT(*) FROM BOOKS WHERE COST > 350;
```

---

## 7. How many different Authors name are available in the BOOKS table.

```sql
SELECT COUNT(DISTINCT AUTHOR_NAME) FROM BOOKS;
```

---

## 8. Calculate the following Numeric functions:

### a. What is the absolute value of -167.

```sql
SELECT ABS(-167) FROM DUAL;
```

### b. Calculate 8%6.

```sql
SELECT MOD(8,6) FROM DUAL;
```

### c. Round up to 2 decimal points (134.56789).

```sql
SELECT ROUND(134.56789,2) FROM DUAL;
```

### d. What is the square root of 144.

```sql
SELECT SQRT(144) FROM DUAL;
```

### e. Floor and Ceil value of 13.15.

```sql
SELECT FLOOR(13.15), CEIL(13.15) FROM DUAL;
```

---

## 9. Extract Year, Month, Day from System Date.

```sql
SELECT EXTRACT(YEAR FROM SYSDATE),
       EXTRACT(MONTH FROM SYSDATE),
       EXTRACT(DAY FROM SYSDATE)
FROM DUAL;
```

---

## 10. What is the greatest value between 4, 5 and 17.

```sql
SELECT GREATEST(4,5,17) FROM DUAL;
```

---

## 11. What is the Least value between ‘4’, ‘5’ and ‘17’.

```sql
SELECT LEAST(4,5,17) FROM DUAL;
```

---

## 12. Extract 4 letters from 3rd position of this word ‘INFOSYS’.

```sql
SELECT SUBSTR('INFOSYS',3,4) FROM DUAL;
```

---

## 13. What is the ASCII value of ‘a’ and ‘S’.

```sql
SELECT ASCII('A'), ASCII('S') FROM DUAL;
```

---

## 14. What is Length of this word ‘INFOSYS’ AND change ‘S’ with ‘T’.

```sql
SELECT LENGTH('INFOSYS'), REPLACE('INFOSYS','S','T') FROM DUAL;
```

---

## 15. Retrieve the Names and Address of the Members who belong to Kolkata.

```sql
SELECT MEMBER_NAME, MEMBER_ADDRESS
FROM MEMBER
WHERE MEMBER_ADDRESS='KOLKATA';
```

---

## 16. Retrieve the Name of Books, where Cost prices are between 300 and 500.

```sql
SELECT BOOK_NAME 
FROM BOOKS 
WHERE COST BETWEEN 300 AND 500;
```

---

## 17. List the Name of the Members whose Membership type is “HALF YEARLY”.

```sql
SELECT MEMBER_NAME 
FROM MEMBER 
WHERE MEMBERSHIP_TYPE='HALF YEARLY';
```

---

## 18. List the Name of the Members who open their accounts in the year 2011.

```sql
SELECT MEMBER_NAME 
FROM MEMBER 
WHERE EXTRACT(YEAR FROM ACC_OPEN_DATE)=2011;
```

---

## 19. Retrieve the Penalty Amount of the Members who has taken the book “LET US C”.

```sql
SELECT M.PENALTY_AMOUNT
FROM MEMBER M, ISSUE I, BOOKS B
WHERE M.MEMBER_ID = I.MEMBER_ID
AND I.BOOK_NO = B.BOOK_NO
AND B.BOOK_NAME='LET US C';
```

---

## 20. Retrieve the no of Max books allowed to a Member, who has issued books on January.

```sql
SELECT DISTINCT MAX_BOOKS_ALLOWED
FROM MEMBER M, ISSUE I
WHERE M.MEMBER_ID = I.MEMBER_ID
AND TO_CHAR(ISSUE_DATE,'MON')='JAN';
```

---

## 21. Give the Names of the Members who have not issued any books.

```sql
SELECT MEMBER_NAME
FROM MEMBER
WHERE MEMBER_ID NOT IN (SELECT MEMBER_ID FROM ISSUE);
```

---

## 22. Give the Name and Category of the books whose cost is not recorded.

```sql
SELECT BOOK_NAME, CATEGORY
FROM BOOKS
WHERE COST IS NULL;
```

---

## 23. List all the books that are written by Author ‘Loni’ and has Price less than 600.

```sql
SELECT BOOK_NAME
FROM BOOKS
WHERE AUTHOR_NAME='LONI' AND COST < 600;
```

---

## 24. List the Issue details for the Books that are not returned yet.

```sql
SELECT * FROM ISSUE WHERE RETURN_DATE IS NULL;
```

---

## 25. List all the Books that belong to any one of the following categories Science, Database.

```sql
SELECT * FROM BOOKS 
WHERE CATEGORY IN ('SCIENCE','DATABASE');
```

---

## 26. List all the Members in descending order of Penalty due on them.

```sql
SELECT * FROM MEMBER 
ORDER BY PENALTY_AMOUNT DESC;
```

---

## 27. List all the Books in ascending order of category and descending order of price.

```sql
SELECT * FROM BOOKS 
ORDER BY CATEGORY ASC, COST DESC;
```

---

## 28. List the Entire Book name in INIT CAP and Author Name in UPPER case in the descending order of the Book Name.

```sql
SELECT INITCAP(BOOK_NAME), UPPER(AUTHOR_NAME)
FROM BOOKS
ORDER BY BOOK_NAME DESC;
```

---

## 29. List the data in the book table with category data displayed as ‘D’ for Database, ‘S’ for Science, ‘R’ for RDBMS and ‘O’ for all the others.

```sql
SELECT BOOK_NAME,
CASE
WHEN CATEGORY='DATABASE' THEN 'D'
WHEN CATEGORY='SCIENCE' THEN 'S'
WHEN CATEGORY='RDBMS' THEN 'R'
ELSE 'O'
END
FROM BOOKS;
```

---

## 30. List all the Members that became the Member in the year 2011.

```sql
SELECT MEMBER_NAME
FROM MEMBER
WHERE EXTRACT(YEAR FROM ACC_OPEN_DATE)=2011;
```
