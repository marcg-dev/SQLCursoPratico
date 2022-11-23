# Basic SQL Annotations

#### `OPERATORS`

**Relational**
- `=` SAME
- `<` NETHER THAN
- `<=` NETHER OR SAME
- `>` UPPER THAN
- `>=` UPPER OR SAME
- `!= OU <>` DIFFERENT
  
**Logical**
- `AND` = AND
- `OR` = OR
- `NOT or !` = NOT / NEGATION

**Special**
- `IS NULL` = NULL FIELDS
- `IS NOT NULL` = NON-NULL FIELDS
- `BETWEEN` = INTERVAL
- `LIKE 'A%'` = BEGIN WITH THE LETTER A
- `LIKE '%A'` = ENDS WITH THE LETTER A
- `LIKE '%A%'` = HAVE LETTER A IN ANY POSITION
- `LIKE 'A_'` = TWO-CHARACTER STRING THAT STARTS WITH THE LETTER A, FOLLOWED BY ANY OTHER LETTER
- `LIKE '_A'` = TWO-CHARACTER STRING, STARTING WITH ANY CHARACTER AND THE SECOND CHARACTER BEING A
- `LIKE '_A_'` = THREE-CHARACTER STRING WITH THE SECOND LETTER A
- `LIKE '%A_'` = LETTER A IN THE PENULTIMATE POSITION
- `LIKE '_A%'` = LETTER A IN THE SECOND POSITION
- `IN` = COMPARISON WITH VALUE SET

**Arithmetic**
- `+` = ADDITION
- `-` = SUBTRACTION
- `*` = MUTIPLICATION
- `/` = DIVISION

---

#### `SELECT`
We can use `DISTINCT` only if the objective is: not to show repeated values. If you don't have `DISTINCT` defined in the syntax, we will have `ALL` defined by default. Thus, all values will be displayed. Even the repeats.

```
SELECT DISTINCT columnName, columnName2
    FROM tableName
    WHERE condition
    ORDER BY columnName;
```

Example:
```
SELECT *
    FROM CD;

---

SELECT CODE_CD, NAME_CD
    FROM CD;

---

SELECT CODE_CD, NAME_CD
    FROM CD
    ORDER BY NAME_CD;

---

SELECT CODE_CD, NAME_CD
    FROM CD
    WHERE CODE_RECORDER = 1
    ORDER BY NAME_CD;

---

SELECT CODE_CD, NAME_CD, RELEASE_DATE
    FROM CD
    WHERE RELEASE_DATE BETWEEN '01-02-2021' AND '01-03-2021';

---

SELECT CODE_CD, NAME_CD
    FROM CD
    WHERE NAME_CD LIKE 'R%';

---

SELECT * FROM CD
    WHERE CODE_CD IN (1, 10, 20);
```

---

#### `CALCULATIONS`
We can do calculations directly in a database query by simply applying an arithmetic operator to columns.

The precedence of operators is the same as in mathematics, that is, multiplication and division have priority over addition and subtraction

The operation will be performed in the order in which it appears, or we can change the priority using parentheses.

```
SELECT columnName, columnName2, columnName3 OPERATOR Value
    FROM tableName
```

Example:
```
SELECT NAME_CD, PRICE_CD * 1.05
    FROM CD;
```

---


#### `POSITION / INSTR`
Returns the position of the search string in the source string.

Depending on the database, we can find the two types mentioned below.

```
SELECT POSITION('destino' IN 'origem') columnName FROM DUAL;

---

SELECT INST('origem' IN 'destino') columnName FROM DUAL;
```

Example:
```
SELECT POSITION('Ru' IN 'Renato Russo') SEARCH FROM DUAL;

---

SELECT INST('Renato Russo' IN 'Ru') SEARCH FROM DUAL;
```

---

#### `CHARACTER_LENGTH / LENGTH`
Returns the number of characters contained in a string.

Depending on the database, we can find the two types mentioned below.

```
SELECT CHARACTER_LENGTH('string') columnName FROM DUAL;

---

SELECT LENGTH( 'string' ) columnName FROM DUAL;
```

Example:
```
SELECT CHARACTER_LENGTH('Renato Russo') SIZE FROM DUAL;

---

SELECT LENGTH( 'Renato russo' ) SIZE FROM DUAL;
```

---

#### `PIPES ||`
To concatenate strings.

To merge two columns into one, use:

```
SELECT columnName || 'separator' || columnName2
 FROM tableName;
```

Example
```
SELECT NAME_CD || ' - ' || VLPRICE
    FROM CD;
```

---

#### `UPPER / LOWER`
Used so that all contents are converted into uppercase or lowercase characters

```
SELECT columnName
    FROM tableName
    WHERE UPPER( value ) LIKE 'value';
```

Example
```
SELECT * FROM CD
    WHERE UPPER( NAME_CD ) LIKE 'ROBERTO%';
```

---

#### `SUBSTRING`
Return a part of a string.

```
SELECT SUBSTRING (columnName FROM initial_position FOR number_characters) columnName, columnName2
    FROM tableName
    WHERE columnName LIKE 'value';
```

Example
```
SELECT SUBSTRING (NAME_CD FROM 1 FOR 3) BY, NAME_CD
    FROM CD
    WHERE NAME_CD LIKE 'R%';
```

---

#### `TRANSLATE`
Replaces some characters in a string.

```
SELECT TRANSLATE (columnName, 'searchValue' , 'replacementValue')
    FROM tableName
    WHERE columnName = 1;
```

Example
```
SELECT TRANSLATE ( UPPER (NAME_CD), 'RT', 'AB' )
    FROM CD
    WHERE NAME_CD = 1;
```

---

#### `REPLACE`
Replaces one string with another.

```
SELECT REPLACE (columnName, 'searchValue' , 'replacementValue')
    FROM tableName
    WHERE columnName = 1;
```

Example
```
SELECT REPLACE ( UPPER (NAME_CD), 'RE', 'AB' )
    FROM CD
    WHERE NAME_CD = 1;
```

---

#### `CURRENT`
Determines current system date and/or time.

Can be used with (DATE, TIME and TIMESTAMP)

```
SELECT * FROM tableName
    WHERE columnName = CURRENT_DATE;
```

Example
```
SELECT * FROM CD
    WHERE RELEASE_DATE = CURRENT_DATE;

---

SELECT CURRENT_DATE, RELEASE_DATE,
    CURRENT_DATE - RELEASE_DATE DIFFERENCE
    FROM CD
```

#### `DATE MANIPULATION`
Expressions that include INTERVAL, specify which type of interval you want to view the response (YEAR, MONTH, DAY).

Examples
```
// Ascending 7 days
SELECT RELEASE_DATE + 7 FROM CD;
```

```
// Ascending 7 days
SELECT RELEASE_DATE + INTERVAL '7' DAY FROM CD;
```

```
// Subtract 2 months
SELECT RELEASE_DATE - INTERVAL '2' MONTH FROM CD;
```

```
// Extract and return the value
SELECT EXTRACT( YEAR FROM DATE '2002-05-01' )
    FROM DUAL;
```