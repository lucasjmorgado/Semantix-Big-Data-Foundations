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

## Importar tabela
```
sqoop import --table tabela --connect <caminhoDB> --username --password
```

## Importar tabela
```
sqoop import ... --columns "nomeColuna1,nomeColuna2"
```

## Importar linhas
```
sqoop import ... --where "state='sp'"
```

## Armazenar em um diretório específico
```
sqoop import ... --target-dir /user/root/dir -> insere em /user/root/dir
sqoop import ... --warehouse-dir /user/root/dir -> insere em /user/root/dir/nomeTabela

--Caso seja necessário sobrescrever o diretorio

sqoop import ... --warehouse-dir /user/root/dir -delete-target-dir

--Caso seja necessário anexar o diretorio

sqoop import ... --warehouse-dir /user/root/dir -append
```

## Armazenar arquivos com delimitadores específicos
```
--fields-terminated-by <delimitador>
--lines-terminated-by <delimitador>
```

## Paralelismo Mapeadores
```
sqoop import ... -m 2

--Dividir mapeadores em colunas sem chave

sqoop import ... --split-by: id
```

## Paralelismo Valores Nulos
```
--null-non-string '-1'
--null-string 'NA'
```

## Importar arquivo definindo formato de arquivo
```
sqoop import ... --as-textfile
sqoop import ... --as-parquetfile
sqoop import ... --as-avrodatafile
```

## Comprimir arquivos
```
sqoop import ... --compress --compression-codec <codec>
```

## Jobs
```
-- Criar jobs
sqoop job --create myjob

-- List jobs
sqoop job --list

-- Show details jobs
sqoop job --show myjob

-- Execc jobs
sqoop job --exec myjob

-- Delete jobs
sqoop job --delete myjob
```

## Append
```
-- Anexar todos os dados
sqoop import ... --append --where 'id_venda>10'

-- Anexar apenas os dados novos(incrementa em relação a uma coluna e um valor)
sqoop import ... --incremental append --check-column id_venda --last_value 50
```

## lastmodified
```
-- Sobrescrever os dados, em relação a uma coluna e um valor de dadta e hora
sqoop import ... --incremental lastmodified --merge-key data_id --check-column data_venda --last_value '2021-01-18'
```

## Importar tabelas no Hive
```
--hive-import
--hive-overwrite
--create-hive-table

EX:

sqoop import --table employees --connect jdbc:mysql://database/employees --username root --password secret --warehouse-dir /user/hive/warehouse/teste.db --hive-import --create-hive-table --hive-table teste.user
```

## Exportar dados do HDF para o RDBMS
```
--exmport-dir <dir>
--table <dir>
--update-mode 
    updateonly -> cada registro é transformado em um insert
    allowinsert -> atualiza as linhas se não existirem na tabela ou insere

EX:
criar a tabela no SGBD

sqoop export --table employees --connect jdbc:mysql://database/employees --username root --password secret --export-dir /user/root/recommended_output --update-mode allowinsert --table product_recommendations

```