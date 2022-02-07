# Hive
```
Outras ferramentas para análise de dados:

- Hive
- Impala
- Presto
- Spark

Hive permite acesso aos dados via SQL
    Data Warehouse construído em cima do Hadoop

Ótimo para realizar particionamentos de tabelas
```
## Componentes do Hive
```
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
```
## Formatos de arquivos
```
Conector para vários formatos

- Txt, csv
- Parquet
- Orc
- Avro

Não existe formato hive
```
## Estrutura dos dados
```
Database -> table -> partition -> bucket

exemplo de caminho: /user/hive/warehouse/banco.db/data=010119/000000_0
```
## HiveQL
```
Instruções SQL são transformadas internamente em Jobs de MapReduce
```
## Tabelas Hive
```
Dois tipos:

- Internas 
- Externas

Partição

- Não particionada
- Particionada
    Dinâmico e Estático
```
## Particionamento

```
Tabela não particionada 
    -Consultas precisam varrer todos os arquivos no diretório
        -Processo leto para grande tabelas

Tabela particionada
    -Consultas podem varrer apenas os dados de uma partição
        -Campo com registros duplicados
            -Estado, gênero, categoria, classe

Comandos
    - Partitioned by (<campo><type>)
    - Bucket -> Quantidade de dados que serão divididos
        - clustered by (<campo>) into <qtd> buckets;

Ex:
create table user(
    id int, 
    name string, 
    age int
)
partitioned by (data string)
clustered by (id) into 4 buckets;
```

## Tipos de particionamento

- Particionamento estático
```

Você cria partições manualmente

alter table logs add partition(data='2019-01-01')
```

- Particionamento dinâmico
```
Partições criadas automaticamente nos tempos de carregamento

insert overwrite table user_cidade partition (cidade) select * from user;

SET hive.exec.dynamic.partition = true;
SET hive.exec.dynamic.partition.mode = nonstrict;
```