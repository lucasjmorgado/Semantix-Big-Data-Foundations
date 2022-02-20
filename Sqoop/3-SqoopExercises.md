# Sqoop - Importação BD Employees- Otimização

Realizar com uso do MySQL

## 1. Criar a tabela cp_titles_date, contendo a cópia da tabela titles com os campos title e to_date
```
sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "create table cp_titles_date as (
select title, to_Date from employees.titles
)"

```
## 2. Pesquisar os 15 primeiros registros da tabela cp_titles_date
```
sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "select * from cp_titles_date limit 15"
```
## 3. Alterar os registros do campo to_date para null da tabela cp_titles_date, quando o título for igual a Staff
```
sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "update cp_titles_date set to_date = null where title = 'Staff'"
```
Realizar com uso do Sqoop - Importações no warehouse /user/hive/warehouse/db_test_<numero_questao> e visualizar no HDFS

## 4. Importar a tabela titles com 8 mapeadores no formato parquet
```
sqoop import --table titles --connect jdbc:mysql://database/employees --username root --password secret --warehouse-dir /user/hive/warehouse/db_test2_4 -m 8 --as-parquetfile

hdfs dfs -ls /user/hive/warehouse/db_test2_4/titles
hdfs dfs -cat /user/hive/warehouse/db_test2_4/titles/43c7ac84-0af2-4997-b151-d2211e927ea0.parquet | head -n 5

```
## 5. Importar a tabela titles com 8 mapeadores no formato parquet e compressão snappy
```
sqoop import --table titles --connect jdbc:mysql://database/employees --username root --password secret --warehouse-dir /user/hive/warehouse/db_test2_5 -m 8 --as-parquetfile --compress --compression-codec org.apache.hadoop.io.compress.SnappyCodec

hdfs dfs -ls /user/hive/warehouse/db_test2_5/titles
```
## 6. Importar a tabela cp_titles_date com 4 mapeadores (erro)

### Importar a tabela cp_titles_date com 4 mapeadores divididos pelo campo título no warehouse /user/hive/warehouse/db_test2_title
```
sqoop import --table cp_titles_date --connect jdbc:mysql://database/employees --username root --password secret --warehouse-dir /user/hive/warehouse/db_test2_6 -m 4 


"No primary key could be found for table cp_titles_date. Please specify one with --split-by or perform a sequential import with '-m 1'."

sqoop import -Dorg.apache.sqoop.splitter.allow_text_splitter=true --table cp_titles_date --connect jdbc:mysql://database/employees --username root --password secret --warehouse-dir /user/hive/warehouse/db_test2_title -m 4 --split-by title 
```
### Importar a tabela cp_titles_date com 4 mapeadores divididos pelo campo data no warehouse /user/hive/warehouse/db_test2_date
```
sqoop import -Dorg.apache.sqoop.splitter.allow_text_splitter=true --table cp_titles_date --connect jdbc:mysql://database/employees --username root --password secret --warehouse-dir /user/hive/warehouse/db_test2_date -m 4 --split-by date 

```
### Qual a diferença dos registros nulos entre as duas importações?
```
root@namenode:/# hdfs dfs -count -h /user/hive/warehouse/db_test2_title
           2            7              8.8 M /user/hive/warehouse/db_test2_title

root@namenode:/# hdfs dfs -ls -h -R /user/hive/warehouse/db_test2_title 
drwxr-xr-x   - root supergroup          0 2022-02-20 14:41 /user/hive/warehouse/db_test2_title/cp_titles_date
-rw-r--r--   3 root supergroup          0 2022-02-20 14:41 /user/hive/warehouse/db_test2_title/cp_titles_date/_SUCCESS
-rw-r--r--   3 root supergroup          0 2022-02-20 14:41 /user/hive/warehouse/db_test2_title/cp_titles_date/part-m-00000
-rw-r--r--   3 root supergroup    443.2 K 2022-02-20 14:41 /user/hive/warehouse/db_test2_title/cp_titles_date/part-m-00001
-rw-r--r--   3 root supergroup      2.2 M 2022-02-20 14:41 /user/hive/warehouse/db_test2_title/cp_titles_date/part-m-00002
-rw-r--r--   3 root supergroup        456 2022-02-20 14:41 /user/hive/warehouse/db_test2_title/cp_titles_date/part-m-00003
-rw-r--r--   3 root supergroup      5.8 M 2022-02-20 14:41 /user/hive/warehouse/db_test2_title/cp_titles_date/part-m-00004
-rw-r--r--   3 root supergroup    414.5 K 2022-02-20 14:41 /user/hive/warehouse/db_test2_title/cp_titles_date/part-m-00005



root@namenode:/# hdfs dfs -count -h /user/hive/warehouse/db_test2_date 
           2            5              7.7 M /user/hive/warehouse/db_test2_date

root@namenode:/# hdfs dfs -ls -h -R /user/hive/warehouse/db_test2_date 
drwxr-xr-x   - root supergroup          0 2022-02-20 14:43 /user/hive/warehouse/db_test2_date/cp_titles_date
-rw-r--r--   3 root supergroup          0 2022-02-20 14:43 /user/hive/warehouse/db_test2_date/cp_titles_date/_SUCCESS
-rw-r--r--   3 root supergroup      2.6 M 2022-02-20 14:43 /user/hive/warehouse/db_test2_date/cp_titles_date/part-m-00000
-rw-r--r--   3 root supergroup          0 2022-02-20 14:43 /user/hive/warehouse/db_test2_date/cp_titles_date/part-m-00001
-rw-r--r--   3 root supergroup          0 2022-02-20 14:43 /user/hive/warehouse/db_test2_date/cp_titles_date/part-m-00002
-rw-r--r--   3 root supergroup      5.1 M 2022-02-20 14:43 /user/hive/warehouse/db_test2_date/cp_titles_date/part-m-00003

--Particionar pelo date faz os campos nulos serem ignorados e apagados

```