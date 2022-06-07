# Outras Opções com Consultas

## 1. Mostrar todos os documentos da collection produto
```
use morgado
morgado.produto.find()
```
## 2. Realizar as seguintes pesquisas na collection produto:

- a) Mostrar os documentos ordenados pelo nome em ordem alfabética.
```
morgado.produto.find().sort({nome:1})
```
- b) Mostrar os 3 primeiros documentos ordenados por nome e quantidade.
```
morgado.produto.find().sort({nome:1, qtd:1}).limit(3)
```
- c) Mostrar apenas 1 documento que tenha o atributo Conexão = USB.
```
morgado.produto.find({'descricao.conexao':'usb'}).limit(1)
morgado.produto.findOne('descricao.conexao':'usb')
```
- d) Mostrar os documentos de tenham o atributo conexão = USB e quantidade menor que 25.
```
morgado.produto.find({'descricao.conexao':'usb', qtd:{$lt: 25}})
```
- e) Mostrar os documentos de tenham o atributo conexão = USB ou quantidade menor que 25.
```
morgado.produto.find({$or:[{'descricao.conexao':'usb'}, {qtd:{$lt: 25}}]})
```
- f) Mostrar apenas os id dos documentos de tenham o atributo conexão = USB ou quantidade menor que 25.
```
morgado.produto.find({'descricao.conexao':'usb', qtd:{$lt: 25}},{_id:1})
```