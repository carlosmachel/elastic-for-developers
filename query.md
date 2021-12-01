# Fazendo queries

Existem várias maneiras de fazer queries para pesquisar os documentos. Vamos fazer exemplos no kibana e no sistema.

1. Pesquisa completa que retorne todos os documentos

```sql
SELECT * FROM Books
```

```js
GET /books/_search
{
    "query": {
        "match_all": {}
    }
}
```

Equivalente:

```
GET /books/_search
```

2. Limitando a pesquisa

```sql
SELECT TOP 10 * from Books
```

```js
GET /books/_search
{
    "size": 10,
    "query": {
        "match_all":{}
    }
}
```

3. Controlar a quantidade de propriedades que devem retornar na query.

```sql
SELECT Title from Books
```

```js
GET /books/_search
{
    "_source": ["title"],
    "query": {
        "match_all": {}
    }
}
```

Você pode adicionar ou excluir as propriedades que deseja retornar:

- utilizando o comando **includes** e **excludes**

```js
GET /books/_search
{
    "source": {
        "includes": ["authors"],
        "excludes": ["title"]
    },
    "query": {
        "match_all":{}
    }
}
```

4. Uso de range

- Greater Than Equal

- Greater Than

- Less Than Equal

- Less Than

5. Usando match

6. Usando operator

7. Usando match_phrase

8. Usando slop

9. Usando minimum_should_match

10. Usando must

11. Usando should

12. Usando must_not

13. Usando multi_match

14. Usando score

15. Usando fuzziness

- Quantidade

- Auto

16. Usando sort

17. Usando highlight

18. Usando filter

19. Usando prefix

20. Usando wildcard

21. Usando regexp
