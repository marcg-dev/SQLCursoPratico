## Chapter 6 - Basic query in the table

In this chapter we will do some table query exercises.

The command used for query is: `SELECT`. Behind it there are a lot of possibilities, from simply extracting the contents of all rows and columns from a table, to joining several tables, to calculating, grouping, sorting, and filtering rows and columns.

---

If you need to consult how to write the syntax, we have some notes for consultation in case of doubt: [Notes](../notes/SqlBasic.md)

Let's go to the exercises. :nerd_face:

---

### Proposed exercises

#### 1.
**List all fields and rows from the BAIRRO table.**

##### REPLY
```
SELECT * FROM BAIRRO;
```

&#xa0;

#### 2.
**List all rows and fields: CDCOMPRADOR, NMCOMPRADOR and EMAIL from the COMPRADOR table.**

##### REPLY
```
SELECT CDCOMPRADOR, NMCOMPRADOR, EMAIL
	FROM COMPRADOR;
```

&#xa0;

#### 3.
**List all rows and fields: CDVENDEDOR, NMVENDEDOR and EMAIL from the VENDEDOR table in alphabetical order.**

##### REPLY
```
SELECT CDVENDEDOR, NMVENDEDOR, EMAIL
	FROM VENDEDOR
	ORDER BY NMVENDEDOR;
```

&#xa0;

#### 4.
**Repeat the previous command in descending alphabetical order.**

##### REPLY
```
SELECT CDVENDEDOR, NMVENDEDOR, EMAIL
	FROM VENDEDOR
	ORDER BY NMVENDEDOR DESC;
```

&#xa0;

#### 5.
**List the rows from the BAIRRO table that have SGESTADO = SP.**

##### REPLY
```
SELECT * FROM BAIRRO
	WHERE SGESTADO = 'SP';
```

&#xa0;

#### 6.
**List the rows with the columns CDIMOVEL, CDVENDEDOR and VLPRECO from the IMOVEL table, which have CDVENDEDOR = 2.**

##### REPLY
```
SELECT CDIMOVEL, CDVENDEDOR, VLPRECO
	FROM IMOVEL
	WHERE CDVENDEDOR = 2;
```

&#xa0;

#### 7.
**List the columns CDIMOVEL, CDVENDEDOR, VLPRECO, SGESTADO from the IMOVEL table, whose value in the column VLPRECO is less than 150 thousand and the column SGESTADO is equal to RJ.**

##### REPLY
```
SELECT CDIMOVEL, CDVENDEDOR, VLPRECO, SGESTADO
	FROM IMOVEL
    WHERE VLPRECO < 150000 AND SGESTADO = 'RJ';
```

&#xa0;

#### 8.
**List the columns CDIMOVEL, CDVENDEDOR, VLPRECO and SGESTADO from the IMOVEL table, whose column VLPRECO is less than 150 thousand, or the column CDVENDEDOR is equal to 1.**

##### REPLY
```
SELECT CDIMOVEL, CDVENDEDOR, VLPRECO, SGESTADO
	FROM IMOVEL
    WHERE VLPRECO < 150000 OR CDVENDEDOR = 1;
```

&#xa0;

#### 9.
**List the columns CDIMOVEL, CDVENDEDOR, VLPRECO and SGESTADO from the IMOVEL table, whose column VLPRECO is less than 150 thousand and the column CDVENDEDOR is not 2.**

##### REPLY
```
SELECT CDIMOVEL, CDVENDEDOR, VLPRECO, SGESTADO
	FROM IMOVEL
    WHERE VLPRECO < 150000 AND CDVENDEDOR != 2;
```

&#xa0;

#### 10.
**List the columns CDCOMPRADOR, NMCOMPRADOR, NMENDERECO and SGESTADO from the table COMPPRADOR, which has the value of the column SGESTADO null.**

##### REPLY
```
SELECT CDCOMPRADOR, NMCOMPRADOR, NMENDERECO, SGESTADO
    FROM COMPRADOR
    WHERE SGESTADO IS NULL;
```

&#xa0;

#### 11.
**List the columns CDCOMPRADOR, NMCOMPRADOR, NMENDERECO, SGESTADO from the COMPPRADOR table, where the column SGESTADO is not null.**

##### REPLY
```
SELECT CDCOMPRADOR, NMCOMPRADOR, NMENDERECO, SGESTADO
    FROM COMPRADOR
    WHERE SGESTADO IS NOT NULL;
```

&#xa0;

#### 12.
**List all rows in the OFFER table whose value in the VLOFERTA column is between 100 thousand and 150 thousand.**

##### REPLY
```
SELECT * FROM OFERTA
	WHERE VLOFERTA BETWEEN 100000 AND 150000;
```

&#xa0;

#### 13.
**List all rows in the OFFER table whose DTOFERTA column is between '02/02/01' and '02/03/01'.**

##### REPLY
```
SELECT * FROM OFERTA
	WHERE DTOFERTA BETWEEN '2002-02-01' AND '2002-03-01';
```

&#xa0;

#### 14.
**List all rows in the VENDEDOR table that have the column NMVENDEDOR starting with the letter M.**

##### REPLY
```
SELECT * FROM VENDEDOR
	WHERE NMVENDEDOR LIKE 'M%';
```

&#xa0;

#### 15.
**List all rows in the VENDEDOR table that have the letter A in the second position of the NMVENDEDOR column.**

##### REPLY
```
SELECT * FROM VENDEDOR
	WHERE NMVENDEDOR LIKE '_A%';
```

&#xa0;

#### 16.
**List all rows in the COMPRADOR table that have the letter U in any position of the NMENDERECO column.**

##### REPLY
```
SELECT * FROM COMPRADOR
	WHERE NMENDERECO LIKE '%U%';
```

&#xa0;

#### 17.
**List all rows in the OFERTA table whose value in the CDIMOVEL column is equal to 1 or 2.**

##### REPLY
```
SELECT * FROM OFERTA
	WHERE CDIMOVEL IN (1, 2);
```

&#xa0;

#### 18.
**List all rows in the IMOVEL table whose CDIMOVEL is equal to 2 or 3 in alphabetical order by column NMENDERECO.**

##### REPLY
```
SELECT * FROM IMOVEL
	WHERE CDIMOVEL IN (2, 3)
    ORDER BY NMENDERECO;
```

&#xa0;

#### 19.
**List all rows in the OFFER table whose CDIMOVEL is equal to 2 or 3 and the VLOFERTA column is greater than 140 thousand, in descending order by the DTOFERTA column.**

##### REPLY
```
SELECT * FROM OFERTA
	WHERE CDIMOVEL IN (2, 3) AND VLOFERTA > 140000
    ORDER BY DTOFERTA DESC;
```

&#xa0;

#### 20.
**List all the rows of the IMOVEL table, whose value in the VLPRECO column is between 110,000 and 200,000 or the CDVENDEDOR column is equal to 1, and organize the ordering by the NRAREAUTIL column.**

##### REPLY
```
SELECT * FROM IMOVEL
	WHERE VLPRECO BETWEEN 110000 AND 200000 OR CDVENDEDOR = 1
    ORDER BY NRAREAUTIL;
```
