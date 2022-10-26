4## Capitulo 2 - Projetando banco de dados

Antes da criação do banco de dados ou iniciarmos a utilização dos comandos SQL. O livro aborda um assunto de extrema importancia: Planejamento de um banco de dados.

Em resumo, existem estudos que indicam que quanto maior o tempo despendido no desenho do banco de dados, menor será o tempo despendido na manutenção do modelo. Então esse desenho é de extrema importancia para a estabilidade de todo o sistema, evitando futuramente um comprometimento de todo o desenvolvimento.

Podemos comparar o planejamento do banco de dados com uma estrutura de um prédio. Se não for dado a devida atencão, o edifício irá cair.

*Conforme apresentado no livro, iremos realizar os primeiros exercícios fazendo a criacão das entidades e seus relacionamentos.*

------

### Exercícios propostos

### 1.

> **Veja os modelos de dados a seguir. Identifique os relacionamentos entre as entidades apresentadas. Leve em consideração que o Gênero é Drama, Comédia, Aventura etc. e Categoria é a faixa de preço do filme. Em um modelo mais completo, deveria haver várias fitas para um mesmo filme, mas imagine que, nesse sistema não haja essa necessidade.**


````mermaid
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
````

````mermaid
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
````


**<span style='color:red'>Resposta</span>**


````mermaid
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
````