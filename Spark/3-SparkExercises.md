# Spark - Exercícios da API Catalog

Realizar os exercícios usando a API Catalog.

## 1. Visualizar todos os banco de dados
```
spark.catalog.listDatabases.show(false)
```
## 2. Definir o banco de dados “seu-nome” como principal
```
spark.catalog.setCurrentDatabase("morgado")
```
## 3. Visualizar todas as tabelas do banco de dados “seu-nome”
```
spark.catalog.listTables.show()
```
## 4. Visualizar as colunas da tabela tab_alunos
```
spark.catalog.listColumns("tab_alunos").show()
```
## 5.  Visualizar os 10 primeiros registos da tabela "tab_alunos" com uso do spark.sql
```
spark.sql("select * from tab_alunos limit 10").show()
```