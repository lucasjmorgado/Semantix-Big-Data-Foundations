# Spark
## Conceito
```
Suporta MapReduce, streaming
Execução em memória
Compatível com Hadoop
    Funciona com YARN

Linguagem Scala(criada pelo spark e mais performática, geralmente 30% em relação ao python), Java, Python e R
```

## Ferramentas
```
Spark - etl e batch
Spark SQL - consulta em dados estruturados
Spark Streaming - processamento de stream
Spark MLib - Machine learning
Spark GraphX - Processamento de grafos
```

## Shell
```
pyspark -> python
spark-shell -> scala
```

## Dataframe
```
representação de dados no spark
    transformação e ação

Create dataframe and read file
val <dataframe> = spark.read.<formato>("<arquivo>")
<formato>
    jdbc(jdbcUrl,"bd.tabela", connectionProperties)
    parquet("arquivo.parquet")

<arquivo>
    "diretorio/"
    "diretorio/*.log"
    "arq*"

EX:
val userDF = spark.read.json("user.json")
val userDF = spark.read.format("json").load("user.json")
```

## Ações Dataframe
```
<dataframe>.<ação>()
clienteDF.first()
clienteDF.show(5)

count - número de linhas
first - retorna primeira linha
show(n) - exisbe primeiras n linhas da tabela
distincts - retorna registros deduplicados
write - salva os dados
    save("arquivoParquet")
    json("arquivoJson")
    csv("arquivoCSV")
    saveAsTable("tableHive")
        (/user/hive/warehouse)
printSchema() - estrutura dos dados

dadosDF.write.save("outputData")
hdfs dfs -ls /user/cloudera/outputData

SCALA> dadosDF.write.mode("append").option("path","/user/root").saveAsTable("outputData")
```

## Transformação Dataframe
```
Imutáveis
    Dados no DataFrame nunca são modificados

select 
where
orderBy
groupBy
join
limit(n)

val prodQtdDF = propdDF.select("nome","qtd")
val 50prodQtdDF = propdDF.where("qtd > 50")
prodDF.select("nome","qtd").where("qtd > 50").orderBy("nome").show()
val DF = prodDF.select("nome","qtd").where("qtd > 50").orderBy("nome")

groupBy
    count
    max
    min
    mean
    sum
    pivot
    agg

Acessar atributo do dado

    prodDF.select("nome","qtd").show()
    prodDF.select($"nome",$"qtd" * 0,1).show()
    prodDF.where(prodDF("nome").startsWith("A")).show()
```    

## Inferir schema
```
Spark não seta tipos de dados a não ser que vc peça

val sDF = spark.read.option("inferSchema","true").csv("setor.csv").printSchema()

Dados com cabeçalho

val sDF = spark.read.option("inferSchema","true").option("header","true").csv("setor.csv").printSchema()
```

## Joins
```
inner join

val clienteDF = spark.read.option("header","true").csv("cliente.csv")
val cidadeDF = spark.read.option("header","true").csv("cidade.csv")
clienteDF.join(cidadeDF,"id_c").show()

left outer join

val clienteDF = spark.read.option("header","true").csv("cliente.csv")
val cidadeDF = spark.read.option("header","true").csv("cidade.csv")
clienteDF.join(cidadeDF,clienteDF("id_c")===cidadeDF("id_c"), "left_outer").show()
```

## Spark SQL Queries
```
val myDF = spark.sql("select * from people") --> query apontando para o banco de dados hive default
myDF.printSchema()
myDF.show()

val testDF = spark.sql("select * from json.`/bd/tabela.json`") 
```

## Spark SQL Views
```
View Regular -> apenas uma seção spark
View Global -> multiplas seções spark

Criar uma view

DataFrame.createTempView(view-name)
DataFrame.createOrReplaceTempView(view-name)

val clienteDF = spark.read.json("cliente.json").createTempView("clienteView")
val tabDF = spark.sql("select * from clienteView").show(10)
```

## API Catalog
```
spark.catalog

listDatabases
listTables
setCurrentDatabase(nomeDB)
listColumns(nomeTabela)
dropTempView(nomeView)

setCurrentDatabase(morgs)
```
