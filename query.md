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

4. Retornar todos os tipos ordernados por campo.

```sql
SELECT top 10 * FROM Books ORDER BY title asc
```

```js
GET /books/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "title.keyword": {
        "order": "desc"
      }
    }
  ],
  "size": 10
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

4. Retornar top 10 autores que mais publicaram livros

```sql
SELECT top 10 Authors, count(1)
FROM Books
group by Authors
order by count(1) desc
```

```js
GET /books/_search
{
  "sort": [{
      "authors.keyword": {
        "order": "asc"
      }
    }
  ],
  "size":10,
  "aggs": {
    "top_authors": {
      "value_count": {
        "field": "authors.keyword"
      }
    }
  }
}
```

4. Uso de range

```sql

```

```js
{"from":1,"query":{"range":{"originalPublicationYear":{"gt":1990.0,"lt":2000.0}}},"size":10}
```

- Greater Than Equal

```sql

```

```js

```

- Greater Than

```sql

```

```js

```

- Less Than Equal

```sql

```

```js

```

- Less Than

```sql

```

```js

```

5. Usando match

```sql

```

```js
GET /books/_search
{
    "query": {
        "match": {
            "title": "The Hunger Games"
        }
    }
}
```

6. Usando operator

```sql

```

```js

```

7. Usando match_phrase

```sql

```

```js
{"from":1,"query":{"match_phrase":{"title":{"query":"The Hunger Games"}}},"size":10}
```

```csharp
var query = new QueryContainer();

query = Query<Book>.MatchPhrase(mp => mp.Field(f => f.Title).Query(term));

var result = await _elasticClient.SearchAsync<Book>(s => s
.From(from)
.Size(size)
.Query(_ => query));
```

8. Usando slop

```sql

```

```js

```

9. Usando minimum_should_match

```sql

```

```js

```

10. Usando must

```sql

```

```js
{"query":{"bool":{"must":[{"bool":{"must":[{"match":{"authors":{"query":"Suzanne"}}},{"match":{"title":{"query":"Hunger Games"}}}]}}]}}}
```

11. Usando should

```sql

```

```js

```

12. Usando must_not

```sql

```

```js

```

13. Usando multi_match

```sql

```

```js

```

14. Usando score

```sql

```

```js

```

15. Usando fuzziness

- Quantidade

```sql

```

```js

```

- Auto

```sql

```

```js

```

16. Usando sort

```sql

```

```js

```

17. Usando highlight

```sql

```

```js

```

18. Usando filter

```sql

```

```js

```

19. Usando prefix

```sql

```

```js

```

20. Usando wildcard

```sql

```

```js

```

21. Usando regexp

```sql

```

```js

```

22. Usando nested

```js
GET /books/_search
{
    "query": {
        "nested": {
            "path": "caminho_do_documento_nested",
            "query":{}
        }
    }
}
```

```js
GET /books-nested/_search
{
  "query": {
      "nested":{
        "path": "authors",
        "query": {
          "bool": {
            "must": [
              {"match": {"authors.name": "Suzzane"}},
              {"match": {"authors.year": 35}}
            ]
          }
        }
      }
    }
  }
```
