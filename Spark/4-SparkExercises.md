# Spark - Exercícios de SQL Queries vs Operações de DataFrame

Realizar as seguintes consultas usando SQL queries e transformações de DataFrame na tabela “tab_alunos” no banco de dados <nome>

## 1. Visualizar o id e nome dos 5 primeiros registros
```
spark.read.table("morgado.tab_alunos").show(5)
spark.sql("select * from morgado.tab_alunos limit 5").show()
```
## 2. Visualizar o id, nome e ano quando o ano de ingresso for maior ou igual a 2018
```
spark.read.table("morgado.tab_alunos").select("id_discente","nome","ano_ingresso").where("ano_ingresso>=2018").show()
spark.sql("select id_discente, nome, ano_ingresso from morgado.tab_alunos where ano_ingresso>=2018").show()
```
## 3. Visualizar por ordem alfabética do nome o id, nome e ano quando o ano de ingresso for maior ou igual a 2018
```
spark.read.table("morgado.tab_alunos").select("id_discente","nome","ano_ingresso").where("ano_ingresso>=2018").orderBy($"nome".desc).show()
spark.sql("select id_discente, nome, ano_ingresso from morgado.tab_alunos where ano_ingresso>=2018 order by nome desc").show()
```
## 4. Contar a quantidade de registros do item anterior
```
spark.read.table("morgado.tab_alunos").select("id_discente","nome","ano_ingresso").where("ano_ingresso>=2018").orderBy($"nome".desc).count()
spark.sql("select id_discente, nome, ano_ingresso from morgado.tab_alunos where ano_ingresso>=2018 order by nome desc").count()

```