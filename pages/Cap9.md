## Chapter 8 - Group functions and groupings

Group Functions operate on sets of rows, aiming to provide a result for the group. So far the book has only covered functions that handle only one line at a time. The basic difference is that groups of lines will be used. These groups can be constituted from the entire table to subgroups of the table.

Let's go to the exercises. :nerd_face:

---

### Proposed exercises

#### 1.
**Check the highest, lowest and average value of offers in the table.**

##### REPLY
```sql
SELECT MAX(VLOFERTA), MIN(VLOFERTA), AVG(VLOFERTA)
	FROM OFERTA;
```

&#xa0;

#### 2.
**Check the standard deviation and variance of the selling price of the properties.**

##### REPLY
```sql
SELECT STDDEV(VLPRECO) DESVIO_PADRAO, VARIANCE(VLPRECO) VARIANCA
	FROM IMOVEL;
```

&#xa0;

#### 3.
**Repeat the previous command showing the result in decimal format with two places after the decimal point.**

##### REPLY
```sql
SELECT CAST(STDDEV(VLPRECO) AS DECIMAL (10,2)) DESVIO_PADRAO, CAST(VARIANCE(VLPRECO) AS DECIMAL(16,2)) VARIANCA
	FROM IMOVEL;
```

&#xa0;

#### 4.
**Show the highest, lowest, total and average sales price of the properties.**

##### REPLY
```sql
SELECT MAX(VLPRECO), MIN(VLPRECO), SUM(VLPRECO), CAST(AVG(VLPRECO) AS DECIMAL (10,2)) MEDIA_VLPRECO
	FROM IMOVEL;
```

&#xa0;

#### 5.
**Modify the previous command so that the same indexes per neighborhood are shown.**

##### REPLY
```sql
SELECT BAIRRO.NMBAIRRO, MAX(VLPRECO), MIN(VLPRECO), SUM(VLPRECO), CAST(AVG(VLPRECO) AS DECIMAL (10,2)) MEDIA_VLPRECO
	FROM IMOVEL NATURAL JOIN BAIRRO
    GROUP BY BAIRRO.NMBAIRRO;
```

&#xa0;

#### 6.
**Do a search that returns the total number of properties per seller. Present in total order of properties.**

##### REPLY
```sql
SELECT VENDEDOR.NMVENDEDOR, COUNT(*)
	FROM IMOVEL JOIN VENDEDOR USING(CDVENDEDOR)
    GROUP BY VENDEDOR.NMVENDEDOR
    ORDER BY COUNT(*);
```

&#xa0;

#### 7.
**Check the price difference between the largest and smallest property in the table.**

##### REPLY
```sql


```

&#xa0;

#### 8.
**Show the seller's code and the lowest price of his property in the register. Exclude property values below 10,000 from the search.**

##### REPLY
```sql
SELECT VENDEDOR.CDVENDEDOR, MIN(IMOVEL.VLPRECO) MENOR_VALOR
	FROM VENDEDOR JOIN IMOVEL USING(CDVENDEDOR)
    GROUP BY CDVENDEDOR
    HAVING MENOR_VALOR > 10000.00
    ORDER BY MENOR_VALOR;
```

&#xa0;

#### 9.
**Show the buyer's code and name and the average bid value and number of bids for this buyer.**

##### REPLY
```sql
SELECT COMPRADOR.CDCOMPRADOR, COMPRADOR.NMCOMPRADOR, AVG(OFERTA.VLOFERTA) MEDIA_VALOR_OFERTAS, COUNT(OFERTA.CDCOMPRADOR) QTD_OFERTAS
	FROM COMPRADOR JOIN OFERTA USING(CDCOMPRADOR)
    GROUP BY COMPRADOR.CDCOMPRADOR, COMPRADOR.NMCOMPRADOR
```

&#xa0;

#### 10.
**Run a search that returns the total offers made in the years 2000, 2001 and 2002.**

##### REPLY
```sql
SELECT EXTRACT( YEAR FROM DTOFERTA ) ANOS, COUNT(*)
	FROM OFERTA
    GROUP BY ANOS
    HAVING ANOS IN (2000, 2001, 2002)
```

&#xa0;