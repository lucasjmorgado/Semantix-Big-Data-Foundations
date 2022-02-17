# Sqoop
## Ingestão de dados
```
Processo de enviar/receber os dados locais para o sistema distribuído

Batch
    Sqoop

Stream
    Flume
    Kafka
```

## Sqoop
```
Ferramenta para transferir os dados entre o Hadoop e banco de dados relacionais

Sqoop = 'SQL to Hadoop'

Importar dados
    Banco de dados relacionais(RDBMS)
        MySQL, SQL Server, Oracle

Para HDFS, HIVE OU HBase
    Transformar dados em MapReduce
        Execução em paralelo
        Tolerância a falhas

Exportar dados 
    Armazenamento do Hadoop para um RDBMS

MySQL -> Sqoop Client -> MapReduce -> HDFS/Hive/HBase
```