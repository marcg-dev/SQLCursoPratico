# Annotations

#### `DATA DEFINITION`
- INT = Integer positive or negative number;
- SMALLINT = Same as INT but takes up less space;
- NUMERIC = Positive or negative floating point number;
- DECIMAL = Similar to NUMERIC with high precision;
- REAL = Floating point number with low precision, can be rounded;
- DOUBLE PRECISION = Double-precision floating point number;
- FLOAT = Floating point number that we set the precision level;
- BIT = A fixed number of bits. If the number is not indicated the default is 1;
- BIT VARYING = Same as BIT, allowing to store larger values;
- DATE = Dates;
- TIME = Time;
- TIMESTAMP = Date and time;
- CHAR = Character strings (letters, symbols, numbers), with fixed length;
- VARCHAR = Strings, but with variable length;
- INTERVAL = Date and time range.

---

#### `DEFAULT`
It is used to assign a default content to a table column whenever a new row is added to the table
```
columnName columnDataType DEFAULT value,
```

Example:
```
AMOUNT INTEGER DEFAULT 1,
```

---

#### `NOT NULL`
Indicates that the content of a column cannot be Null.
```
columnName columnDataType NOT NULL,
```

Example:
```
CPF DECIMAL(11) NOT NULL,
```

---

#### `UNIQUE`
Indica que não poderá haver repeticão no conteúdo da coluna.
```
columnName columnDataType UNIQUE,
```

Example:
```
CPF NUMERIC(11) UNIQUE,
```

---

#### `CHECK`
An expression of possible values for the contents of a column. When creating a column, we can specify which values can be used to fill the column.
```
columnName columnDataType CHECK (UPPER(columnName) = 'value' OR UPPER(columnName) = 'value'),
```

Example:
```
GENDER CHAR(1) CHECK (UPPER(GENDER) = 'M' OR UPPER(GENDER) = 'W'),
```

---

#### `ASSERTIVES`
Establishes constraints on the database based on data from one or more tables.
```
CREATE ASSERTION name
	CHECK (kogicExpression);
```

Example:
```
CREATE ASSERTION CD
	CHECK (EXISTS SELECT CODE_CD FROM CD);
```

---

#### `CREATING TABLES`
```
CREATE TABLE tableName (
	columnName columnDataType columnRules,
	tableRules
);
```

Example:
```
CREATE TABLE CD (
    CODE_CD INTEGER NOT NULL,
    CODE_RECORDER INTERGER NULL,
    NAME_CD VARCHAR(60) NULL,
    PRICE_SALE DEDCIMAL(16,2) NULL,
    RELEASE_DATE TIMESTAMP DEFAULT SYSDATE,
	PRIMARY KEY (CODE_CD),
	FOREING KEY (CODE_RECORDER)
	REFERENCES RECORDER (CODE_RECORDER),
	CHECK (PRICE_SALE > 0)
);
```

---

#### `CHANGING TABLES`
```
ALTER TABLE tableName
	ADD/MODIFY columnName columnDataType columnRules

```

Example:
```
ALTER TABLE CD
	ADD NAME_CD VARCHAR(70) UNIQUE

---

ALTER TABLE CD
	MODIFY NAME_CD VARCHAR(60)

---

ALTER TABLE CD
	ADD PRIMARY KEY (CODE_RECORDER)
```

---

#### `EXCLUDING`

```
DROP TABLE tableName

---

DROP INDEX nameIndex

---

ALTER TABLE tableName
	DELETE element
;

---

DELETE FROM tableName
	WHERE condition
;
```

Example:
```
DROP TABLE CD

---

DROP INDEX xNameCD

---

ALTER TABLE CD
	DELETE PRICE_SALE

---

ALTER TABLE CD
	DELETE PRIMARY KEY

---

DELETE FROM CD
	WHERE CODE_CD = 1;

```

---

#### `CHANGE NAME OF ELEMENTS`
```
ALTER TABLE tableName
	RENAME newTableName

---

ALTER TABLE tableName
	RENAME oldColumnName TO newColumnName
```

Example:
```
ALTER TABLE CD
	RENAME CDS

---

ALTER TABLE CD
	RENAME CODE_CD TO C_CD

```
---

#### `INDEX CREATION`
The index serves to provide quick access to table rows.

The creation of indexes on the table has an enormous advantage when well directed, but it can cause enormous problems if applied without criteria.

```
CREATE UNIQUE INDEX nameIndex ON tableName
	(columnName ASC/DESC);
```

Exemplo:
```
CREATE INDEX xNameCD
	ON CD (NAME_CD)

---

CREATE INDEX xNameCD
	ON CD (NAME_CD ASC)

---

CREATE UNIQUE INDEX xNameCD
	ON CD (NAME_CD DESC)

```

#### `ADD ROWS IN THE TABLE`
```
INSERT INTO tableName (columnName, columnName)
	VALUES('value', value);
```

Exemplo:
```
INSERT INTO CD (CODE_CD, CODE_RECORDER, NAME_CD, PRICE_SALE, RELEASE_DATE)
	VALUES (1, 4, 'Tempo Perdido', 15, '2018-12-03')
```

---

#### `DATA UPDATE`
```
UPDATE tableName
	SET columnName = value
	WHERE columnName = value;
```

Exemplo:
```
UPDATE CD
	SET PRICE_SALE = 15
	WHERE CODE_CD = 1;

---

UPDATE CD
	SET PRICE_SALE = 15
	WHERE CODE_CD = 1 AND CODE_RECORDER = 1;

---

UPDATE CD
	SET PRICE_SALE = PRICE_SALE * 1.05;

---

UPDATE CD
	SET NAME_CD 

---

UPDATE CD
	SET NAME_CD = 'Tempo Perdido',
	RELEASE_DATE = '2018-12-04'
	WHERE CODE_CD = 1;

```