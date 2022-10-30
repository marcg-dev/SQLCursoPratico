## Capitulo 2 - Projetando banco de dados

Antes da criação do banco de dados ou iniciarmos a utilização dos comandos SQL. O livro aborda um assunto de extrema importancia: Planejamento de um banco de dados.

Em resumo, existem estudos que indicam que quanto maior o tempo despendido no desenho do banco de dados, menor será o tempo despendido na manutenção do modelo. Então esse desenho é de extrema importancia para a estabilidade de todo o sistema, evitando futuramente um comprometimento de todo o desenvolvimento.

Podemos comparar o planejamento do banco de dados com uma estrutura de um prédio. Se não for dado a devida atenção, o edifício irá cair.

*Conforme apresentado no livro, iremos realizar os primeiros exercícios fazendo a criação das entidades e seus relacionamentos.*

------


### Exercícios propostos

#### 1.
**Veja os modelos de dados a seguir. Identifique os relacionamentos entre as entidades apresentadas. Leve em consideração que o Gênero é Drama, Comédia, Aventura etc. e Categoria é a faixa de preço do filme. Em um modelo mais completo, deveria haver várias fitas para um mesmo filme, mas imagine que, nesse sistema não haja essa necessidade.**


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

##### Resposta
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

#### 2.
**Complete os relacionamentos a seguir, levando em consideração que esse sistema é utilizado para cadastrar pessoas interessadas em vender e comprar imóveis. Portando, imagine que há apenas um vendedor para cada imóvel, mas que vários compradores podem fazer oferta para o mesmo imóvel. Leve em consideração que o imóvel será posteriormente pesquisado por Estado, Cidade, Bairro e Faixa de Preço. Por esse motivo, não há necessidade de relacionar Estado, Cidade e Bairro com o Vendedor e Comprador. Acrescente um relacionamento para a indicação de outro Imóvel. Note que a Faixa do Imóvel representa a faixa de preço dos imóveis e que, portando, não é um relacionamento que pode ser feito diretamente à tabela Imóvel.**

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

##### Resposta

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
        VARCHAR NMENDERECO
        DECIMAL NRAREAUTIL
        DECIMAL NRAREATOTAL
        VARCHAR DSIMOVEL
        DECIMAL VLPRECO
        INT NROFERTAS
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

### 3
**Relacione as entidades a seguir e acrescente atributos que você julgue importantes para o sistema. Nesse caso, trata-se de uma empresa de instalação de acessórios para automóveis e, portando, o cliente leva o seu automóvel para instalar produtos na loja.**

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

##### Resposta

```mermaid
    erDiagram
    LOJA ||--|{ PEDIDO : Esta_no
    LOJA {
        INT CDLOJA PK
        VARCHAR NMLOJA
        VARCHAR NMENDERECO
        VARCHAR NRTELEFONE
        VARCHAR NMGERENTE                                        
    }
    PEDIDO {
        INT CDPEDIDO PK
        INT CDLOJA FK
        INT CDPRODUTO FK
        INT CDAUTOMOVEL FK
        DECIMAL PRECO_TOTAL
    }
    PRODUTO }o--o{ PEDIDO : Esta_no
    PRODUTO {
        INT CDPRODUTO PK
        VARCHAR NMPRODUTO
        DECIMAL PRECO
        DECIMAL TEMP_INSTALACAO
    }
    AUTOMOVEL }|--o{ PEDIDO : Esta_no
    AUTOMOVEL {
        VARCHAR NRPLACA PK
        VARCHAR NMMODELO
        DATE ANO_FABRICACAO
        CHAR TIPO_COMBUSTIVEL
        DECIMAL NRKM
    }
    AUTO_CLIENTE }o--|| CLIENTE : Contem
    AUTO_CLIENTE }o--|| AUTOMOVEL : Contem
    AUTO_CLIENTE {
        INT CDCLIENTE PK
        VARCHAR NRPLACA PK
    }
    CLIENTE {
        INT CDCLIENTE PK
        VARCHAR NMCLIENTE
        DECIMAL NRCPF
        VARCHAR NRTELEFONE
        VARCHAR NMENDERECO
    }
```


### 4
**Com base nos escopos a seguir, crie um modelo de Entidade X Relacionamento para cada sistema:**

- A) Sou gerente de uma empresa de treinamento que ministra vários cursos técnicos. Esses cursos são identificados por código, nome, e tempo de duração. Montamos turmas com base nos cursos que oferecemos. As turmas têm dias fixos da semana, que identificamos como uma letra (S para segunda-quarta-sexta, T para terça-quinta e B para sábado), um horário específico para início e fim, e um preço. Um instrutor pode dar aulas para várias turmas e nós não trocamos os respectivos instrutores enquanto durar o curso de uma turma. É importante saber o nome, o endereço e o telefone de cada instrutor. Os alunos estão sempre vinculados a uma turma. Devemos saber o nome, o endereco e o telefone de cada aluno.

##### Resposta

> Obs.: Criei a entidade (cronograma) para que futuramente possa ser feito consultas, com o intuito de verificar os dias das siglas. Pensando também na possibilidade de serem criadas siglas no futuro.*

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
        TIME HOR_INICIO
        TIME HOR_FINAL
        INT CDINSTRUTOR FK
        INT CDCURSO FK
    }
    CURSO{
        INT CDCURSO PK
        VARCHAR NMCURSOR
        DECIMAL PRECO
        TIME TEMP_CURSO
    }
    CRONOGRAMA }|--|{ TURMAS : Esta-em
    CRONOGRAMA{
        VARCHAR NMCRONOGRAMA PK
        DATE DIA1
        DATE DIA2
        DATE DIA3
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

- B) Sou um gerente de Recursos Humanos. Preciso manter informações de cada funcionário da empresa. As informações de cada funcionário de que necessito são: o primeiro nome, o último nome, a função, a data de admissão e o salário. Caso o funcionário seja comissionado, preciso saber o valor médio da comissão. A empresa é dividida em departamento. Cada funcionário é alocado em um departamento. Preciso saber o nome do departamento e sua localização. Alguns funcionários são também gerentes, portando preciso saber qual o gerente de cada funcionário. Note que o próprio gerente é também um funcionário

##### Resposta

```mermaid
    erDiagram
    FUNCIONARIO }|--o| DEPARTAMENTO : Pertence
    FUNCIONARIO {
        INT CDFUNCIONARIO PK
        VARCHAR NMPRIMEIRO
        VARCHAR NMULTIMO
        DECIMAL CPF
        DECIMAL CEP
        INT CDBAIRRO FK
        INT CDCIDADE FK
        CHAR SGESTADO FK
        VARCHAR NMENDERECO
        DATETIME DATA_ADMISSAO
        DECIMAL SALARIO
        DECIMAL VL_MED_COMISSAO
        INT CDFUNCAO FK
        VARCHAR NMCARGO FK
        VARCHAR NMDEPARTAMENTO FK
        INT CDGERENTE FK
    }
    DEPARTAMENTO {
        VARCHAR NMDEPARTAMENTO PK
        INT CDLOCALIZACAO FK
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
    GERENTE ||..o{ FUNCIONARIO : Contem_ou_e
    GERENTE {
        INT CDFUNCIONARIO PK
        INT CDGERENTE PK
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

- C) Possuo um site na Internet onde tentamos resolver questões relacionadas com informática. Para facilitar a localização das questões, segmentamos as dúvidas por plataforma e área de interesse. A partir daí, localizamos os eventos relacionados com essa plataforma (como Windows, Unix, Linux) e esse segmento (como pacotes prontos Office Entre outros, sistema operacional, linguagens de programação). Com essas informações, podemos buscar os eventos relacionados à plataforma e ao segmento para mostrar ao usuário. Nos eventos armazenamos a data da ocorrência, a descrição do problema e da solução apresentada, além do usuário que levantou a dúvida. Outros usuários podem fazer comentários (um texto livre) sobre os eventos apresentados. Cadastramos todos os usuários com o nome, o endereço e o telefone. Cadastramos também os consultores que respondem as questões. Precisamos saber o nome, o endereço e o telefone dos consultores.

##### Resposta

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
        INT CDPLATAFORMA FK
        INT CDAREA FK
        INT CDUSUARIO FK
        INT CDUSUARIO
        VARCHAR DESCRICAO
        VARCHAR SOLUCAO
        DATETIME ABERTURA
    }
    COMENTARIOS }|--|{ DUVIDAS : Responde
    COMENTARIOS {
        INT CDCOMENTARIO PK
        INT CDDUVIDA PK
        INT CDUSUARIO FK
        VARCHAR DESCRICAO
        BIT SOLUCAO
    }
    USUARIO }|--|{ DUVIDAS : Criado_por
    USUARIO {
        INT CDUSUARIO PK
        VARCHAR NMPRIMEIRO
        VARCHAR NMULTIMO
        DECIMAL CPF
        DECIMAL CEP
        VARCHAR SGESTADO
        VARCHAR NMCIDADE
        VARHCAR NMBAIRRO
        VARCHAR NMLOGRADOURO
        DATE DATA_CADASTRO
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