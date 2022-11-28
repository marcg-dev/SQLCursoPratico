## Chapter 7 - Usual calculations and functions

Continuing with the queries, this chapter brings a very important use of SQL. Calculations and totals of unit values.

In addition to using some character manipulation functions.

Let's go to the exercises. :nerd_face:

---

### Proposed exercises

#### 1.
**Write a search that shows the current date.**

##### REPLY
```sql
SELECT CURRENT_DATE
	FROM DUAL;
```

&#xa0;

#### 2.
**Write a search that shows the columns CDIMOVEL, VLPRECO and VLPRECO with a 10% increase in the IMOVEL table.**

##### REPLY
```sql
SELECT CDIMOVEL, VLPRECO, VLPRECO * 1.10 COM_10
	FROM IMOVEL;
```

&#xa0;

#### 3.
**Write a query like the previous one, but add a column showing the difference between VLPRECO and VLPRECO with a 10% increase.**

##### REPLY
```sql
SELECT CDIMOVEL, VLPRECO, VLPRECO * 1.10 COM_10, (VLPRECO * 1.10) - VLPRECO DIFERENCA
	FROM IMOVEL;
```

&#xa0;

#### 4.
**Write a query that shows the NMVENDEDOR column in uppercase and the EMAIL column in lowercase.**

##### REPLY
```sql
 SELECT UPPER(NMVENDEDOR), LOWER(EMAIL)
    FROM VENDEDOR;
```

&#xa0;

#### 5.
**Write a query that shows NMCOMPRADOR and CDCIDADE in a single column and separated by a hyphen.**

##### REPLY
```sql
SELECT NMCOMPRADOR || ' - ' || NMCIDADE
    FROM COMPRADOR;
```

&#xa0;

#### 6.
**Write a query that returns all rows from the COMPRADOR table that have the letter A in column NMCOMPRADOR.**

##### REPLY
```sql
SELECT * FROM COMPRADOR
    WHERE NMCOMPRADOR LIKE '%A%';
```

&#xa0;

#### 7.
**Write a query that shows the first letter of the NMCOMPRADOR column, followed by the NMBAIRRO column.**

##### REPLY
```sql
SELECT SUBSTRING(NMCOMPRADOR FROM 1 FOR 1) COMPRADOR, NMBAIRRO
    FROM COMPRADOR;
```

&#xa0;

#### 8.
**Write a search that shows the CDIMOVEL and the number of days between the current system date and the DTOFERTA column.**

##### REPLY
```sql
SELECT CDIMOVEL, CURRENT_DATE - DTOFERTA DIFERENCA
    FROM OFERTA;
```

&#xa0;

#### 9.
**Write a query that displays the CDIMOVEL, the DTLANCTO and the number of days between the current system date and the DTLANCTO column.**

##### REPLY
```sql
SELECT CDIMOVEL, DTLANCTO, CURRENT_DATE - DTLANCTO DIFERENCA
    FROM IMOVEL
    WHERE DTLANCTO IS NOT NULL;
```

&#xa0;

#### 10.
**Write a search like the previous one and show a column with 15 days added to DTLANCTO.**

##### REPLY
```sql
SELECT CDIMOVEL, DTLANCTO, CURRENT_DATE - DTLANCTO 'DIAS APÓS LANCAMENTO', DTLANCTO + INTERVAL '15' DAY '15 DIAS APOS A DTLANCTO'
    FROM IMOVEL
    WHERE DTLANCTO IS NOT NULL;
```
