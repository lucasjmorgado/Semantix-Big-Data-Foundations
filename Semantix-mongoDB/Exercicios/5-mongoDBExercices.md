# CRUD de Documentos

## 1. Criar a collection teste no banco de dados seu nome
```
morgado.createCollection('teste')
```

## 2. Inserir o seguinte documento:
- Campo: usuario, valor: Semantix
- Campo: data_acesso, valor: data atual no formato ISODate

```
morgado.teste.insertOne({usuario: 'Semantix': new Date()})
```
## 3. Buscar todos os documentos do ano >= 2020
```
morgado.teste.find({data_acesso: {$gte: new Date('2020')}})
```

## 4. Atualizar o campo “data_acesso” para timestamp com o valor da atualização do usuario Semantix
```
morgado.teste.updateOne({usuario: 'Semantix'},{$currentDate: {data_acesso: {type: 'timestamp'}}})
```

## 5. Buscar todos os documentos
```
morgado.teste.find()
```

## 6. Deletar o documento criado pelo id
```
morgado.test.deleteOne({_id: ObjectId("5f3454493098faf852019979")})
```

## 7. Deletar a collection
```
morgado.teste.drop()
```