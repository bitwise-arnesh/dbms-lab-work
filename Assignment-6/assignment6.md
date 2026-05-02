# Assignment 6 - DBMS Lab

## 🔹 Step 1: Create Sequences

```sql
CREATE SEQUENCE match_seq START WITH 1 INCREMENT BY 1;
CREATE SEQUENCE player_seq START WITH 1 INCREMENT BY 1;
CREATE SEQUENCE bowling_seq START WITH 1000 INCREMENT BY 2;
CREATE SEQUENCE batting_seq START WITH 500 INCREMENT BY 1;
```

---

## 🔹 Step 2: Create Tables

### Match Table

```sql
CREATE TABLE Match (
    SLNO NUMBER PRIMARY KEY,
    Match_Id NUMBER,
    Team1 VARCHAR2(20),
    Team2 VARCHAR2(20),
    Ground VARCHAR2(20),
    Play_Date DATE,
    Winner VARCHAR2(20)
);
```

### Player Table

```sql
CREATE TABLE Player (
    SLNO NUMBER PRIMARY KEY,
    Player_Id NUMBER,
    Lname VARCHAR2(20),
    Fname VARCHAR2(20),
    Country VARCHAR2(20),
    Yborn NUMBER,
    Bplace VARCHAR2(20),
    Ftest NUMBER
);
```

### Bowling Table

```sql
CREATE TABLE Bowling (
    SLNO NUMBER PRIMARY KEY,
    Match_Id NUMBER,
    Player_Id NUMBER,
    Novers NUMBER,
    Maidens NUMBER,
    Nrun_rcv NUMBER,
    Nwickets NUMBER,
    FOREIGN KEY (Match_Id) REFERENCES Match(Match_Id),
    FOREIGN KEY (Player_Id) REFERENCES Player(Player_Id)
);
```

### Batting Table

```sql
CREATE TABLE Batting (
    SLNO NUMBER PRIMARY KEY,
    Match_Id NUMBER,
    Player_Id NUMBER,
    Nrun_sc NUMBER,
    FOREIGN KEY (Match_Id) REFERENCES Match(Match_Id),
    FOREIGN KEY (Player_Id) REFERENCES Player(Player_Id)
);
```

---

## 🔹 Step 3: Insert Data

### Match

```sql
INSERT INTO Match VALUES (match_seq.NEXTVAL, 2475, 'Australia', 'India', 'Melbourne', DATE '2008-02-10', 'Team2');
INSERT INTO Match VALUES (match_seq.NEXTVAL, 2576, 'India', 'Srilanka', 'Adelaide', DATE '2008-02-19', 'Team1');
INSERT INTO Match VALUES (match_seq.NEXTVAL, 2677, 'Australia', 'India', 'Sydney', DATE '2008-03-02', 'Team1');
INSERT INTO Match VALUES (match_seq.NEXTVAL, 2778, 'Australia', 'Srilanka', 'Brisbane', DATE '2008-03-04', 'Team2');
INSERT INTO Match VALUES (match_seq.NEXTVAL, 2879, 'Srilanka', 'India', 'Colombo', DATE '2008-08-27', 'Team2');
```

### Player

```sql
INSERT INTO Player VALUES (player_seq.NEXTVAL, 49001, 'Tendulkar', 'Sachin', 'India', 1973, 'Mumbai', 1986);
INSERT INTO Player VALUES (player_seq.NEXTVAL, 49002, 'Dravid', 'Rahul', 'India', 1973, 'Indore', 1996);
INSERT INTO Player VALUES (player_seq.NEXTVAL, 59001, 'Vass', 'Chaminda', 'Srilanka', 1974, 'Mattumagala', 1994);
INSERT INTO Player VALUES (player_seq.NEXTVAL, 59002, 'Jayasuriya', 'Sanath', 'Srilanka', 1969, 'Matara', 1991);
INSERT INTO Player VALUES (player_seq.NEXTVAL, 69001, 'Lee', 'Brett', 'Australia', 1976, 'Wollongong', 1999);
INSERT INTO Player VALUES (player_seq.NEXTVAL, 69002, 'Symonds', 'Andrew', 'Australia', 1975, 'Birmingham', 2004);
```

### Bowling

```sql
INSERT INTO Bowling VALUES (bowling_seq.NEXTVAL, 2576, 59001, 8, 3, 58, 1);
INSERT INTO Bowling VALUES (bowling_seq.NEXTVAL, 2677, 69001, 10, 1, 27, 3);
INSERT INTO Bowling VALUES (bowling_seq.NEXTVAL, 2879, 49002, 7, 0, 44, 0);
INSERT INTO Bowling VALUES (bowling_seq.NEXTVAL, 2576, 49001, 3, 2, 15, 1);
INSERT INTO Bowling VALUES (bowling_seq.NEXTVAL, 2778, 59001, 7, 1, 20, 5);
```

### Batting

```sql
INSERT INTO Batting VALUES (batting_seq.NEXTVAL, 2677, 49001, 60);
INSERT INTO Batting VALUES (batting_seq.NEXTVAL, 2778, 59002, 71);
INSERT INTO Batting VALUES (batting_seq.NEXTVAL, 2879, 59001, 60);
INSERT INTO Batting VALUES (batting_seq.NEXTVAL, 2778, 69002, 17);
INSERT INTO Batting VALUES (batting_seq.NEXTVAL, 2879, 59002, 45);
INSERT INTO Batting VALUES (batting_seq.NEXTVAL, 2576, 49001, 36);
INSERT INTO Batting VALUES (batting_seq.NEXTVAL, 2475, 49002, 72);
```

---

# 🔹 Step 4: Queries

---

## Q1. Find the ground of the matches batted by a player whose Fname is starting from 'S'.

```sql
SELECT M.Ground
FROM Match M, Batting B, Player P
WHERE M.Match_Id = B.Match_Id
AND B.Player_Id = P.Player_Id
AND P.Fname LIKE 'S%';
```

---

## Q2. Find Id of player that have bowled in the match 2576 but not have batted.

```sql
SELECT DISTINCT B.Player_Id
FROM Bowling B
WHERE B.Match_Id = 2576
AND B.Player_Id NOT IN (
    SELECT Player_Id FROM Batting WHERE Match_Id = 2576
);
```

---

## Q3. Find the batting average of each Indian player along with the Player_Id.

```sql
SELECT P.Player_Id, AVG(B.Nrun_sc)
FROM Player P, Batting B
WHERE P.Player_Id = B.Player_Id
AND P.Country = 'India'
GROUP BY P.Player_Id;
```

---

## Q4. Find the name of that player who has bowled the highest number of overs and also find the ground where he has bowled.

```sql
SELECT P.Fname, P.Lname, M.Ground
FROM Player P, Bowling B, Match M
WHERE P.Player_Id = B.Player_Id
AND B.Match_Id = M.Match_Id
AND B.Novers = (SELECT MAX(Novers) FROM Bowling);
```

---

## Q5. Find the total run scored by a player who played the First Test in 1991.

```sql
SELECT SUM(B.Nrun_sc)
FROM Batting B, Player P
WHERE B.Player_Id = P.Player_Id
AND P.Ftest = 1991;
```

---

## Q6. Find the name and the number of wickets taken by the youngest player in the database.

```sql
SELECT P.Fname, P.Lname, SUM(B.Nwickets)
FROM Player P, Bowling B
WHERE P.Player_Id = B.Player_Id
AND P.Yborn = (SELECT MAX(Yborn) FROM Player)
GROUP BY P.Fname, P.Lname;
```

---

## Q7. Find the names of the players who batted in only one match.

```sql
SELECT P.Fname, P.Lname
FROM Player P, Batting B
WHERE P.Player_Id = B.Player_Id
GROUP BY P.Player_Id, P.Fname, P.Lname
HAVING COUNT(DISTINCT B.Match_Id) = 1;
```

---

## Q8. Find the name of the player who has taken the highest wickets in a particular match and also find the ground where the player has taken the wickets.

```sql
SELECT P.Fname, P.Lname, M.Ground
FROM Player P, Bowling B, Match M
WHERE P.Player_Id = B.Player_Id
AND B.Match_Id = M.Match_Id
AND B.Nwickets = (SELECT MAX(Nwickets) FROM Bowling);
```

---

## Q9. Find the ground where Sachin Tendulkar has scored his highest run.

```sql
SELECT M.Ground
FROM Match M, Batting B, Player P
WHERE M.Match_Id = B.Match_Id
AND B.Player_Id = P.Player_Id
AND P.Fname = 'Sachin'
AND P.Lname = 'Tendulkar'
AND B.Nrun_sc = (
    SELECT MAX(B2.Nrun_sc)
    FROM Batting B2
    WHERE B2.Player_Id = P.Player_Id
);
```

---

## Q10. Find out the name of a SriLankan bowler who has delivered at least 2 maiden overs.

```sql
SELECT P.Fname, P.Lname
FROM Player P, Bowling B
WHERE P.Player_Id = B.Player_Id
AND P.Country = 'Srilanka'
AND B.Maidens >= 2;
```

---

## Q11. Find the Number of wickets of that player whose Birth place is in Mattumagala.

```sql
SELECT SUM(B.Nwickets)
FROM Player P, Bowling B
WHERE P.Player_Id = B.Player_Id
AND P.Bplace = 'Mattumagala';
```

---

## Q12. Find the names of the players who played in more than one matches.

```sql
SELECT P.Fname, P.Lname
FROM Player P, Batting B
WHERE P.Player_Id = B.Player_Id
GROUP BY P.Player_Id, P.Fname, P.Lname
HAVING COUNT(DISTINCT B.Match_Id) > 1;
```
