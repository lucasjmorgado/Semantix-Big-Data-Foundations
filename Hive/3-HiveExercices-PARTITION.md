# Exercícios Hive 3
## 1. Criar o diretório “/user/aluno/<nome>/data/nascimento” no HDFS
```
hdfs dfs -mkdir /user/aluno/morgado/data/nascimento
```
## 2. Criar e usar o Banco de dados <nome>
```
beeline -u jdbc:hive2://localhost:10000
create database morgado;
use morgado;
```
## 3. Criar uma tabela externa no Hive com os parâmetros:
    a) Tabela: nascimento
    b) Campos: nome (String), sexo (String) e frequencia (int)
    c) Partição: ano
    d) Delimitadores:
        i) Campo ‘,’
        ii)  Linha ‘\n’
    e) Salvar
        i) Tipo do arquivo: texto
        ii) HDFS: '/user/aluno/<nome>/data/nascimento’
```
create external table nascimento(
    nome string,
    sexo string,
    frequencia int
)
partitioned by (ano int)
row format delimited
fields terminated by ','
lines terminated by '\n'
stored as textfile
location "/user/aluno/morgado/data/nascimento";
```
## 4.Adicionar partição ano=2015
```
alter table morgado.nascimento add partition(ano=2015);
```
## 5.Enviar o arquivo local “input/exercises-data/names/yob2015.txt” para o HDFS no diretório /user/aluno/<nome>/data/nascimento/ano=2015
```
ctrl+d
docker exec -it namenode bash
hdfs dfs -put input/exercises-data/names/yob2015.txt /user/aluno/morgado/data/nascimento/ano=2015
```
## 6.Selecionar os 10 primeiros registros da tabela nascimento no Hive
```
ctrl+d
docker exec -it hive-server bash
select * from morgado.nascimento limit 10;
```
## 7.Repita o processo do 4 ao 6 para os anos de 2016 e 2017.
```
alter table morgado.nascimento add partition(ano=2016);
alter table morgado.nascimento add partition(ano=2017);
ctrl+d
docker exec -it namenode bash
hdfs dfs -put input/exercises-data/names/yob2016.txt /user/aluno/morgado/data/nascimento/ano=2016
hdfs dfs -put input/exercises-data/names/yob2017.txt /user/aluno/morgado/data/nascimento/ano=2017
ctrl+d
docker exec -it hive-server bash
beeline -u jdbc:hive2://localhost:10000
select * from morgado.nascimento where ano=2016 limit 10;
select * from morgado.nascimento where ano=2017 limit 10;
```