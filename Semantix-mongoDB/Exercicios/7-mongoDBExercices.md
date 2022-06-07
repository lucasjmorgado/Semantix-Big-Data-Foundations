# Consultas com Regex

## 1. Mostrar todos os documentos da collection produto do banco de dados seu nome
```
morgado.produto.find()
```

## 2. Buscar os documentos com o atributo nome,  que contenham a palavra “cpu”
```
morgado.produto.find({nome:{$regex: /cpu/}})
```

## 3. Buscar os documentos  com o atributo nome, que começam por “hd” e apresentar os campos nome e qtd
```
morgado.produto.find({nome:{$regex: /^hd/}},{nome:1, qtd:1})
```

## 4. Buscar os documentos  com o atributo descricao.armazenamento, que terminam com “GB” ou “gb” e apresentar os campos nome e descricao
```
morgado.produto.find({"descricao.armazenamento":{$regex: /gb/i}},{nome:1, descricao:1})
```

## 5. Buscar os documentos  com o atributo nome, que contenha a palavra memória, ignorando a letra “o”
```
morgado.produto.find({"nome":{$regex: /mem.ria/}})
```

## 6. Buscar os documentos  com o atributo qtd  que contenham valores com letras, ao invés de números.
```
morgado.produto.find({"qtd":{$regex: /[a-z]/}})
```

## 7. Buscar os documentos com o atributo descricao.sistema, que tenha exatamente a palavra “Windows”
```
morgado.produto.find({"descrica.sistema":{$regex: /^Windows$/}})
morgado.produto.find({"descrica.sistema":Windows})
```