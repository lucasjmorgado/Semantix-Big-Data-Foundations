# Exercícios Hive 4
## 1. Selecionar os 10 primeiros registros da tabela nascimento pelo ano de 2016
```
select * from morgado.nascimento where ano = 2016 limit 10;
```
## 2. Contar a quantidade de nomes de crianças nascidas em 2017
```
select count(distinct(nome)) from morgado.nascimento where ano = 2017;
```
## 3. Contar a quantidade de crianças nascidas em 2017
```
select sum(frequencia) from morgado.nascimento where ano = 2017
```
## 4. Contar a quantidade de crianças nascidas por sexo no ano de 2015
```
select sum(frequencia),sexo from morgado.nascimento where ano = 2015 group by sexo;
```
## 5. Mostrar por ordem de ano decrescente a quantidade de crianças nascidas por sexo
```
select sum(frequencia),sexo, ano from morgado.nascimento group by sexo,ano order by ano,sexo desc;
```
## 6. Mostrar por ordem de ano decrescente a quantidade de crianças nascidas por sexo com o nome iniciado com ‘A’
```
select sum(frequencia),sexo, ano from morgado.nascimento where nome like 'A%' group by sexo,ano order by ano desc;
```
## 7. Qual nome e quantidade das 5 crianças mais nascidas em 2016
```
select nome, max(frequencia) as qtde from morgado.nascimento where ano = 2016 group by nome order by qtde desc limit 5;
```
## 8. Qual nome e quantidade das 5 crianças mais nascidas em 2016 do sexo masculino e feminino
```
select nome, max(frequencia) as qtde, sexo from morgado.nascimento where ano = 2016 group by nome,sexo order by qtd desc limit 5;
```