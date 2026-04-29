# Assignment 4 - Subquery Based Solutions

---

## 1. Find the names in upper case and ages of all sailors.

```sql id="x1"
SELECT UPPER(SNAME), AGE FROM SAILOR_1003;
```

---

## 2. Select all records from sailors in ascending order by name.

```sql id="x2"
SELECT * FROM SAILOR_1003 ORDER BY SNAME ASC;
```

---

## 3. Select all distinct sailors' names.

```sql id="x3"
SELECT DISTINCT SNAME FROM SAILOR_1003;
```

---

## 4. Show all distinct sailors names, ratings who have ratings between 5 and 10.

```sql id="x4"
SELECT DISTINCT SNAME, RATING 
FROM SAILOR_1003 
WHERE RATING BETWEEN 5 AND 10;
```

---

## 5. Select all records from sailors in ascending order by rating and descending order by age.

```sql id="x5"
SELECT * 
FROM SAILOR_1003 
ORDER BY RATING ASC, AGE DESC;
```

---

## 6. Find records for sailor name Horatio and age = 35.4.

```sql id="x6"
SELECT * 
FROM SAILOR_1003 
WHERE SNAME = 'Horatio' AND AGE = 35.4;
```

---

## 7. Select names of sailors who have reserved boat 104.

```sql id="x7"
SELECT SNAME 
FROM SAILOR_1003
WHERE SID IN (
    SELECT SID FROM RESERVED_1003 WHERE BID = 104
);
```

---

## 8. Find SID of sailors who have reserved red boat.

```sql id="x8"
SELECT DISTINCT SID 
FROM RESERVED_1003
WHERE BID IN (
    SELECT BID FROM BOAT_1003 WHERE COLOR = 'red'
);
```

---

## 9. Select names for rating present.

```sql id="x9"
SELECT SNAME 
FROM SAILOR_1003 
WHERE RATING IS NOT NULL;
```

---

## 10. Select names for rating absent.

```sql id="x10"
SELECT SNAME 
FROM SAILOR_1003 
WHERE RATING IS NULL;
```

---

## 11. Find the color of boats reserved by Lubber.

```sql id="x11"
SELECT COLOR 
FROM BOAT_1003
WHERE BID IN (
    SELECT BID FROM RESERVED_1003
    WHERE SID = (
        SELECT SID FROM SAILOR_1003 WHERE SNAME = 'Lubber'
    )
);
```

---

## 12. Find a sailor name that has reserved at least one boat.

```sql id="x12"
SELECT DISTINCT SNAME 
FROM SAILOR_1003
WHERE SID IN (SELECT SID FROM RESERVED_1003);
```

---

## 13. Find the names of sailors whose name begins with B and has at least 3 characters.

```sql id="x13"
SELECT SNAME 
FROM SAILOR_1003 
WHERE SNAME LIKE 'B%' AND LENGTH(SNAME) >= 3;
```

---

## 14. Find names of sailors whose name begins and ends with 'B' and has exactly 3 chars.

```sql id="x14"
SELECT SNAME 
FROM SAILOR_1003 
WHERE SNAME LIKE 'B_B';
```

---

## 15. Find names of sailors who have reserved a red boat or a green boat.

```sql id="x15"
SELECT DISTINCT SNAME 
FROM SAILOR_1003
WHERE SID IN (
    SELECT SID FROM RESERVED_1003
    WHERE BID IN (
        SELECT BID FROM BOAT_1003 WHERE COLOR IN ('red','green')
    )
);
```

---

## 16. Find names of sailors who have reserved a red boat but not a green boat.

```sql id="x16"
SELECT DISTINCT SNAME 
FROM SAILOR_1003
WHERE SID IN (
    SELECT SID FROM RESERVED_1003
    WHERE BID IN (SELECT BID FROM BOAT_1003 WHERE COLOR = 'red')
)
AND SID NOT IN (
    SELECT SID FROM RESERVED_1003
    WHERE BID IN (SELECT BID FROM BOAT_1003 WHERE COLOR = 'green')
);
```

---

## 17. Find names of sailors who have reserved boat 103.

```sql id="x17"
SELECT SNAME 
FROM SAILOR_1003
WHERE SID IN (
    SELECT SID FROM RESERVED_1003 WHERE BID = 103
);
```

---

## 18. Find names of sailors who have reserved a red boat.

```sql id="x18"
SELECT DISTINCT SNAME 
FROM SAILOR_1003
WHERE SID IN (
    SELECT SID FROM RESERVED_1003
    WHERE BID IN (
        SELECT BID FROM BOAT_1003 WHERE COLOR = 'red'
    )
);
```

---

## 19. Find names of sailors who have not reserved red boats.

```sql id="x19"
SELECT SNAME 
FROM SAILOR_1003
WHERE SID NOT IN (
    SELECT SID FROM RESERVED_1003
    WHERE BID IN (
        SELECT BID FROM BOAT_1003 WHERE COLOR = 'red'
    )
);
```

---

## 20. Find all records of sailors for which rating is greater than the rating of Horatio.

```sql id="x20"
SELECT * 
FROM SAILOR_1003
WHERE RATING > (
    SELECT RATING FROM SAILOR_1003 WHERE SNAME = 'Horatio'
);
```

---

## 21. Find average age of sailors with rating 10.

```sql id="x21"
SELECT AVG(AGE) 
FROM SAILOR_1003 
WHERE RATING = 10;
```

---

## 22. Find the names of sailors who are older than the oldest sailor of rating = 10.

```sql id="x22"
SELECT SNAME 
FROM SAILOR_1003
WHERE AGE > (
    SELECT MAX(AGE) FROM SAILOR_1003 WHERE RATING = 10
);
```

---

## 23. Find the age of the youngest sailor for each rating level.

```sql id="x23"
SELECT RATING, MIN(AGE) 
FROM SAILOR_1003 
GROUP BY RATING;
```

---

## 24. Find the name of each sailor who is eligible to vote for each rating level.

```sql id="x24"
SELECT SNAME, RATING 
FROM SAILOR_1003 
WHERE AGE >= 18;
```

---

## 25. Find the average age of sailor for each rating level with at least two sailors.

```sql id="x25"
SELECT RATING, AVG(AGE) 
FROM SAILOR_1003 
GROUP BY RATING 
HAVING COUNT(*) >= 2;
```

---

## 26. For each red boat count the number of reservations.

```sql id="x26"
SELECT BID, COUNT(*) 
FROM RESERVED_1003
WHERE BID IN (SELECT BID FROM BOAT_1003 WHERE COLOR = 'red')
GROUP BY BID;
```

---

## 27. Find the records of the sailor who is getting the 2nd highest rating.

```sql id="x27"
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

```sql id="x28"
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

```sql id="x29"
SELECT SNAME 
FROM SAILOR_1003 S
WHERE NOT EXISTS (
    SELECT BID FROM BOAT_1003
    MINUS
    SELECT BID FROM RESERVED_1003 R WHERE R.SID = S.SID
);
```

---

## 30. Find sailors who have reserved more than 2 boats.

```sql id="x30"
SELECT SNAME 
FROM SAILOR_1003
WHERE SID IN (
    SELECT SID 
    FROM RESERVED_1003 
    GROUP BY SID 
    HAVING COUNT(BID) > 2
);
```
