## Chapter 2 - Designing database

Before creating the database or starting to use SQL commands. The book addresses an extremely important subject: Planning a database.

In summary, there are studies that indicate that the more time spent on database design, the less time spent on model maintenance. Therefore, this planning is extremely important for the stability of the entire system, avoiding future development problems.

We can compare database planning with a building structure. If not given proper attention, the building will collapse.

*As presented in the book, we will perform the first exercises by doing an ERDiagram*

------

### Proposed exercises

#### 1.
**See data models below. Identify the relationships between the entities presented. Take into account that the Genre is Drama, Comedy, Adventure, etc. and Category is the price range of the movie. In a more complete model, there should be several tapes for the same film, but imagine that, in this system, there is no such need.**


```mermaid
erDiagram
    GENERO {
        INT CDGENERO FK
        VARCHAR NMGENERO
    }
    FILME {
        INT CDFILME PK
        VARCHAR NMFILME
        DECIMAL DURACAO
        VARCHAR SINOPSE
        BLOB FOTO
        VARCHAR STLOCADO
    }
    CATEGORIA {
        INT CDCATEGORIA PK
        VARCHAR NMCATEGORIA
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
        VARCHAR NMCLIENTE
        VARCHAR NMENDERECO
        VARCHAR TELEFONE
        NUMERIC RG
        DECIMAL CPF
    }
```

##### REPLY
```mermaid
erDiagram
    GENERO ||--o{ FILME : Contem
    GENERO {
        INT CDGENERO FK
        VARCHAR NMGENERO
    }
    FILME }o--o{ LOCACAO : Esta-em
    FILME {
        INT CDFILME PK
        INT CDGENERO FK
        VARCHAR NMFILME
        DECIMAL DURACAO
        VARCHAR SINOPSE
        BLOB FOTO
        VARCHAR STLOCADO
        INT CDCATEGORIA FK
    }
    CATEGORIA ||--o{ FILME : Contem
    CATEGORIA {
        INT CDCATEGORIA PK
        VARCHAR NMCATEGORIA
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
        VARCHAR NMCLIENTE
        VARCHAR NMENDERECO
        VARCHAR TELEFONE
        NUMERIC RG
        DECIMAL CPF
    }
```

&#xa0;

#### 2.
**Fill in the following relationships, taking into account that this system is used to register people interested in selling and buying properties. So imagine that there is only one seller for each property, but that multiple buyers can bid on the same property. Take into account that the property will be later searched by State, City, Neighborhood and Price Range. For this reason, there is no need to relate State, City and Neighborhood with Seller and Buyer. Add a relation that points to another Property. Note that the entity (FAIXA_IMOVEL) represents the price range of the property. And therefore it is not a relationship that can be made directly with the properties entity.**

```mermaid
erDiagram
    VENDEDOR {
        INT CDVENDEDOR FK
        VARCHAR NMVENDEDOR
        DECIMAL NMENDERECO
        VARCHAR NMCIDADE
        VARCHAR NMBAIRRO
        CHAR SGESTADO
        VARCHAR TELEFONE
        VARCHAR EMAIL
    }
    IMOVEL {
        INT CDIMOVEL PK
        INT CDVENDEDOR FK
        INT CDBAIRRO FK
        INT CDCIDADE FK
        CHAR SGESTADO FK
        VARCHAR NMENDERECO
        DECIMAL NRAREAUTIL
        DECIMAL NRAREATOTAL
        VARCHAR DSIMOVEL
        DECIMAL VLPRECO
        INT NROFERTAS
        VARCHAR STVENDIDO
        DATE DTLANCTO
    }
```

```mermaid
erDiagram
    ESTADO {
        CHAR SGESTADO PK
        VARCHAR NMESTADO
    }
    CIDADE {
        INT CDCIDADE PK
        VARCHAR NMCIDADE
    }
    BAIRRO {
        INTER CDBAIRRO
        VARCHAR NMBAIRRO
    }
```

```mermaid
erDiagram
    COMPRADOR {
        INT CDCOMPRADOR PK
        VARCHAR NMCOMPRADOR
        DECIMAL NMENDERECO
        VARCHAR NMCIDADE
        VARCHAR NMBAIRRO
        CHAR SGESTADO
        VARCHAR TELEFONE
        VARCHAR EMAIL
    }
    x {
        DECIMAL VLOFERTA
        DATE DTOFERTA
    }
    FAIXA_IMOVEL {
        VARCHAR NMFAIXA PK
        DECIMAL VLMINIMO
        DECIMAL VLMAXIMO
    }
```

##### REPLY

```mermaid
erDiagram
    FAIXA_IMOVEL {
        INT CDFAIXA PK
        VARCHAR NMFAIXA
        DECIMAL VLMINIMO
        DECIMAL VLMAXIMO
    }
    VENDEDOR |o--o{ IMOVEL : Anuncia
    VENDEDOR {
        INT CDVENDEDOR FK
        VARCHAR NMVENDEDOR
        DECIMAL NMENDERECO
        VARCHAR NMCIDADE
        VARCHAR NMBAIRRO
        CHAR SGESTADO
        VARCHAR TELEFONE
        VARCHAR EMAIL
    }
    COMPRADOR ||--|{ OFERTA : Faz_oferta
    COMPRADOR {
        INT CDCOMPRADOR PK
        VARCHAR NMCOMPRADOR
        DECIMAL NMENDERECO
        VARCHAR NMCIDADE
        VARCHAR NMBAIRRO
        CHAR SGESTADO
        VARCHAR TELEFONE
        VARCHAR EMAIL
    }
    IMOVEL }o..|| IMOVEL : Indica
    IMOVEL {
        INT CDIMOVEL PK
        INT CDBAIRRO FK
        INT CDCIDADE FK
        CHAR SGESTADO FK
        VARCHAR NMENDERECO
        DECIMAL NRAREAUTIL
        DECIMAL NRAREATOTAL
        VARCHAR DSIMOVEL
        INT NROFERTAS
        DECIMAL VLPRECO
        VARCHAR STVENDIDO
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
        VARCHAR NMESTADO
    }
    CIDADE ||--|{ BAIRRO : Esta-em
    CIDADE {
        INT CDCIDADE PK
        VARCHAR SGESTADO PK
        VARCHAR NMCIDADE
    }
    BAIRRO |o--o{ IMOVEL : Esta-em
    BAIRRO {
        INTER CDBAIRRO PK
        INT CDCIDADE PK
        VARCHAR SGESTADO PK
        VARCHAR NMBAIRRO
    }
```

&#xa0;

### 3
** Add attributes that you consider important to the entities below. In this exercise, you are an auto accessories installation company, so the customer takes his car to install the products in the store.**

```mermaid
erDiagram
    LOJA {

    }
    PEDIDO {

    }
    CLIENTE {

    }
```

```mermaid
erDiagram
    PRODUTO {
    }
    AUTOMOVEL {

    }
```

##### REPLY

```mermaid
    erDiagram
    ESTADO ||--|{ CIDADE : Esta-em
    ESTADO {
        CHAR SGESTADO PK
        VARCHAR NMESTADO
    }
    CIDADE ||--|{ BAIRRO : Esta-em
    CIDADE {
        INT CDCIDADE PK
        VARCHAR SGESTADO PK
        VARCHAR NMCIDADE
    }
    BAIRRO |o--o{ LOJA : Esta-em
    BAIRRO {
        INTER CDBAIRRO PK
        INT CDCIDADE PK
        VARCHAR SGESTADO PK
        VARCHAR NMBAIRRO
    }
    LOJA ||--|{ PEDIDO : Esta_no
    LOJA {
        INT CDLOJA PK
        VARCHAR NMLOJA
        VARCHAR SGESTADO FK
        VARCHAR CDCIDADE FK
        VARCHAR CDBAIRRO FK
        VARCHAR NMENDERECO
        VARCHAR NRTELEFONE
        VARCHAR NMGERENTE                                        
    }
    PEDIDO {
        INT CDPEDIDO PK
        INT CDLOJA FK
        INT CDPRODUTO FK
        INT CDAUTOMOVEL FK
        DECIMAL VLTOTAL
    }
    PRODUTO }o--o{ PEDIDO : Esta_no
    PRODUTO {
        INT CDPRODUTO PK
        VARCHAR NMPRODUTO
        DECIMAL PRECO
        DECIMAL TEMPINSTALACAO
    }
    COMBUSTIVEL ||--o{ AUTOMOVEL : Esta_no
    COMBUSTIVEL {
        INT CDCOMBUSTIVEL PK
        VARCHAR NMCOMBUSTIVEL
    }
    AUTOMOVEL }|--o{ PEDIDO : Esta_no
    AUTOMOVEL {
        VARCHAR NRPLACA PK
        VARCHAR CDMODELO FK
        VARCHAR CDCOMBUSTIVEL FK
        DATE ANOFABRICACAO
        DECIMAL NRKM
        VARCHAR OBSERVACAO
    }
    MODELO_CARRO }|--o{ AUTOMOVEL : Esta_no
    MODELO_CARRO {
        INT CDMODELO PK
        INT CDMARCA FK
        VARCHAR NMMODELO
    }
    MARCA_CARRO }|--o{ MODELO_CARRO : Esta_no
    MARCA_CARRO {
        INT CDMARCA PK
        VARCHAR NMMARCA
    }
    AUTO_CLIENTE }o--|| AUTOMOVEL : Contem
    AUTO_CLIENTE {
        INT CDCLIENTE PK
        VARCHAR NRPLACA PK
    }
    CLIENTE ||--o{ AUTO_CLIENTE : Contem
    CLIENTE {
        INT CDCLIENTE PK
        VARCHAR NMCLIENTE
        DECIMAL NRCPF
        VARCHAR NRTELEFONE
        VARCHAR SGESTADO
        VARCHAR NMCIDADE
        VARCHAR NMBAIRRO
        VARCHAR NMENDERECO
    }
```

&#xa0;

### 4

**Based on the following scopes, create an Entity X Relationship model for each system:**

- ##### 4ᴬ) I am the manager of a training company that teaches several technical courses. These courses are identified by code, name, and duration. We set up classes based on the courses we offer. Classes have fixed days of the week, which we identify as a letter (S for Monday-Wednesday-Friday, T for Tuesday-Thursday, and B for Saturday), a specific start and end time, and a price. One instructor can teach multiple classes and we do not change instructors for the duration of a class. It is important to know the name, address and telephone number of each instructor. Students are always linked to a class. We must know the name, address and telephone number of each student.

##### REPLY

```mermaid
    erDiagram
    INSTRUTOR ||--o{ TURMAS : Ministra
    INSTRUTOR{
        INT CDINSTRUTOR PK
        VARCHAR NMPRIMEIRO
        VARCHAR NMSEGUNDO
        DECIMAL CPF
        VARCHAR TELEFONE
        VARCHAR EMAIL
        VARCHAR PASSWORD
        NUMERIC CEP
        INT CDBAIRRO FK
        INT CDCIDADE FK
        CHAR SGESTADO FK
        VARCHAR NMENDERECO
    }
    ALUNO }o--o{ TURMAS : Cursa
    ALUNO{
        INT CDALUNO PK
        INT CDTURMA FK
        VARCHAR NMPRIMEIRO
        VARCHAR NMSEGUNDO
        DECIMAL CPF
        VARCHAR TELEFONE
        VARCHAR EMAIL
        VARCHAR PASSWORD
        NUMERIC CEP
        INT CDBAIRRO FK
        INT CDCIDADE FK
        CHAR SGESTADO FK
        VARCHAR NMENDERECO
    }
    TURMAS }|--|{ CURSO : Contem
    TURMAS{
        INT CDTURMA PK
        VARCHAR CRONOGRAMA FK
        VARCHAR NMTURMA
        INT CDINSTRUTOR FK
        INT CDCURSO FK
    }
    CURSO{
        INT CDCURSO PK
        VARCHAR NMCURSOR
        DECIMAL PRECO
        DATE INICIO
        DATE FIM
    }
    CRONOGRAMA }|--|{ TURMAS : Esta-em
    CRONOGRAMA{
        CHAR NMCRONOGRAMA PK
        VARCHAR NMSDIA
        TIME HORINICIO
        TIME HORFINAL
    }
    ESTADO ||--|{ CIDADE : Esta-em
    ESTADO {
        CHAR SGESTADO PK
        VARCHAR NMESTADO
    }
    CIDADE ||--|{ BAIRRO : Esta-em
    CIDADE {
        INT CDCIDADE PK
        VARCHAR SGESTADO PK
        VARCHAR NMCIDADE
    }
    BAIRRO |o--o{ INSTRUTOR : Contem
    BAIRRO |o--o{ ALUNO : Contem
    BAIRRO {
        INTER CDBAIRRO PK
        INT CDCIDADE PK
        VARCHAR SGESTADO PK
        VARCHAR NMBAIRRO
    }
```

&#xa0;

- ##### 4ᴮ) I'm a Human Resources manager. I need to keep information of every employee in the company. The information for each employee I need is: first name, last name, role, hire date and salary. If the employee is commissioned, I need to know the average commission amount. The company is divided into department. Each employee is allocated to a department. I need to know the name of the department and its location. Some employees are also managers, so I need to know which manager each employee is. Note that the manager himself is also an employee

##### REPLY

```mermaid
    erDiagram
    FUNCIONARIO }|--|| DEPARTAMENTO : Pertence
    FUNCIONARIO {
        INT CDFUNCIONARIO PK
        VARCHAR NMPRIMEIRO
        VARCHAR NMULTIMO
        DECIMAL CPF
        DECIMAL CEP
        INT CDBAIRRO FK
        VARCHAR NMENDERECO
        DATETIME DATA_ADMISSAO
        DECIMAL SALARIO
        INT CDFUNCAO FK
        VARCHAR NMDEPARTAMENTO FK
    }
    GERENTE }|--|| FUNCIONARIO : CARGO
    GERENTE {
        INT CDFUNCIONARIO PK
        INT CDGERENTE PK
    }
    DEPARTAMENTO }|--|| GERENTE : GERENCIA
    DEPARTAMENTO {
        VARCHAR NMDEPARTAMENTO PK
        INT CDLOCALIZACAO FK
        INT CDGERENTE FK
    }
    DEPARTAMENTO }|--|| LOCALIZACAO : Esta-no
    LOCALIZACAO {
        INT CDLOCALIZACAO PK
        INT NRBLOCO
        INT NRPISO
        VARCHAR NMLADO
        INT NRSALA
    }
    FUNCAO ||--o{ FUNCIONARIO : Contem
    FUNCAO{
        INT CDFUNCAO PK
        VARCHAR NMFUNCAO
    }
    LANCAMENTO_COMISSAO ||--o{ FUNCIONARIO : Contem
    LANCAMENTO_COMISSAO {
        INT CDLANCAMENTO
        INT CDFUNCIONARIO
        DECIMAL VLPAGO
        DATETIME DTPAGAMENTO
    }
    ESTADO ||--|{ CIDADE : Esta-em
    ESTADO {
        CHAR SGESTADO PK
        VARCHAR NMESTADO
    }
    CIDADE ||--|{ BAIRRO : Esta-em
    CIDADE {
        INT CDCIDADE PK
        VARCHAR SGESTADO PK
        VARCHAR NMCIDADE
    }
    BAIRRO ||--|{ FUNCIONARIO : Contem
    BAIRRO {
        INTER CDBAIRRO PK
        INT CDCIDADE PK
        VARCHAR SGESTADO PK
        VARCHAR NMBAIRRO
    }
```

&#xa0;

- ##### 4ᶜ) I have a website where we try to solve computer related problems. To make questions easier to find, we've segmented questions by platform and segment. From there, we find the events related to that platform (such as Windows, Unix, Linux) and with the segments (such as Office packages ready, among others, operating system, programming languages). With this information, we can fetch the events related to the platform and the segment to show the user. In the events, we store the date of occurrence, the description of the problem and the solution presented, in addition to the user who raised the issue. Other users can make comments (a free text) about the presented events. We register all users with their name, address and telephone number. We also record the consultants who answer the questions. We need to know the name, address and telephone number of the consultants.

##### REPLY

```mermaid
    erDiagram
    PLATAFORMAS ||--|{ AREA_INTERESSE : Contem
    PLATAFORMAS {
        INT CDPLATAFORMA PK
        VARCHAR NMPLATAFORMA
    }
    AREA_INTERESSE }|--|{ DUVIDAS : Escolhe
    AREA_INTERESSE {
        INT CDAREA PK
        INT CDPLATAFORMA FK
        VARCHAR NMAREA
        VARCHAR DESAREA
    }
    DUVIDAS {
        INT CDDUVIDA PK
        INT CDUSUARIO FK
        INT CDPLATAFORMA FK
        INT CDAREA FK
        VARCHAR DESCRICAO
        VARCHAR SOLUCAO
        INT CDCONSULTOR FK
        DATETIME ABERTO
        DATETIME FECHADO
    }
    COMENTARIOS }|--|{ DUVIDAS : Responde
    COMENTARIOS {
        INT CDCOMENTARIO PK
        INT CDDUVIDA PK
        INT CDUSUARIO FK
        VARCHAR DESCRICAO
    }
    USUARIO }|--|{ DUVIDAS : Criado_por
    USUARIO {
        INT CDUSUARIO PK
        VARCHAR NMPRIMEIRO
        VARCHAR NMULTIMO
        DECIMAL CPF
        DECIMAL CEP
        VARHCAR CDBAIRRO
        VARCHAR NMLOGRADOURO
        DATE DATA_CADASTRO
    }
    ESTADO ||--|{ CIDADE : Esta-em
    ESTADO {
        CHAR SGESTADO PK
        VARCHAR NMESTADO
    }
    CIDADE ||--|{ BAIRRO : Esta-em
    CIDADE {
        INT CDCIDADE PK
        VARCHAR SGESTADO PK
        VARCHAR NMCIDADE
    }
    BAIRRO ||--|{ USUARIO : Contem
    BAIRRO {
        INTER CDBAIRRO PK
        INT CDCIDADE PK
        VARCHAR SGESTADO PK
        VARCHAR NMBAIRRO
    }
    GRUPO_USUARIO }|--|| USUARIO : Contem
    GRUPO_USUARIO {
        INT CDGRUPO PK
        INT CDUSUARIO PK
    }
    GRUPO ||--|{ GRUPO_USUARIO : Contem
    GRUPO {
        INT CDGRUPO PK
        VARCHAR NMGRUPO
    }
```