# 📘 Assignment 7 – PL/SQL

**Subject:** DBMS Lab
**University:** Sister Nivedita University

---

## 🔹 Q1. Largest of Two Numbers

```sql
DECLARE
    A NUMBER;
    B NUMBER;
BEGIN
    A := :A;
    B := :B;

    IF A > B THEN
        DBMS_OUTPUT.PUT_LINE(A);
    ELSE
        DBMS_OUTPUT.PUT_LINE(B);
    END IF;
END;
```

---

## 🔹 Q2. Even or Odd

```sql
DECLARE
    N NUMBER;
BEGIN
    N := :N;

    IF MOD(N, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE('EVEN');
    ELSE
        DBMS_OUTPUT.PUT_LINE('ODD');
    END IF;
END;
```

---

## 🔹 Q3. Factorial of a Number

```sql
DECLARE
    N NUMBER;
    I NUMBER;
    ANS NUMBER := 1;
BEGIN
    N := :N;

    FOR I IN 1..N LOOP
        ANS := ANS * I;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE(ANS);
END;
```

---

## 🔹 Q4. Leap Year Check

```sql
DECLARE
    Y NUMBER;
BEGIN
    Y := :Y;

    IF (MOD(Y,400)=0) OR (MOD(Y,4)=0 AND MOD(Y,100)<>0) THEN
        DBMS_OUTPUT.PUT_LINE('LEAP YEAR');
    ELSE
        DBMS_OUTPUT.PUT_LINE('NOT LEAP YEAR');
    END IF;
END;
```

---

## 🔹 Q5. Reverse a String

```sql
DECLARE
    STR VARCHAR2(50);
    REV VARCHAR2(50) := '';
    I NUMBER;
BEGIN
    STR := :STR;

    FOR I IN REVERSE 1..LENGTH(STR) LOOP
        REV := REV || SUBSTR(STR, I, 1);
    END LOOP;

    DBMS_OUTPUT.PUT_LINE(REV);
END;
```

---

## 🔹 Q6. Create CIRCLE Table & Insert Data

```sql
-- Create table
CREATE TABLE CIRCLE (
    RADIUS NUMBER(3),
    AREA NUMBER(10,3)
);

-- Insert values
DECLARE
    R NUMBER := 1;
    A NUMBER;
BEGIN
    WHILE R <= 10 LOOP
        A := 3.14 * R * R;
        INSERT INTO CIRCLE VALUES (R, A);
        R := R + 1;
    END LOOP;
END;
```

---

## 🔹 Q7. Update BOOKS_COPY Cost

```sql
DECLARE
    BNO NUMBER;
    NEWCOST NUMBER;
BEGIN
    BNO := :BNO;
    NEWCOST := :NEWCOST;

    UPDATE BOOKS_COPY
    SET COST = NEWCOST
    WHERE BOOK_NO = BNO
    AND COST < 450
    AND NEWCOST < 900;

    IF SQL%ROWCOUNT = 0 THEN
        DBMS_OUTPUT.PUT_LINE('ERROR');
    ELSE
        DBMS_OUTPUT.PUT_LINE('UPDATED');
    END IF;
END;
```

---

## 🔹 Q8. Display Member Details

```sql
DECLARE
    MEM_REC MEMBER_1003%ROWTYPE;
    ID MEMBER_1003.MEMBER_ID%TYPE;
BEGIN
    ID := :ID;

    SELECT * INTO MEM_REC
    FROM MEMBER_1003
    WHERE MEMBER_ID = ID;

    DBMS_OUTPUT.PUT_LINE('NAME: ' || MEM_REC.MEMBER_NAME);
    DBMS_OUTPUT.PUT_LINE('ADDRESS: ' || MEM_REC.MEMBER_ADDRESS);
    DBMS_OUTPUT.PUT_LINE('FEES: ' || MEM_REC.FEES_PAID);
END;
```

---

## 🔹 Q9. Remove Spaces & Count Spaces

```sql
DECLARE
    STR VARCHAR2(100);
    NEWSTR VARCHAR2(100) := '';
    COUNT_SP NUMBER := 0;
    I NUMBER;
BEGIN
    STR := :STR;

    FOR I IN 1..LENGTH(STR) LOOP
        IF SUBSTR(STR, I, 1) = ' ' THEN
            COUNT_SP := COUNT_SP + 1;
        ELSE
            NEWSTR := NEWSTR || SUBSTR(STR, I, 1);
        END IF;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE(NEWSTR);
    DBMS_OUTPUT.PUT_LINE('SPACES: ' || COUNT_SP);
END;
```

---

## 🔹 Q10. Display Each Word

```sql
DECLARE
    STR VARCHAR2(100);
    WORD VARCHAR2(50) := '';
    I NUMBER;
BEGIN
    STR := :STR;

    FOR I IN 1..LENGTH(STR) LOOP
        IF SUBSTR(STR, I, 1) = ' ' THEN
            DBMS_OUTPUT.PUT_LINE(WORD);
            WORD := '';
        ELSE
            WORD := WORD || SUBSTR(STR, I, 1);
        END IF;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE(WORD);
END;
```

---

## 🔹 Q11. Uppercase & Lowercase Member Name

```sql
DECLARE
    MEM_REC MEMBER_1003%ROWTYPE;
    ID MEMBER_1003.MEMBER_ID%TYPE;
BEGIN
    ID := :ID;

    SELECT * INTO MEM_REC
    FROM MEMBER_1003
    WHERE MEMBER_ID = ID;

    DBMS_OUTPUT.PUT_LINE(UPPER(MEM_REC.MEMBER_NAME));
    DBMS_OUTPUT.PUT_LINE(LOWER(MEM_REC.MEMBER_NAME));
END;
```

---
