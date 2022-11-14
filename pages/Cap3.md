## Chapter 3 - Database Normalization

In the previous chapter, we did the modeling, using the strategy: Entity Relationship.

Now let's talk about database normalization, a "scientific" way of creating and validating a model.

Database normalization occurs through a sequence of successive steps: (1NF, 2NF, 3NF and BCNF ). Which, in the end, will present a stable data model with minimal redundancy.

The final result of a data model can be extracted with extreme quality in both formats. Whether in ERDiagram or database normalization. But we can use both formats in the same modeling, to ensure a very stable model.

---

**Stage of Normalization**

- **1NF:** An entity is in first normal form when none of its attributes have repetitions.
  
* **2NF:** An entity is in second normal form when all of its non-key attributes depend solely on the key.

- **3NF:** An entity is in third normal form when all its non-key attributes do not depend on any other non-key attributes.

- **BCNF:** An entity will be in fourth normal form if we need to split an entity that was already in third normal form and still has redundancies. This occurs when a non-key attribute contains multiple values for the same key.

`After the normalization process is complete, no entity can be below third normal form.`

`If necessary, we repeat the process of applying the rules as many times as necessary in each entity.`

---

### Proposed exercises

#### 1.
**Review the data models created in Exercise Chapter 2 and see if you need to change any of the models. Justify your answer.**

[Exercise 1:](https://github.com/marcg-dev/SQLCursoPratico/blob/master/pages/Cap2.md#1)
It was not necessary to make corrections after applying the database normalization rules.	

[Exercise 2:](https://github.com/marcg-dev/SQLCursoPratico/blob/master/pages/Cap2.md#2)
It was not necessary to make corrections after applying the database normalization rules.

[Exercise 3:](https://github.com/marcg-dev/SQLCursoPratico/blob/master/pages/Cap2.md#3)
To create a scalable system and within the database normalization rules, it was necessary to add the entities: **(MARCA_CARRO | MODELO_CARRO | AUTO_CLIENTE | COMBUSTIVEL).** Using the structure presented in the exercise, we would have an extremely limited system.

[Exercise 4ᴬ:](https://github.com/marcg-dev/SQLCursoPratico/blob/master/pages/Cap2.md#4%E1%B4%AC)
It was necessary to make some changes to the entity **(CRONOGRAMA)**. So that in the future it is possible to have better flexibility in the creation of new departments

[Exercise 4ᴮ:](https://github.com/marcg-dev/SQLCursoPratico/blob/master/pages/Cap2.md#4%E1%B4%AE)
To respect the database normalization rules, it was necessary to correct some entities **(FUNCIONARIO | GERENTE | DEPARTAMENTO).** and add a new entity called **(LANCAMENTO_COMISSAO).**

[Exercise 4ᶜ:](https://github.com/marcg-dev/SQLCursoPratico/blob/master/pages/Cap2.md#4%E1%B6%9C)
Finally, I also needed to make corrections to the entities **(DUVIDAS | USUARIO)** to have the data normalization rules applied reliably.

**Conclusion**

> **To avoid redundancies and incorrect data, I have kept the entities **(ESTADO | CIDADE | BAIRRO)** for all the Exercises mentioned above.**
> 
> **It is evident how the database normalization strategy helped me to correct several problems in my first modeling, where I used the ERDiagram strategy. It was clear that the corrections made provided me with more scalable systems with better data qualities.**

**NOTE**
> The book informs us that it is often necessary to assess the need to keep some redundant fields in the entity.
>
> This process is called “database denormalization”.
>
> This doesn't mean we're going to throw away all the work we've done before, but we need to remember that: Even the most advanced databases have limitations and costs.
>
> It is necessary to carry out an analysis considering the scalability of the system and how this would affect each entity. When encountering any issues that hamper system performance or growth, we need to consider  “database denormalization”.