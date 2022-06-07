# Consulta básica em documentos

## 1. Mostrar todos os documentos da collection produto
```
use morgado
morgado.produto.show()
```
## 2. Pesquisar na collection produto, os documentos com os seguintes atributos:

- a) Nome = mouse
```
morgado.produto.find(nome:"mouse")
```
- b) Quantidade = 20 e apresentar apenas o campo nome
```
morgado.produto.find({qtd:20},{nome:1, _id:0})
```
- c) Quantidade <= 20 e apresentar apenas os campos nome e qtd
```
morgado.produto.find({qtd:{$lte:20}},{nome:1,qtd:1})
```
- d) Quantidade entre 10 e 20
```
morgado.produto.find({qtd:{$lte:20,$gte:10}})
```
- e) Conexão = USB e não apresentar o campo _id e qtd
```
morgado.produto.find({'descricao.conexao':"USB"},{_id:0,qtd:0})
```
- f) SO que contenha “Windows” ou “Windows 10”
```
morgado.produto.find({'descricao.so':{$in:["Windows","Windows 10"]}})
```