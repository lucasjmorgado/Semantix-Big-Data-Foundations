## 1. Iniciar o cluster de Big Data
```
cd docker-bigdata
docker-compose up -d
```
## 2. Baixar os dados dos exercícios do treinamento
```
cd input
sudo git clone https://github.com/rodrigo-reboucas/exercises-data.git
```
## 3. Acessar o container do namenode
```
docker exec -it namenode bash
```
## 4. Criar a estrutura de pastas apresentada a baixo pelo comando: $ hdfs dfs -ls -R /
```
user/aluno/<nome>data
user/aluno/<nome>recover
user/aluno/<nome>delete

hdfs dfs -mkdir / user/aluno/morgado/data
hdfs dfs -mkdir / user/aluno/morgado/recover
hdfs dfs -mkdir / user/aluno/morgado/delete
```

## 5. Enviar a pasta “/input/exercises-data/escola” e o arquivo “/input/exercises-data/entrada1.txt” para  data
```
hdfs dfs -put /input/exercises-data/escola/ /user/aluno/morgado/data
hdfs dfs -put /input/exercises-data/entrada1.txt /user/aluno/morgado/data
```
## 6. Mover o arquivo “entrada1.txt” para recover
```
hdfs dfs -mv /user/aluno/morgado/data/entrada1.txt /user/aluno/morgado/recover
```
## 7. Baixar o arquivo do hdfs “escola/alunos.json” para o sistema local /
```
hdfs dfs -get /user/aluno/morgado/data/escola/alunos.json /
```
## 8. Deletar a pasta recover
```
hdfs dfs -rm -R /user/aluno/morgado/recover
```
## 9. Deletar permanentemente o delete
```
hdfs dfs -rm -skipTrash -R /user/aluno/morgado/delete
```
## 10. Procurar o arquivo “alunos.csv” dentro do /user
```
hdfs dfs -find /user -iname alunos.csv
```
## 11. Mostrar o último 1KB do arquivo “alunos.csv”
```
hdfs dfs -tail /user/aluno/morgado/data/escola/alunos.csv
```
## 12. Mostrar as 2 primeiras linhas do arquivo “alunos.csv”
```
hdfs dfs -cat /user/aluno/morgado/data/escola/alunos.csv | head -n 2
```
## 13. Verificação de soma das informações do arquivo “alunos.csv”
```
hdfs dfs -checksum /user/aluno/morgado/data/escola/alunos.csv 
```
## 14. Criar um arquivo em branco com o nome de “test” no data
```
hdfs dfs -touchz /user/aluno/morgado/data/test
```
## 15. Alterar o fator de replicação do arquivo “test” para 2
```
hdfs dfs -setrep 2 /user/aluno/morgado/data/test
```
## 16. Ver as informações do arquivo “alunos.csv”
```
hdfs dfs -stat %r /user/aluno/morgado/data/escola/alunos.csv -> replicação
hdfs dfs -stat %o /user/aluno/morgado/data/escola/alunos.csv -> tamanho do bloco
```
## 17. Exibir o espaço livre do data e o uso do disco
```
hdfs dfs -df -h /user/aluno/morgado/data/
```