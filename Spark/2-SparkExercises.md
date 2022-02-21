# Spark - Exercícios de Esquema e Join
## 1. Criar o DataFrame alunosDF para ler o arquivo no hdfs “/user/aluno/<nome>/data/escola/alunos.csv” sem usar as “option”
```
val alunosDF = spark.read.csv("/user/aluno/morgado/data/escola/alunos.csv")
```
## 2. Visualizar o esquema do alunosDF
```
alunosDF.printSchema()
```
## 3. Criar o DataFrame alunosDF para ler o arquivo “/user/aluno/<nome>/data/escola/alunos.csv” com a opção de Incluir o cabeçalho
```
val alunosDF = spark.read.option("header","true").csv("/user/aluno/morgado/data/escola/alunos.csv")
```
## 4. Visualizar o esquema do alunosDF
```
alunosDF.printSchema()
```
## 5. Criar o DataFrame alunosDF para ler o arquivo “/user/aluno/<nome>/data/escola/alunos.csv” com a opção de Incluir o cabeçalho e inferir o esquema
```
val alunosDF = spark.read.option("inferSchema","true").option("header","true").csv("/user/aluno/morgado/data/escola/alunos.csv")
```
## 6. Visualizar o esquema do alunosDF
```
alunosDF.printSchema()
```
## 7. Salvar o DaraFrame alunosDF como tabela Hive “tab_alunos” no banco de dados <nome>
```
alunosDF.write.saveAsTable("morgado.tab_alunos")
```
## 8. Criar o DataFrame cursosDF para ler o arquivo “/user/aluno/<nome>/data/escola/cursos.csv” com a opção de Incluir o cabeçalho e inferir o esquema
```
val cursosDF = spark.read.option("inferSchema","true").option("header","true").csv("/user/aluno/morgado/data/escola/cursos.csv")
```
## 9. Criar o DataFrame alunos_cursosDF com o inner join do alunosDF e cursosDF quando o id_curso dos 2 forem o mesmo
```
val alunos_cursosDF = alunosDF.join(cursosDF,"id_curso")
```
## 10. Visualizar os dados, o esquema e a quantidade de registros do alunos_cursosDF
```
alunos_cursosDF.show(4)
alunos_cursosDF.printSchema()
alunos_cursosDF.count()

```
