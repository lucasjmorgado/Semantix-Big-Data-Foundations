# Commandos Sqoop

## Estrutura de comandos
```
sqoop <commando>
```

- help
```
sqoop help import
```
- version
- import
- import-all-tables(importar todas as tabelas do banco de dados)
- export
- validation
- job(automatizar importações/exportações)
- metastore
- merge
- codegen
- create-hive-table
- eval(query no banco de dados externo)
```
sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "select *  from employees limit 15"
```
- list-databases
```
sqoop list-databases --connect jdbc:mysql://database --username usuario --password senha
```
- list-tables
```
sqoop list-tables --connect jdbc:mysql://database --username usuario --password senha
```