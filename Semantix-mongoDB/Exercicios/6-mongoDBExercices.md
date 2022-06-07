# Index e plano de execução

## 1. Mostrar todos os documentos da collection produto do banco de dados seu nome
```
morgado.produto.find()
```

## 2. Criar o index “query_produto” para pesquisar o campo nome do produto em ordem alfabética
```
morgado.produto.createIndex({nome:1},{name: 'query_produto'})
```

## 3. Pesquisar todos os índices da collection produto
```
morgado.produto.getIndexes()
```

## 4. Pesquisar todos os documentos da collection produto
```
morgado.produto.find()
```

## 5. Visualizar o plano de execução do exercício 4
```
morgado.produto.find().explain()
```

## 6. Pesquisar todos os documentos da collection produto, com uso da index “query_produto”
```
morgado.produto.find().hint({nome:1})
```

## 7. Visualizar o plano de execução do exercício 7
```
morgado.produto.find().hint({nome:1}).explain()
```

## 8. Remover o index “query_produto”
```
morgado.produto.dropIndex({nome:1})
```

## 9. Pesquisar todos os índices da collection produto
```
morgado.produto.getIndexes()
```