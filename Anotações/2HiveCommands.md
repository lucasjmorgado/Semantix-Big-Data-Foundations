# Commandos Hive

## Estrutura sobre o bd

desc database <nomeBD>

## Estrutura sobre a tabela

desc formatted <nomeTabela>

## Criar bd com local diferente do conf. Hive

create database <nomeBanco> location "/diretorio"

## Adicionar Comentario

create database <nomeBanco> comment "descrição"

# Ex create

create database tes location "/user/hive/warehouse/test" comment "banco de dados para treinamento"

## Create tabela externa

create external table e_user(cod int, name string) location "/user/hive/warehouse/test"
drop table apaga apenas os metadados, dados ficam armazenados no sistema de arquivos

## Delimitadores

Row format delimited
fields terminated by '<delimitador>'
lines terminated by '<delimitador>'
\b Backspace, \n newline, |t tab

## Pular linhas na leitura do arquivo

tblproperties("skipp.header.line.count"="<numero de linhas>")

# Exemplo tabela externa

```
create external table user(
    id int, 
    name string,
    age int
)
row format delimited
fields terminated by '\t'
lines terminated by '\n'
stored as textfile
location '/user;cloudera/data/client'
```