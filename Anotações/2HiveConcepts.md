# Hive

Outras ferramentas para análise de dados:

- Hive
- Impala
- Presto
- Spark

Hive permite acesso aos dados via SQL
    Data Warehouse construído em cima do Hadoop

Ótimo para realizar particionamentos de tabelas

## Componentes do Hive

- HCatalog

Camada de gerenciamento para o hadoop
Permite que usuários com diferentes ferramentas de processamento de dados leiam e gravem os dados

- WebHCat 

Servidor web para conectar com o Metastore Hive

- HiveServer2(HS2)

Serviço que permite aos clientes executar consultas no Hive

- Metastore

Todos os metadados das tabelas e partições do Hive são acessados através do Hive Metastore

- Beeline

Cliente Hive
Faz uso de JDBC para se conectar ao HiveServer2

## Formatos de arquivos

Conector para vários formatos

- Txt, csv
- Parquet
- Orc
- Avro

Não existe formato hive

## Estrutura dos dados

Database -> table -> partition -> bucket

exemplo de caminho: /user/hive/warehouse/banco.db/data=010119/000000_0

## HiveQL

Instruções SQL são transformadas internamente em Jobs de MapReduce

## Tabelas Hive

Dois tipos:

- Internas 
- Externas

Partição

- Não particionada
- Particionada
    Dinâmico e Estático
