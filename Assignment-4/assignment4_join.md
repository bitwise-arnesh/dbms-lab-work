# Assignment 4 - JOIN Based Solutions

---

## 1. Find the names in upper case and ages of all sailors.

```sql
SELECT UPPER(SNAME), AGE FROM SAILOR_1003;
```

---

## 2. Select all records from sailors in ascending order by name.

```sql
SELECT * FROM SAILOR_1003 ORDER BY SNAME ASC;
```

---

## 3. Select all distinct sailors' names.

```sql
SELECT DISTINCT SNAME FROM SAILOR_1003;
```

---

## 4. Show all distinct sailors names, ratings who have ratings between 5 and 10.

```sql
SELECT DISTINCT SNAME, RATING 
FROM SAILOR_1003 
WHERE RATING BETWEEN 5 AND 10;
```

---

## 5. Select all records from sailors in ascending order by rating and descending order by age.

```sql
SELECT * 
FROM SAILOR_1003 
ORDER BY RATING ASC, AGE DESC;
```

---

## 6. Find records for sailor name Horatio and age = 35.4.

```sql
SELECT * 
FROM SAILOR_1003 
WHERE SNAME = 'Horatio' AND AGE = 35.4;
```

---

## 7. Select names of sailors who have reserved boat 104.

```sql
SELECT S.SNAME 
FROM SAILOR_1003 S, RESERVED_1003 R
WHERE S.SID = R.SID AND R.BID = 104;
```

---

## 8. Find SID of sailors who have reserved red boat.

```sql
SELECT DISTINCT S.SID 
FROM SAILOR_1003 S, RESERVED_1003 R, BOAT_1003 B
WHERE S.SID = R.SID 
AND R.BID = B.BID 
AND B.COLOR = 'red';
```

---

## 9. Select names for rating present.

```sql
SELECT SNAME 
FROM SAILOR_1003 
WHERE RATING IS NOT NULL;
```

---

## 10. Select names for rating absent.

```sql
SELECT SNAME 
FROM SAILOR_1003 
WHERE RATING IS NULL;
```

---

## 11. Find the color of boats reserved by Lubber.

```sql
SELECT B.COLOR 
FROM BOAT_1003 B, SAILOR_1003 S, RESERVED_1003 R
WHERE B.BID = R.BID 
AND S.SID = R.SID 
AND S.SNAME = 'Lubber';
```

---

## 12. Find a sailor name that has reserved at least one boat.

```sql
SELECT DISTINCT S.SNAME 
FROM SAILOR_1003 S, RESERVED_1003 R
WHERE S.SID = R.SID;
```

---

## 13. Find the names of sailors whose name begins with B and has at least 3 characters.

```sql
SELECT SNAME 
FROM SAILOR_1003 
WHERE SNAME LIKE 'B%' AND LENGTH(SNAME) >= 3;
```

---

## 14. Find names of sailors whose name begins and ends with 'B' and has exactly 3 chars.

```sql
SELECT SNAME 
FROM SAILOR_1003 
WHERE SNAME LIKE 'B_B';
```

---

## 15. Find names of sailors who have reserved a red boat or a green boat.

```sql
SELECT DISTINCT S.SNAME 
FROM SAILOR_1003 S, RESERVED_1003 R, BOAT_1003 B
WHERE S.SID = R.SID 
AND R.BID = B.BID 
AND (B.COLOR = 'red' OR B.COLOR = 'green');
```

---

## 16. Find names of sailors who have reserved a red boat but not a green boat.

```sql
SELECT DISTINCT S.SNAME 
FROM SAILOR_1003 S
WHERE S.SID IN (
    SELECT R.SID 
    FROM RESERVED_1003 R, BOAT_1003 B
    WHERE R.BID = B.BID AND B.COLOR = 'red'
)
AND S.SID NOT IN (
    SELECT R.SID 
    FROM RESERVED_1003 R, BOAT_1003 B
    WHERE R.BID = B.BID AND B.COLOR = 'green'
);
```

---

## 17. Find names of sailors who have reserved boat 103.

```sql
SELECT S.SNAME 
FROM SAILOR_1003 S, RESERVED_1003 R
WHERE S.SID = R.SID AND R.BID = 103;
```

---

## 18. Find names of sailors who have reserved a red boat.

```sql
SELECT DISTINCT S.SNAME 
FROM SAILOR_1003 S, RESERVED_1003 R, BOAT_1003 B
WHERE S.SID = R.SID 
AND R.BID = B.BID 
AND B.COLOR = 'red';
```

---

## 19. Find names of sailors who have not reserved red boats.

```sql
SELECT SNAME 
FROM SAILOR_1003 
WHERE SID NOT IN (
    SELECT R.SID 
    FROM RESERVED_1003 R, BOAT_1003 B
    WHERE R.BID = B.BID AND B.COLOR = 'red'
);
```

---

## 20. Find all records of sailors for which rating is greater than the rating of Horatio.

```sql
SELECT S1.* 
FROM SAILOR_1003 S1, SAILOR_1003 S2
WHERE S1.RATING > S2.RATING 
AND S2.SNAME = 'Horatio';
```

---

## 21. Find average age of sailors with rating 10.

```sql
SELECT AVG(AGE) 
FROM SAILOR_1003 
WHERE RATING = 10;
```

---

## 22. Find the names of sailors who are older than the oldest sailor of rating = 10.

```sql
SELECT SNAME 
FROM SAILOR_1003 
WHERE AGE > (
    SELECT MAX(AGE) 
    FROM SAILOR_1003 
    WHERE RATING = 10
);
```

---

## 23. Find the age of the youngest sailor for each rating level.

```sql
SELECT RATING, MIN(AGE) 
FROM SAILOR_1003 
GROUP BY RATING;
```

---

## 24. Find the name of each sailor who is eligible to vote for each rating level.

```sql
SELECT SNAME, RATING 
FROM SAILOR_1003 
WHERE AGE >= 18;
```

---

## 25. Find the average age of sailor for each rating level with at least two sailors.

```sql
SELECT RATING, AVG(AGE) 
FROM SAILOR_1003 
GROUP BY RATING 
HAVING COUNT(*) >= 2;
```

---

## 26. For each red boat count the number of reservations.

```sql
SELECT B.BID, COUNT(R.SID) 
FROM BOAT_1003 B, RESERVED_1003 R
WHERE B.BID = R.BID 
AND B.COLOR = 'red'
GROUP BY B.BID;
```

---

## 27. Find the records of the sailor who is getting the 2nd highest rating.

```sql
SELECT * 
FROM SAILOR_1003 
WHERE RATING = (
    SELECT MAX(RATING) 
    FROM SAILOR_1003 
    WHERE RATING < (SELECT MAX(RATING) FROM SAILOR_1003)
);
```

---

## 28. Find the name of sailors who got 3rd minimum rating.

```sql
SELECT SNAME 
FROM SAILOR_1003 
WHERE RATING = (
    SELECT MIN(RATING) 
    FROM SAILOR_1003 
    WHERE RATING > (
        SELECT MIN(RATING) 
        FROM SAILOR_1003 
        WHERE RATING > (SELECT MIN(RATING) FROM SAILOR_1003)
    )
);
```

---

## 29. Find sailors who have reserved all boats.

```sql
SELECT S.SNAME 
FROM SAILOR_1003 S, RESERVED_1003 R
WHERE S.SID = R.SID
GROUP BY S.SNAME
HAVING COUNT(DISTINCT R.BID) = (SELECT COUNT(*) FROM BOAT_1003);
```

---

## 30. Find sailors who have reserved more than 2 boats.

```sql
SELECT S.SNAME 
FROM SAILOR_1003 S, RESERVED_1003 R
WHERE S.SID = R.SID
GROUP BY S.SNAME
HAVING COUNT(DISTINCT R.BID) > 2;
```
