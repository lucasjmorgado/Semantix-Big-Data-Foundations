# File Formats
## Tipos de arquivo

- Text file
- Sequence File
- RC File
- ORC File
- Avro
- Parquet

## Sequence File
```
Arquivo de sequencia Hadoop, formado por pares de chave e valor
Mais eficiente que o arquivo texto pois armazena em dados binários
```

## Avro
```
Utilizado para trafegar dados pela rede
Armazenas dados e metadados
Suporta MapReduce e evolução de schema
```

## ORC File
```s
Optimized Row Colunnar file
Projetado para otimizar desempenho do hive
    Formados por faixas e grupos de linhas
```

## Parquet File
```
Formado por grupo de colunas
Suporta mapReduce
Evolução de Schema 
É processado pelo impala e spark
```

# Compressão de dados
##  Armazenamento x Velocidade de leitura
```
ZLIB(GZip)
    Alta compressão, lento
Snappy
    Baixa compressão, rápido
```