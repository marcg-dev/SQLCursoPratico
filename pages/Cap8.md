## Chapter 8 - Search in multiple tables

So far we've seen how to perform lookups on a single table. However, in the assembly of our Data Model we always have several tables. So throughout this chapter, we'll introduce the various ways to join columns and how to implement them in SQL.

As previously seen, the union between the Entities of our Logical Model takes place through primary and foreign keys. These keys are, in the Physical representation of the Model, the columns that the tables have in common.

Let's go to the exercises. :nerd_face:

---

### Proposed exercises

#### 1.
**Do a search that shows CDIMOVEL, CDVENDEDOR, NMVENDEDOR and SGESTADO.**

##### REPLY
```sql
SELECT imv.CDIMOVEL, imv.CDVENDEDOR, vnd.NMVENDEDOR, imv.SGESTADO
    FROM IMOVEL imv JOIN VENDEDOR vnd USING (CDVENDEDOR);
```

&#xa0;

#### 2.
**Do a search that shows CDCOMPRADOR, NMCOMPRADOR, CDIMOVEL and VLOFERTA.**

##### REPLY
```sql
SELECT oft.CDCOMPRADOR, cmp.NMCOMPRADOR, oft.CDIMOVEL, oft.VLOFERTA
    FROM OFERTA oft NATURAL JOIN COMPRADOR cmp;
```
&#xa0;

#### 3.
**Do a search that shows CDIMOVEL, VLPRECO and NMBAIRRO, whose CDVENDEDOR code is 3.**

##### REPLY
```sql
SELECT imv.CDIMOVEL, imv.VLPRECO, bar.NMBAIRRO
    FROM IMOVEL imv JOIN BAIRRO bar USING(CDBAIRRO)
    WHERE CDVENDEDOR IN (3);
```

&#xa0;

#### 4.
**Do a search that shows all rows from the IMOVEL table that are in the OFERTA table.**

##### REPLY
```sql
SELECT DISTINCT imv.CDIMOVEL, imv.NMENDERECO, imv.NRAREAUTIL, imv.NRAREATOTAL, imv.VLPRECO 
	FROM IMOVEL imv NATURAL JOIN OFERTA oft
	WHERE imv.CDIMOVEL IN (oft.CDIMOVEL);
```

&#xa0;

#### 5.
**Do a search that shows all the rows of the IMOVEL table together with the OFERTA table, even if there is no OFERTA registered for the IMOVEL.**

##### REPLY
```sql
SELECT imv.CDIMOVEL, imv.NMENDERECO, imv.NRAREAUTIL, imv.NRAREATOTAL, imv.VLPRECO, oft.VLOFERTA
	FROM IMOVEL imv LEFT OUTER JOIN OFERTA oft
    USING (CDIMOVEL);
```

&#xa0;

#### 6.
**Do a search that shows all rows in the COMPRADOR table and the respective OFERTA made by them.**

##### REPLY
```sql
SELECT cmp.CDCOMPRADOR, cmp.NMCOMPRADOR, cmp.EMAIL, oft.VLOFERTA
	FROM COMPRADOR cmp NATURAL JOIN OFERTA oft;
```

&#xa0;

#### 7.
**Carry out the same search, but adding the COMPRADOR who have not yet made an OFERTA for the IMOVEL.**

##### REPLY
```sql
SELECT cmp.CDCOMPRADOR, cmp.NMCOMPRADOR, cmp.EMAIL, oft.VLOFERTA
	FROM COMPRADOR cmp LEFT OUTER JOIN OFERTA oft
    USING (CDCOMPRADOR);
```

&#xa0;

#### 8.
**Do a search that shows the NMENDERECO column of the IMOVEL table and the NMENDERECO column of the IMOVEL_INDICADO column.**

##### REPLY
```sql
SELECT imv1.CDIMOVEL, vnd.NMVENDEDOR, imv1.NMENDERECO, imv1.IMOVEL_INDICADO, imv2.NMENDERECO, vnd.NMVENDEDOR,
	FROM IMOVEL imv1, IMOVEL imv2, VENDEDOR vnd
    WHERE imv1.IMOVEL_INDICADO = imv2.CDIMOVEL
```

&#xa0;

#### 9.
**Add to the previous search the NMVENDEDOR column, both from the IMOVEL and IMOVEL_INDICADO tables.**

##### REPLY
```sql
SELECT imv1.CDIMOVEL, imv1.NMENDERECO, vnd1.NMVENDEDOR, imv1.IMOVEL_INDICADO, imv2.NMENDERECO, vnd2.NMVENDEDOR
	FROM IMOVEL imv1, IMOVEL imv2, VENDEDOR vnd1, VENDEDOR vnd2
    WHERE imv1.IMOVEL_INDICADO = imv2.CDIMOVEL
    AND imv1.CDVENDEDOR = vnd1.CDVENDEDOR
    and imv2.CDVENDEDOR = vnd2.CDVENDEDOR
    ORDER BY CDIMOVEL;
```

&#xa0;

#### 10.
**Do a search that shows the column NMENDERECO, CDBAIRRO and FAIXA_IMOVEL.**

##### REPLY
```sql
SELECT CDIMOVEL, NMENDERECO, NMBAIRRO, NMFAIXA
	FROM IMOVEL imv NATURAL JOIN BAIRRO bro, FAIXA_IMOVEL fimv
    WHERE imv.VLPRECO BETWEEN fimv.VLMINIMO AND fimv.VLMAXIMO
    ORDER BY CDIMOVEL;
```

&#xa0;
