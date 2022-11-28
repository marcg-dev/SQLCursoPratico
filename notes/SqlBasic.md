# Basic SQL Annotations

#### `OPERATORS`

**Relational**
- `=` SAME
- `<` NETHER THAN
- `<=` NETHER OR SAME
- `>` UPPER THAN
- `>=` UPPER OR SAME
- `!= or <>` DIFFERENT
  
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

```sql
SELECT DISTINCT columnName, columnName2
    FROM tableName
    WHERE condition
    ORDER BY columnName;
```

Example:
```sql
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

```sql
SELECT columnName, columnName2, columnName3 OPERATOR Value
    FROM tableName
```

Example:
```sql
SELECT NAME_CD, PRICE_CD * 1.05
    FROM CD;
```

---


#### `POSITION / INSTR`
Returns the position of the search string in the source string.

Depending on the database, we can find the two types mentioned below.

```sql
SELECT POSITION('destino' IN 'origem') columnName FROM DUAL;

---

SELECT INST('origem' IN 'destino') columnName FROM DUAL;
```

Example:
```sql
SELECT POSITION('Ru' IN 'Renato Russo') SEARCH FROM DUAL;

---

SELECT INST('Renato Russo' IN 'Ru') SEARCH FROM DUAL;
```

---

#### `CHARACTER_LENGTH / LENGTH`
Returns the number of characters contained in a string.

Depending on the database, we can find the two types mentioned below.

```sql
SELECT CHARACTER_LENGTH('string') columnName FROM DUAL;

---

SELECT LENGTH( 'string' ) columnName FROM DUAL;
```

Example:
```sql
SELECT CHARACTER_LENGTH('Renato Russo') SIZE FROM DUAL;

---

SELECT LENGTH( 'Renato russo' ) SIZE FROM DUAL;
```

---

#### `PIPES ||`
To concatenate strings.

To merge two columns into one, use:

```sql
SELECT columnName || 'separator' || columnName2
    FROM tableName;
```

Example
```sql
SELECT NAME_CD || ' - ' || VLPRICE
    FROM CD;
```

---

#### `UPPER / LOWER`
Used so that all contents are converted into uppercase or lowercase characters

```sql
SELECT columnName
    FROM tableName
    WHERE UPPER( value ) LIKE 'value';
```

Example
```sql
SELECT * FROM CD
    WHERE UPPER( NAME_CD ) LIKE 'ROBERTO%';
```

---

#### `SUBSTRING`
Return a part of a string.

```sql
SELECT SUBSTRING (columnName FROM initial_position FOR number_characters) columnName, columnName2
    FROM tableName
    WHERE columnName LIKE 'value';
```

Example
```sql
SELECT SUBSTRING (NAME_CD FROM 1 FOR 3) BY, NAME_CD
    FROM CD
    WHERE NAME_CD LIKE 'R%';
```

---

#### `TRANSLATE`
Replaces some characters in a string.

```sql
SELECT TRANSLATE (columnName, 'searchValue' , 'replacementValue')
    FROM tableName
    WHERE columnName = 1;
```

Example
```sql
SELECT TRANSLATE ( UPPER (NAME_CD), 'RT', 'AB' )
    FROM CD
    WHERE NAME_CD = 1;
```

---

#### `REPLACE`
Replaces one string with another.

```sql
SELECT REPLACE (columnName, 'searchValue' , 'replacementValue')
    FROM tableName
    WHERE columnName = 1;
```

Example
```sql
SELECT REPLACE ( UPPER (NAME_CD), 'RE', 'AB' )
    FROM CD
    WHERE NAME_CD = 1;
```

---

#### `CURRENT`
Determines current system date and/or time.

Can be used with (DATE, TIME and TIMESTAMP)

```sql
SELECT * FROM tableName
    WHERE columnName = CURRENT_DATE;
```

Example
```sql
SELECT * FROM CD
    WHERE RELEASE_DATE = CURRENT_DATE;

---

SELECT CURRENT_DATE, RELEASE_DATE,
    CURRENT_DATE - RELEASE_DATE DIFFERENCE
    FROM CD
```

---

#### `DATE MANIPULATION`
Expressions that include INTERVAL, specify which type of interval you want to view the response (YEAR, MONTH, DAY).

Examples
```sql
-- Ascending 7 days
SELECT RELEASE_DATE + 7 FROM CD;
```

```sql
-- Ascending 7 days
SELECT RELEASE_DATE + INTERVAL '7' DAY FROM CD;
```

```sql
-- Subtract 2 months
SELECT RELEASE_DATE - INTERVAL '2' MONTH FROM CD;
```

```sql
-- Extract and return the value
SELECT EXTRACT( YEAR FROM DATE '2002-05-01' )
    FROM DUAL;
```

---

#### `INNER JOIN or EQUI-JOIN`
It is optional to place the table ID before the column names in the field list of the SELECT statement. However, this is a best practice to make the command easier to understand.

Regular joins are called joins that have the WHERE clause joining the primary key to the foreign key of the tables affected by the SELECT command.

```sql
SELECT tableName1.columnName, tableName2.columnName2
    FROM tableName1, tableName2
    WHERE tableName1.PrimaryKey = tableName2.ForeignKey;
```

Example:
```sql
SELECT CD.CODE_CD, CD.NAME_CD, RECORDCOMPANY.NAME_RECORDCOMPANY
    FROM CD, RECORDCOMPANY
    WHERE CD.CODE_CD = RECORDCOMPANY.CODE_RECORDCOMPANY;

---

SELECT CD.CODE_CD, CD.NAME_CD, RECORDCOMPANY.NAME_RECORDCOMPANY
    FROM CD NATURAL JOIN RECORDCOMPANY

---

SELECT CD.CODE_CD, CD.NAME_CD, RECORDCOMPANY.NAME_RECORDCOMPANY
    FROM CD JOIN RECORDCOMPANY USING (CODE_RECORDCOMPANY);

---

SELECT CD.CODE_CD, CD.NAME_CD, RECORDCOMPANY.NAME_RECORDCOMPANY
    FROM CD JOIN RECORDCOMPANY
    ON CD.CODE_CD = RECORDCOMPANY.CODE_RECORDCOMPANY;
```

---

#### `NON-EQUIJOIN`

There are situations in which, even though there is no explicit relationship between table columns, there is a relationship between a column and a range of other columns in another table.

This type of relationship is not defined by an equality, but by an interval.

```sql
SELECT a.columnName, a.columnName, b.columnName
    FROM tableName1 a, tableName2 b
    WHERE a.columnName BETWEEN b.columnName AND b.columnName
```

Example:
```sql
SELECT a.NAME_CD, a.PRICE_SALE, b.CODE_CATEGORY
    FROM CD a, CD_CATEGORY b
    WHERE a.PRICE_SALE BETWEEN b.LOWEST_PRICE AND b.BIGGEST_PRICE;

```
---

#### `OUTER-JOIN`

An outer join is defined as one that includes rows in the search result even if there is no relationship between the two tables being joined.

There are three ways to perform outer join:

- **Left Outer Join:** As the name implies, the left join includes rows from the first table in the join expression.
+ **Right Outer Join:** Rows from the second table will be included in the search, even if there is no corresponding column in the first table.
- **Full Outer Join:** Performs a join regardless of whether the optional column is left or right.

*The use of `USING` is not mandatory in some databases.*

```sql
-- Left Outer Join
SELECT a.columnName, a.columnName, b.columnName, b.columnName
    FROM tableName1 a LEFT OUTER JOIN tableName2 b
    USING (columnName);

---

-- Right Outer Join
SELECT a.columnName, a.columnName, b.columnName, b.columnName
    FROM tableName1 a RIGHT OUTER JOIN tableName2 b
    USING (columnName);
---

-- Full Outer Join
SELECT a.columnName, a.columnName, b.columnName, b.columnName
    FROM tableName1 a FULL OUTER JOIN tableName2 b
    USING (columnName);
```

Example:
```sql
-- Left Outer Join
SELECT a.CODE_CD, a.NAME_CD, b.CODE_RECORDCOMPANY, b.NAME_RECORDCOMPANY
    FROM CD a LEFT OUTER JOIN RECORDCOMPANY b
    USING (CODE_RECORDCOMPANY);

---

-- Right Outer Join
SELECT a.CODE_CD, a.NAME_CD, b.CODE_RECORDCOMPANY, b.NAME_RECORDCOMPANY
    FROM CD a RIGHT OUTER JOIN RECORDCOMPANY b
    ON (a.CODE_RECORDCOMPANY = b.CODE_RECORDCOMPANY);

---

-- Full Outer Join
SELECT a.CODE_CD, a.NAME_CD, b.CODE_RECORDCOMPANY, b.NAME_RECORDCOMPANY
    FROM CD a FULL OUTER JOIN RECORDCOMPANY b;

```

Note: for Oracle database users, you can use, in addition to the SQL standard syntax, another form of Outer Union. Just put (+) in the WHERE clause next to the table whose column content can be null. In this way, to have the same result as before, the command would be used:

```sql
--ORACLE
SELECT a.CODE_CD, a.NAME_CD, b.CODE_RECORDCOMPANY, b.NAME_RECORDCOMPANY
    FROM CD a FULL OUTER JOIN RECORDCOMPANY b
    WHERE a.CODE_RECORDCOMPANY (+) b.CODE_RECORDCOMPANY;
```

---

#### `SELF JOIN`

In cases of a self-relationship, it is necessary that we search the table itself.

To do this, the table name is entered twice, but with different nicknames. From there, just put the union clause between the tables in the WHERE clause:

```sql
SELECT a.columnName, a.columnName, b.columnName
    FROM tableName1 a, tableName2 b
    WHERE a.columnName = b.columnName
```

Example:
```sql
SELECT a.CODE_CD, a.NAME_CD, a.CD_INDICATED, b.NAME_CD
    FROM CD a, CD b
    WHERE a.CD_INDICATED = b.CODE_CD
```