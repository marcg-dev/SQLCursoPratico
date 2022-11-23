## Chapter 5 - Adding, updating, and deleting rows in tables

Now that we have the tables created, related and indexed. We enter the stage of entering and manipulating data.

In this phase of the book, the treatment of the Data Manipulation Language (DML) begins, which will only be concluded in Chapter 6.

In summary, there are three commands for inserting and modifying data in a table: `INSERT | DELETE | UPDATE`

---

If you need to consult how to write the syntax, we have some notes for consultation in case of doubt: [Notes](../notes/Concept.md#add-rows-in-the-table)

Let's go to the exercises. :nerd_face:

---

### Proposed exercises

#### 1.
**Add the lines below, in the ESTADO table:**

| SGESTADO |    NMESTADO    |
| :------: | :------------: |
|    SP    |   SÃO PAULO    |
|    RJ    | RIO DE JANEIRO |

##### REPLY
```
INSERT INTO ESTADO (SGESTADO, NMESTADO)
    VALUES('SP', 'RIO DE JANEIRO'),
    ('RJ', 'RIO DE JANEIRO');
```

&#xa0;

#### 2.
**Add the lines below, in the CIDADE table:**

| CDCIDADE |    NMCIDADE    | SGESTADO |
| :------: | :------------: | :------: |
|    1     |   SÃO PAULO    |    SP    |
|    2     |  SANTO ANDRÉ   |    SP    |
|    3     |    CAMPINAS    |    SP    |
|    1     | RIO DE JANEIRO |    RJ    |
|    2     |    NITEROI     |    RJ    |

##### REPLY
```
INSERT INTO CIDADE (CDCIDADE, NMCIDADE, SGESTADO)
    VALUES (1, 'SÃO PAULO', 'SP'),
    (2, 'SANTO ANDRÉ', 'SP'),
    (3, 'CAMPINAS', 'SP'),
    (1, 'RIO DE JANEIRO', 'RJ'),
    (2, 'NITERÓI', 'RJ');
```

&#xa0;

#### 3.
**Add the lines below, in the BAIRRO table:**

| CDBAIRRO | NMBAIRRO  | CDCIDADE | SGESTADO |
| :------: | :-------: | :------: | :------: |
|    1     |  JARDINS  |    1     |    SP    |
|    2     |  MORUMBI  |    1     |    SP    |
|    3     | AEROPORTO |    1     |    SP    |
|    1     | AEROPORTO |    1     |    RJ    |
|    2     | FLAMENGO  |    1     |    RJ    |

##### REPLY
```
INSERT INTO BAIRRO (CDBAIRRO, NMBAIRRO, CDCIDADE, SGESTADO)
    VALUES(1, 'JARDINS', 1, 'SP'),
    (2, 'MORUMBI', 1, 'SP'),
    (3, 'AEROPORTO', 1, 'SP'),
    (1, 'AEROPORTO', 1, 'RJ'),
    (2, 'FLAMENGO', 1, 'RJ');
```

&#xa0;

#### 4.
**Add the lines below, in the VENDEDOR table:**

| CDVENDEDOR |   NMVEDENDOR   |      NMENDERECO       |          EMAIL          |
| :--------: | :------------: | :-------------------: | :---------------------: |
|     1      | MARIA DA SILVA |   RUA DO GRITO, 45    |  msilva@novatec.com.br  |
|     2      | MARCOS ANDRADE |  AV. DA SAUDADE, 325  | mandrade@novatec.com.br |
|     3      | ANDRE CARDOSO  |    AV BRASIL, 401     | acardoso@novatec.com.br |
|     4      | TATIANA SOUZA  | RUA DO IMPERADOR, 778 |  tsouza@novatec.com.br  |

##### REPLY
```
INSERT INTO VENDEDOR (CDVENDEDOR, NMVENDEDOR, NMENDERECO, EMAIL)
    VALUES(1, 'MARIA DA SILVA', 'RUA DO GRITO, 45', 'msilva@novatec.com.br'),
    (2, 'MARCOS ANDRADE', 'AV. DA SAUDADE, 325', 'mandrade@novatec.com.br'),
    (3, 'ANDRE CARDOSO', 'AV. BRASIL, 401', 'acardoso@novatec.com.br'),
    (4, 'TATIANA SOUZA', 'RUA DO IMPERADOR, 778', 'tsouza@novatec.com.br');
```

&#xa0;

#### 5.
**Add the lines below, in the IMOVEL table:**

| CDIMOVEL | CDVENDEDOR | CDBAIRRO | CDCIDADE | SGESTADO |       NMENDERECO        | NRAREAUTIL | NRAREATOTAL | VLPRECO | IMOVEL_INDICADO |
| :------: | :--------: | :------: | :------: | :------: | :---------------------: | :--------: | :---------: | :-----: | :-------------: |
|    1     |     1      |    1     |    1     |    SP    |  AL TIETE, 3304 AP 101  |    250     |     400     | 180000  |      NULL       |
|    2     |     1      |    2     |    1     |    SP    |    AV MORUMBI, 2230     |    150     |     250     | 135000  |        1        |
|    3     |     2      |    1     |    1     |    RJ    | R GAL OSORIO, 445 AP 34 |    250     |     400     | 185000  |        2        |
|    4     |     2      |    2     |    1     |    RJ    |    R D PEDRO I, 882     |    120     |     200     | 110000  |        1        |
|    5     |     3      |    3     |    1     |    SP    |  AV RUBEM BERTA, 2355   |    110     |     200     |  95000  |        4        |
|    6     |     4      |    1     |    1     |    RJ    |  R GETULIO VARGAS, 552  |    200     |     300     |  99000  |        5        |

##### REPLY
```
INSERT INTO IMOVEL (CDIMOVEL, CDVENDEDOR, CDBAIRRO, CDCIDADE, SGESTADO, NMENDERECO, NRAREAUTIL, NRAREATOTAL, VLPRECO, IMOVEL_INDICADO)
    VALUES(1, 1, 1, 1, 'SP', 'AL TIETE, 3304 AP 101', 250, 400, 180000, NULL),
    (2, 1, 2, 1, 'SP', 'AV MORUMBI, 2230', 150, 250, 135000, 1 ),
    (3, 2, 1, 1, 'RJ', 'R GAL OSORIO, 445 AP 34', 250, 400, 185000, 2),
    (4, 2, 2, 1, 'RJ', 'R D PEDRO I, 882', 120, 200, 110000, 1),
    (5, 3, 3, 1, 'SP', 'AV RUBEM BERTA, 2355', 110, 200, 95000, 4),
    (6, 4, 1, 1, 'RJ', 'R GETULIO VARGAS, 552', 200, 300, 99000, 5);
```

&#xa0;

#### 6.
**Add the lines below, in the COMPRADOR table:**

| CDVENDEDOR |   NMCOMPRADOR    |      NMENDERECO      |          EMAIL          |
| :--------: | :--------------: | :------------------: | :---------------------: |
|     1      | EMMANUEL ANTUNES |   RUA SARAIVA, 452   | eantunes@novatec.com.br |
|     2      |  JOANA PEREIRA   |   AV PORTUGAL, 52    | jpereira@novatec.com.br |
|     3      | RONALDO CAMPELO  | R ESTADO UNIDOS, 790 | rcampelo@novatec.com.br |
|     4      | MANFRED AUGUSTO  |    AV BRASIL, 351    | maugusto@novatec.com.br |

##### REPLY
```
INSERT INTO COMPRADOR (CDCOMPRADOR, NMCOMPRADOR, NMENDERECO, EMAIL)
    VALUES(1, 'EMMANUEL ANTUNES', 'R SARAIVA, 452', 'eantunes@novatec.com.br'),
    (2, 'JOANA PEREIRA', 'AV PORTUGAL, 52', 'jpereira@novatec.com.br'),
    (3, 'RONALDO CAMPELO', 'R ESTADOS UNIDOS, 790', 'rcampelo@novatec.com.br'),
    (4, 'MANFRED AUGUSTO', 'AV BRASIL, 351', 'maugusto@novatec.com.br');
```

&#xa0;

#### 7.
**Add the lines below, in the OFERTA table:**

| CDVENDEDOR | CDIMOVEL | VLOFERTA | DTOFERTA |
| :--------: | :------: | :------: | :------: |
|     1      |    1     |  170000  | 10/01/02 |
|     1      |    3     |  180000  | 10/01/02 |
|     2      |    2     |  135000  | 15/02/02 |
|     2      |    4     |  100000  | 15/02/02 |
|     3      |    1     |  160000  | 05/01/02 |
|     3      |    2     |  140000  | 20/02/02 |

##### REPLY
```
INSERT INTO OFERTA (CDCOMPRADOR, CDIMOVEL, VLOFERTA, DTOFERTA)
    VALUES (1, 1, 170000, '2002-01-10'),
    (1, 3, 180000, '2002-01-10'),
    (2, 2, 135000, '2002-02-15'),
    (2, 4, 100000, '2002-02-15'),
    (3, 1, 160000, '2002-01-05'),
    (3, 2, 140000, '2002-02-20');
```

&#xa0;

#### 8.
**Increase the sales price of the table: IMOVEL by 10%:**

##### REPLY
```
UPDATE IMOVEL
	SET VLPRECO = VLPRECO * 1.10;
```

&#xa0;

#### 9.
**Lower the selling price of the table IMOVEL, from seller 1 by 5%**

##### REPLY
```
UPDATE IMOVEL
	SET VLPRECO = VLPRECO * 0.95
	WHERE CDVENDEDOR = 1;
```

&#xa0;

#### 10.
**Increase the VLOFERTA column of the OFERTA table by 5%, of those who have CDCOMPRADOR = 2.**

##### REPLY
```
UPDATE OFERTA
	SET VLOFERTA = VLOFERTA * 1.05
	WHERE CDCOMPRADOR = 2;
```

&#xa0;

#### 11.
**Change the column NMENDERECO, to `R ANANÁS, 45` and SGESTADO to `RJ` in the COMPRADOR table, in the row that has CDCOMPRADOR = 3.**

##### REPLY
```
UPDATE COMPRADOR
	SET NMENDERECO = 'R ANANÁS, 45', SGESTADO = 'RJ'
	WHERE CDCOMPRADOR = 3;
```

&#xa0;

#### 12.
**Change the VLOFERTA column of the OFERTA table, which has CDCOMPRADOR = 2 AND CDIMOVEL = 4 to 101,000.**

##### REPLY
```
UPDATE OFERTA
    SET VLOFERTA = 101,000
    WHERE CDCOMPRADOR = 2 AND CDIMOVEL = 4;
```

&#xa0;

#### 13.
**Delete the row that has CDCOMPRADOR = 3 and CDIMOVEL = 1 in the OFERTA table.**

##### REPLY
```
DELETE FROM OFERTA
    WHERE CDCOMPRADOR = 3 AND CDIMOVEL = 1;
```

&#xa0;

#### 14.
**Delete in the CIDADE table the row that has CDCIDADE = 3 and SGESTADO = SP.**

##### REPLY
```
DELETE FROM CIDADE
    WHERE CDCIDADE = 3 AND SGESTADO = 'SP';
```

&#xa0;

#### 15.
**Add the lines below, in the FAIXA_IMOVEL table:**

| CDFAIXA | NMFAIXA | VLMINIMO | VLMAXIMO |
| :-----: | :-----: | :------: | :------: |
|    1    |  BAIXO  |    0     |  105000  |
|    2    |  MÉDIO  |  105001  |  180000  |
|    3    |  ALTO   |  180001  |  999999  |

##### REPLY
```
INSERT INTO FAIXA_IMOVEL(CDFAIXA, NMFAIXA, VLMINIMO, VLMAXIMO)
    VALUES(1, 'BAIXO', 0, 105000),
    (2, 'MÉDIO', 105001, 180000),
    (3, 'ALTO', 180001, 999999);
```

&#xa0;

---

`NOTE:`

The answers to the exercises (1, 2, 3, 4, 5, 6, 7 and 15) in Chapter 5 are also available in the file: [ImovelNet.sql](.../downloads/ImovelNet.sql).

**In all subsequent exercises, this data structure is used. Until the end of the book.**