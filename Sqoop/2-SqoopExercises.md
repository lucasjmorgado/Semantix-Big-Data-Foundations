# Sqoop - Importação BD Employees
## 1. Pesquisar os 10 primeiros registros da tabela employees do banco de dados employees
```
sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "select * from employees.employees limit 10"
```
## 2. Realizar as importações referentes a tabela employees e para validar cada questão,  é necessário visualizar no HDFS*

### Importar a tabela employees, no warehouse  /user/hive/warehouse/db_test_a
```
sqoop import --table employees --connect jdbc:mysql://database/employees --username root --password secret --warehouse-dir /user/hive/warehouse/db_test_a

hdfs dfs -cat /user/hive/warehouse/db_test_a/employees/part-m-00001 | head -n 5
```
### Importar todos os funcionários do gênero masculino, no warehouse  /user/hive/warehouse/db_test_b
```
sqoop import --table employees --connect jdbc:mysql://database/employees --username root --password secret --warehouse-dir /user/hive/warehouse/db_test_b --where "gender='m'"

hdfs dfs -cat /user/hive/warehouse/db_test_b/employees/part-m-00001 | head -n 5
```
### importar o primeiro e o último nome dos funcionários com os campos separados por tabulação, no warehouse  /user/hive/warehouse/db_test_c
```
sqoop import --table employees --connect jdbc:mysql://database/employees --username root --password secret --warehouse-dir /user/hive/warehouse/db_test_c --columns "first_Name,last_Name" --fields-terminated-by '\t'

hdfs dfs -cat /user/hive/warehouse/db_test_c/employees/part-m-00001 | head -n 5
```
### Importar o primeiro e o último nome dos funcionários com as linhas separadas por “ : ” e salvar no mesmo diretório da questão 2.C
```
sqoop import --table employees --connect jdbc:mysql://database/employees --username root --password secret --warehouse-dir /user/hive/warehouse/db_test_c --columns "first_Name,last_Name" --fields-terminated-by ':' -delete-target-dir

hdfs dfs -cat /user/hive/warehouse/db_test_c/employees/part-m-00001 | head -n 5
```


* Dica para visualizar no HDFS:
$ hdfs dfs -cat /.../db_test/nomeTabela/part-m-00000 | head -n 5