## Enviar arquivo ou diretório
```
    put <src><dst>
```
## Receber arquivo ou diretório
```
    get <src><dst>
        -f substitui arquivo
```
## Uso do disco
```
    du -h <diretório>
```
## Espaço Livre
```
    df -h <diretório>
```
## Informações do diretório
```
    stat <diretório>
        hdfs dfs -stat %r name.txt -> Fator de Replicação
        hdfs dfs -stat %o name.txt -> Tamanho do bloco
```
## Contar numero de diretórios, arquivos e tamanho de arquivos
```
    count -h <diretório>
```
## Esvaziar lixeira
```
    expunge 
```
## Alterar o fator de replicação do arquivo
```        
    setrep <n repetições> <arquivo>
```
## Mostra o último 1kb do arquivo no console
```
    hdfs dfs -tail name.txt -> final do arquivo
    hdfs dfs -cat name.txt | head -n 1
```
## Localiza todos os arquivos que correspondem à expressão
```
        find <caminho><procura> -print

            hdfs dfs -find / -name data -> procura arquivo com nome data not case sensitive
            hdfs dfs -find / -iname data -> procura arquivo com nome data case sensitive
```