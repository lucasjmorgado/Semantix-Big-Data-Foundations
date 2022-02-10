# Commandos Hive

## Estrutura sobre o bd
```
desc database <nomeBD>
```
## Estrutura sobre a tabela
```
desc formatted <nomeTabela>
```
## Criar bd com local diferente do conf. Hive
```
create database <nomeBanco> location "/diretorio"
```
## Adicionar Comentario
```
create database <nomeBanco> comment "descrição"
``` 
# Ex create
```
create database tes location "/user/hive/warehouse/test" comment "banco de dados para treinamento"
```
## Create tabela externa
```
create external table e_user(cod int, name string) location "/user/hive/warehouse/test"
drop table apaga apenas os metadados, dados ficam armazenados no sistema de arquivos
```
## Delimitadores
```
Row format delimited
fields terminated by '<delimitador>'
lines terminated by '<delimitador>'
\b Backspace, \n newline, |t tab
```
## Pular linhas na leitura do arquivo
```
tblproperties("skipp.header.line.count"="<numero de linhas>")
```
# Exemplo tabela externa

```
create external table user(
    id int, 
    name string,
    age int
)
row format delimited
fields terminated by '\t'
lines terminated by '\n'
stored as textfile
location '/user/cloudera/data/client'
```

## Inserir dados
```
insert into table <nomeTabela> partition(<partition>='<value>') values(<campo>,<value>);

insert into users partition(data=now())values(10,'rodrigo');
```

## Carregar dados no sistema de arquivos local
```
load data inpath <diretorio> into table <nomeTabela>;

load data local inpath '/home/cloudera/data/test' into alunos; -> arquivos máquina local

load data inpath '/home/cloudera/data/test' into alunos; -> arquivos dentro do hdfs
```

## Create view
```
create view <nomeView> as select * from nome_table;
```

## Create Particionamento

```
- Partitioned by (<campo><type>)
- Bucket -> clustered by (<campo>) into <qtd> buckets;

Ex:
create table user(
    id int, 
    name string, 
    age int
)
partitioned by (data string)
clustered by (id) into 4 buckets;
```
- Particionamento estático
```
alter table logs add partition(data='2019-01-01')
```
- Particionamento dinâmico
```
insert overwrite table user_cidade partition (cidade) select * from user;
SET hive.exec.dynamic.partition = true;
SET hive.exec.dynamic.partition.mode = nonstrict;
```

## Comandos Partição
- Visualizar partições de uma tabela
```
show partitions user;
```
- Excluir partições de uma tabela
```
alter table user drop partition (city='SP');
```
- Alterar nome de partição de uma tabela
```
alter table user partition city rename to partiton state;
```
- Reparar partições que foram alteradas no HDFS
```
msck rapair table <nomeTabela>; 
```

## Stored as
```
stored as <fileType>
TEXTFILE
ORC
PARQUET
AVRO
JSONFILE
```

## TIpos de compressão
```
Se o arquivo mapred-site.xml não estiver configurado pode setar manualmente
hive> SET hive.exec.compress.output=true;
hive> SET mapred.output.compression.codec= codec;
hive> SET mapred.output.compression.type=BLOCK;

- Codec:

gzip: org.apache.hadoop.io.compress.GzipCodec
bzip2: org.apache.hadoop.io.compress.BZip2Codec
LZO: com.hadoop.compression.lzo.LzopCodec
Snappy: org.apache.hadoop.io.compress.SnappyCodec
Deflate: org.apache.hadoop.io.compress.DeflateCodec

Adicionar o parâmetro compress em tblproperties na criação da tabela

stored as <formatoArquivo> tblproperties(' formatoArquivo.compress’=‘<CompressaoArquivo>’);

- GZIP
- BZIP2
- LZO
- SNAPPY
- DEFLATE
```
## Exemplo tabela com partição e compmressão
```
create table user(
id int,
name String,
age int
)
partitioned by (data String)
clustered by (id) into 256 buckets
stored as parquet tblproperties('parquet.compress'='SNAPPY');
```