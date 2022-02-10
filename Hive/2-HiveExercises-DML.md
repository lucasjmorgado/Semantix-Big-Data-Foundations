# Exercícios Hive 2
## 1.Visualizar a descrição da tabela pop do banco de dados <nome>
```
docker exec -it hive-server bash
beeline -h
beeline -u jdbc:hive2://localhost:10000 -> Acesso root
desc morgado.pop;
desc formatted morgado.pop;
```
## 2.Selecionar os 10 primeiros registros da tabela pop
```
select * from morgado.pop limit 10;
```
## 3.Carregar o arquivo do HDFS “/user/aluno/<nome>/data/população/populacaoLA.csv” para a tabela Hive pop
```
load data inpath '/user/aluno/morgado/data/populacao/populacaoLA.csv' into table morgado.pop;
```
## 4.Selecionar os 10 primeiros registros da tabela pop
```
select * from morgado.pop limit 10;
```
## 5.Contar a quantidade de registros da tabela pop
```
select count(*) from morgado.pop;
```