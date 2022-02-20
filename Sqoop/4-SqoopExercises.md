## 1. Criar a tabela cp_rental_append, contendo a cópia da tabela rental com os campos rental_id e rental_date
```
sqoop eval --connect jdbc:mysql://database/sakila --username root --password secret --query "create table cp_rental_append as (select rental_id, rental_date from rental)"

```
## 2. Criar a tabela cp_rental_id e cp_rental_date, contendo a cópia da tabela cp_rental_append
```
sqoop eval --connect jdbc:mysql://database/sakila --username root --password secret --query "create table cp_rental_id as (select * from cp_rental_append)"

sqoop eval --connect jdbc:mysql://database/sakila --username root --password secret --query "create table cp_rental_date as (select * from cp_rental_append)"
```

Realizar com uso do Sqoop - Importações no warehouse /user/hive/warehouse/db_test3 e visualizar no HDFS

## 3. Importar as tabelas cp_rental_append, cp_rental_id e cp_rental_date com 1 mapeador
```
sqoop import --table cp_rental_append --connect jdbc:mysql://database/sakila --username root --password secret --warehouse-dir /user/hive/warehouse/db_test3_append -m 1 

sqoop import --table cp_rental_id --connect jdbc:mysql://database/sakila --username root --password secret --warehouse-dir /user/hive/warehouse/db_test3_id -m 1 

sqoop import --table cp_rental_date --connect jdbc:mysql://database/sakila --username root --password secret --warehouse-dir /user/hive/warehouse/db_test3_date -m 1 
```

Realizar com uso do MySQL

## 4. Executar o sql /db-sql/sakila/insert_rental.sql no container do database
```
$ docker exec -it database bash

$ cd /db-sql/sakila

$ mysql -psecret < insert_rental.sql
```
 

Realizar com uso do Sqoop - Importações no warehouse /user/hive/warehouse/db_test3 e visualizar no HDFS

## 5. Atualizar a tabela cp_rental_append no HDFS anexando os novos arquivos
```
sqoop import --table cp_rental_append --connect jdbc:mysql://database/sakila --username root --password secret --warehouse-dir /user/hive/warehouse/db_test3_append --append --split-by rental_id
```

## 6. Atualizar a tabela cp_rental_id no HDFS de acordo com o último registro de rental_id, adicionando apenas os novos dados.
```
sqoop eval --connect jdbc:mysql://database/sakila --username root --password secret --query "select * from cp_rental_append order by rental_id desc limit 1"

--Último registro 16049

sqoop import --table cp_rental_id --connect jdbc:mysql://database/sakila --username root --password secret --warehouse-dir /user/hive/warehouse/db_test3_id --incremental append --check-column rental_id --last-value 16049 --split-by rental_id

```

## 7. Atualizar a tabela cp_rental_date no HDFS de acordo com o último registro de rental_date, atualizando os registros a partir desta data.
```
sqoop eval --connect jdbc:mysql://database/sakila --username root --password secret --query "select * from cp_rental_append order by rental_id desc limit 1"

--Último registro 2005-08-23 22:50:12.0 

sqoop import --table cp_rental_date --connect jdbc:mysql://database/sakila --username root --password secret --warehouse-dir /user/hive/warehouse/db_test3_date --incremental lastmodified --merge-key rental_id --check-column rental_date --last-value '2005-08-23 22:50:12.0' --split-by rental_id
```

## Verificar
hdfs dfs -ls -R /user/hive/warehouse/db_test3_date/
