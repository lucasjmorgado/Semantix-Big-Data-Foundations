# Commandos Hbase

## Estrutura de comandos
```
docker hbase_master
hbase shell
```


## Criar tabela
```
create 'nomeTabela','familia','familia'
create 'clientes',{NAME=>'endereco', VERSIONS=>2},{NAME=>'pedido'}
```


## Operações de tabela
```
list -> listar tabelas
describe 'nomeTabela' -> estrutura da tabela
drop 'nomeTabela' ou drop_all 'c.*' -> deletar tabelas
exists 'nomeTabela'
disable 'nomeTabela'
disable_all 'r.*'
enable 'nomeTabela'
is_disabled 'nomeTabela'
is_enable 'nomeTabela'
```

## Inserir dados
```
put 'nomeTabela','chave','familia:coluna','valor'
put 'clientes','emiranda','endereco:cidade'.'BH'
put 'clientes','emiranda','endereco:estado'.'MG'
put 'clientes','emiranda','pedido:data'.'2/2/2016'
put 'clientes','emiranda','pedido:nitem'.'1234D'
```

## Alterar dados
```
put 'clientes','emiranda','pedido:nitem'.'1234A'
```

## Leitura dados
```
1 registro -> Consultar pela chave -> get
Todos registro -> Consultar pela tabela -> scan
```

## Leitura dados get
```
get 'nomeTabela','chave'

get 'nomeTabela','chave',{COLUMNS=>['família']}
get 'clientes','emiranda',{COLUMNS=>['endereco']}

get 'clientes','emiranda',{COLUMNS=>['famiília:coluna']}
get 'clientes','emiranda',{COLUMNS=>['endereco:cidade']}
```

## Leitura dados scan
```
scan 'nomeTabela'

scan 'nomeTabela',{COLUMNS=>['família']}
scan 'clientes',{COLUMNS=>['endereco']}

scan 'clientes',{COLUMNS=>['famiília:coluna']}
scan 'clientes',{COLUMNS=>['endereco:cidade']}

scan 'clientes',{STARTROW=>'emi', COLUMNS=>['endereco:cidade']}
```

## Deletar dados 
```
deletar coluna

delete 'nomeTabela','chave','familia:coluna'
delete 'clientes','emiranda','endereco:cidade'

deletar família de coluna

delete 'nomeTabela','chave','familia'
delete 'clientes','emiranda','endereco'

deletar chave

deleteall 'nomeTabela','chave'
deleteall 'clientes','emiranda'
```