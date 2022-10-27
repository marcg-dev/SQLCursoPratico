## Capitulo 2 - Projetando banco de dados

Antes da criação do banco de dados ou iniciarmos a utilização dos comandos SQL. O livro aborda um assunto de extrema importancia: Planejamento de um banco de dados.

Em resumo, existem estudos que indicam que quanto maior o tempo despendido no desenho do banco de dados, menor será o tempo despendido na manutenção do modelo. Então esse desenho é de extrema importancia para a estabilidade de todo o sistema, evitando futuramente um comprometimento de todo o desenvolvimento.

Podemos comparar o planejamento do banco de dados com uma estrutura de um prédio. Se não for dado a devida atencão, o edifício irá cair.

*Conforme apresentado no livro, iremos realizar os primeiros exercícios fazendo a criacão das entidades e seus relacionamentos.*

------


### Exercícios propostos

#### 1.

> **Veja os modelos de dados a seguir. Identifique os relacionamentos entre as entidades apresentadas. Leve em consideração que o Gênero é Drama, Comédia, Aventura etc. e Categoria é a faixa de preço do filme. Em um modelo mais completo, deveria haver várias fitas para um mesmo filme, mas imagine que, nesse sistema não haja essa necessidade.**


```mermaid
erDiagram
    GENERO {
        INT CDGENERO FK
        STRING NMGENERO
    }
    FILME {
        INT CDFILME PK
        STRING NMFILME
        DECIMAL DURACAO
        STRING SINOPSE
        BLOB FOTO
        STRING STLOCADO
    }
    CATEGORIA {
        INT CDCATEGORIA PK
        STRING NMCATEGORIA
        DECIMAL VLDIARIA
    }
```

```mermaid
erDiagram
    LOCACAO {
        INT CDLOCACAO PK
        DATE DTLOCACAO
        DATE DTDEVOLUCAO
    }
    CLIENTE{
        INT CDCLIENTE PK
        STRING NMCLIENTE
        STRING NMENDERECO
        STRING TELEFONE
        NUMERIC RG
        DECIMAL CPF
    }
```

#####==Resposta==
```mermaid
erDiagram
    GENERO ||--o{ FILME : Contem
    GENERO {
        INT CDGENERO FK
        STRING NMGENERO
    }
    FILME }o--o{ LOCACAO : Esta-em
    FILME {
        INT CDFILME PK
        INT CDGENERO FK
        STRING NMFILME
        DECIMAL DURACAO
        STRING SINOPSE
        BLOB FOTO
        STRING STLOCADO
        INT CDCATEGORIA FK
    }
    CATEGORIA ||--o{ FILME : Contem
    CATEGORIA {
        INT CDCATEGORIA PK
        STRING NMCATEGORIA
        DECIMAL VLDIARIA
    }
    LOCACAO {
        INT CDLOCACAO PK
        INT CDFILME FK
        INT CDCLIENTE FK
        DATE DTLOCACAO
        DATE DTDEVOLUCAO
    }
    CLIENTE }o--o{ LOCACAO : Aluga
    CLIENTE{
        INT CDCLIENTE PK
        STRING NMCLIENTE
        STRING NMENDERECO
        STRING TELEFONE
        NUMERIC RG
        DECIMAL CPF
    }
```

#### 2.
> **Complete os relacionamentos a seguir, levando em consideração que esse sistema é utilizado para cadastrar pessoas interessadas em vender e comprar imóveis. Portando, imagine que há apenas um vendedor para cada imóvel, mas que vários compradores podem fazer oferta para o mesmo imóvel. Leve em consideração que o imóvel será posteriormente pesquisado por Estado, Cidade, Bairro e Faixa de Preço. Por esse motivo, não há necessidade de relacionar Estado, Cidade e Bairro com o Vendedor e Comprador. Acrescente um relacionamento para a indicação de outro Imóvel. Note que a Faixa do Imóvel representa a faixa de preço dos imóveis e que, portando, não é um relacionamento que pode ser feito diretamente à tabela Imóvel.**

```mermaid
erDiagram
    VENDEDOR {
        INT CDVENDEDOR FK
        STRING NMVENDEDOR
        DECIMAL NMENDERECO
        STRING NMCIDADE
        STRING NMBAIRRO
        CHAR SGESTADO
        STRING TELEFONE
        STRING EMAIL
    }
    IMOVEL {
        INT CDIMOVEL PK
        STRING NMENDERECO
        DECIMAL NRAREAUTIL
        DECIMAL NRAREATOTAL
        STRING DSIMOVEL
        DECIMAL VLPRECO
        INT NROFERTAS
        STRING STVENDIDO
        DATE DTLANCTO
    }
```

```mermaid
erDiagram
    ESTADO {
        CHAR SGESTADO PK
        STRING NMESTADO
    }
    CIDADE {
        INT CDCIDADE PK
        STRING NMCIDADE
    }
    BAIRRO {
        INTER CDBAIRRO
        STRING NMBAIRRO
    }
```

```mermaid
erDiagram
    COMPRADOR {
        INT CDCOMPRADOR PK
        STRING NMCOMPRADOR
        DECIMAL NMENDERECO
        STRING NMCIDADE
        STRING NMBAIRRO
        CHAR SGESTADO
        STRING TELEFONE
        STRING EMAIL
    }
    x {
        DECIMAL VLOFERTA
        DATE DTOFERTA
    }
    FAIXA_IMOVEL {
        STRING NMFAIXA PK
        DECIMAL VLMINIMO
        DECIMAL VLMAXIMO
    }
```

#####==Resposta==

```mermaid
erDiagram
    FAIXA_IMOVEL {
        INT CDFAIXA PK
        STRING NMFAIXA
        DECIMAL VLMINIMO
        DECIMAL VLMAXIMO
    }
    VENDEDOR |o..o{ IMOVEL : Anuncia
    VENDEDOR {
        INT CDVENDEDOR FK
        STRING NMVENDEDOR
        DECIMAL NMENDERECO
        STRING NMCIDADE
        STRING NMBAIRRO
        CHAR SGESTADO
        STRING TELEFONE
        STRING EMAIL
    }
    COMPRADOR ||--|{ OFERTA : Faz_oferta
    COMPRADOR {
        INT CDCOMPRADOR PK
        STRING NMCOMPRADOR
        DECIMAL NMENDERECO
        STRING NMCIDADE
        STRING NMBAIRRO
        CHAR SGESTADO
        STRING TELEFONE
        STRING EMAIL
    }
    IMOVEL }o..|| IMOVEL : Indica
    IMOVEL {
        INT CDIMOVEL PK
        STRING NMENDERECO
        DECIMAL NRAREAUTIL
        DECIMAL NRAREATOTAL
        STRING DSIMOVEL
        DECIMAL VLPRECO
        INT NROFERTAS
        STRING STVENDIDO
        DATE DTLANCTO
        INT IMOVEL_INDICADO
    }
    IMOVEL ||--|{ OFERTA : Esta-em
    OFERTA {
        INT CDCOMPRADOR PK
        INT CDIMOVEL PK
        DECIMAL VLOFERTA
        DATE DTOFERTA
    }
    ESTADO ||--|{ CIDADE : Esta-em
    ESTADO {
        CHAR SGESTADO PK
        STRING NMESTADO
    }
    CIDADE ||--|{ BAIRRO : Esta-em
    CIDADE {
        INT CDCIDADE PK
        STRING SGESTADO PK
        STRING NMCIDADE
    }
    BAIRRO }o--o{ IMOVEL : Esta-em
    BAIRRO {
        INTER CDBAIRRO PK
        INT CDCIDADE PK
        STRING SGESTADO PK
        STRING NMBAIRRO
    }
```