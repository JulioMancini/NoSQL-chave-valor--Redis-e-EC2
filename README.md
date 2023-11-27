# NoSQL-chave-valor--Redis-e-EC2
Projeto NoSQL com o objetivo de teste e aprendizado

# Tudo sobre oque é o Redis
```bash
https://aws.amazon.com/pt/elasticache/what-is-redis/#:~:text=Redis%20%C3%A9%20um%20acr%C3%B4nimo%20de,o%20melhor%20desempenho%20do%20mercado.
```

# Criando e configurando uma instância no EC2

* Procurar por EC2 na pesquisa

![foto ec2 1](https://github.com/JulioMancini/Modelo_Relacional-EC2-e-Postgres/assets/145502330/50938737-04f6-4bfc-8245-0d87b9aa43bf)


* procurar por instância e criar uma em Executar instância
* Criar um nome para instância
* escolher uma versão não tão atualizada (versão escolida: Ubuntu Serve 20.04 LTS (HMV), SSD Volume Type) versão gratuita

  ![ec2 2](https://github.com/JulioMancini/Modelo_Relacional-EC2-e-Postgres/assets/145502330/f9f0541d-203c-4e53-a075-8ea58c168c10)

* Arquitetura 64(x68)
* Tipo de instância não precisa alterar ( continuar com t2.micro)
* Criar uma chave
* permitir tráfego SSH
* Após a criação execute a instancia e salve a chave para poder fazer o acesso em SSH no Shell da maquina

![ec2 3](https://github.com/JulioMancini/Modelo_Relacional-EC2-e-Postgres/assets/145502330/3027e9ad-0b9f-441e-be8a-7c9cc988d9f8)

* Abra o Shell da maquina e posicione no diretório onde a chave está.
* Copiar e colar o comando (chave) diretamente do site da AWS

![ec2 4](https://github.com/JulioMancini/Modelo_Relacional-EC2-e-Postgres/assets/145502330/9997509b-8114-4d32-b5aa-74737ac3afbd)

[Pronto, agora voçê está conectado ao Linux e Ubuntu que está rodando em um servidor do AWS]![ec2 5](https://github.com/JulioMancini/Modelo_Relacional-EC2-e-Postgres/assets/145502330/5b33745e-7454-4777-b3a8-1f43635370c9)

## INSTALANDO REDIS

* Instalar redis

```bash
sudo snap install redis
```
* Atualizar a lista de pacotes

```bash
sudo apt-get update
```
* Instalar clientes

```bash
sudo apt install redis-tools
```
* Acessar o cliente

```bash
redis-cli
```
## CRIANDO STRINGS

tipo string, que nos traz a possibilidade de você armazenar uma chave associada a um valor. Esse valor é um texto, pode ser criado a chave e associar ela  

* Chave e Valor

```bash
SET 1 "Engenharia de Dados"
```
![1](https://github.com/JulioMancini/NoSQL-chave-valor--Redis-e-EC2/assets/145502330/02cdb82e-2e6b-40f4-b724-bd0b0074eb1a)

Agora eu posso recuperar um texto, uma string pela chave usando get.

* retorna

```bash
GET 1
```
![2](https://github.com/JulioMancini/NoSQL-chave-valor--Redis-e-EC2/assets/145502330/3fd73b03-a530-4bf5-a0d4-7d7b51bdecd3)

Existe a possibilidade também de incluir várias chaves simultaneamente. Para isso, eu uso M7.

* inclui várias chaves

```bash
MSET 1040 ANALISTA 1050 GERENTE 1060 TESTADOR
```
podemos testar a existencia da chave usando o exists. Ele retorna 1 se o a chave existe e 0 se não existe.

* Testar existencia
```bash
EXISTS 1
```
![3](https://github.com/JulioMancini/NoSQL-chave-valor--Redis-e-EC2/assets/145502330/afe1a2f9-023e-4d0d-af0d-4a9ddb19f9a8)

* Tipo de chave
 
```bash
TYPE 1
```

Podemos deletar a chave com o DEL e o numero da chave

* Exclui pela chave

```bash
DEL 1
```

Podemos definir a chava para expirar usando o `EXPIRE`

* Expiração posterior - SEGUNDOS

```bash
EXPIRE 1 5
```

* Expiração em milesegundos

```bash
PEXPIRE 1 5000
```
podemos verificar quanto tempo resta para expirar e remover a expiração

* Retonar tempo para expirar MILESEGUNDOS

```bash
PTTL 1
```
* Retonar tempo para expirar Segundos

```bash
TTL 1
```
* Remover expiração

```bash
PERSIST 1
```

Podemos atualizar o valor de uma String, vamos usar achave e valor: MSET 1040 ANALISTA, atulizar o valor para o nome "Engenheiro de Dados"

* Atualiza e retorna o valor antigo

```bash
GETSET 1040 "Engenheiro de Dados"
```

Podemos verificar o valor de varias chaves com o `MGET`. Basta colocar o comando e as chaves

* Retorna várias chaves

```bash
MGET 1 2 3 4
```

Podemos verificar o comprimento do valor. 

* tamanho do campo valor

```bash
STRLEN 1
```

![5](https://github.com/JulioMancini/NoSQL-chave-valor--Redis-e-EC2/assets/145502330/e2505440-b677-4e5c-86c6-a3a99840c0c5)

## CRIANDO HASHS (Conjunto de campos/valores, associados a uma chave)

Podemos criar uma chave com varios valores, semelhante a uma lista na linghagem de programação

* HASHS - chave + {campo valor} { camp valor}

```bash
HMSET CADASTRO NOME JOSE PROFISSAO ENGENHEIRO CIDADE "SANTA MARIA"
```

* Retorna todos chave + valor

```bash
HGETALL CADASTRO
```

![6](https://github.com/JulioMancini/NoSQL-chave-valor--Redis-e-EC2/assets/145502330/6cebcaf3-a690-4db2-993e-70b84bd7df4b)

Podemos excluir um campo (o valor será excluido junto)

* Exclui CAMPO e valor pelo CHAVE A NOME DO CAMPO

```bash
HDEL CADASTRO CIDADE
```

Retornado os dados podemos verificar a exclusão

* Retorna todos

```bash
HGETALL CADASTRO
```

![7](https://github.com/JulioMancini/NoSQL-chave-valor--Redis-e-EC2/assets/145502330/38960569-6e7b-4083-863b-9a7a225c6996)

* Retorna valor PELO NOME DO CAMPO

```bash
HMGET CADASTRO NOME PROFISSAO
```

* Retorna todos os VALORES - sem campo

```bash
HVALS CADASTRO
```

* Todo o hash

```bash
HGETALL CADASTRO
```

* Verifica existencia pelo campo

```bash
HEXISTS CADASTRO NOME
```

![8](https://github.com/JulioMancini/NoSQL-chave-valor--Redis-e-EC2/assets/145502330/4b72040a-5b06-4aa8-92cc-0f98f7b095a8)

* Retorna número de campos

```bash
HLEN CADASTRO
```

* Retonar lista de campos

```bash
HKEYS CADASTRO
```

* Saber o tipo

```bash
TYPE CADASTRO
```

![9](https://github.com/JulioMancini/NoSQL-chave-valor--Redis-e-EC2/assets/145502330/0fcaf9f4-0dc4-4c91-8c89-f4182d0b9010)

## CRIANDO LIST
Lista de strings com chave única que pode ser inseridas separadamente. Uma lista ou uma sequência de strings. Porém, elas estão associadas a uma chave única e também você pode inserir ou remover elementos nesta lista.

* Inclusão no inicio da lista
 
```bash
LPUSH 4545 SQLSERVER ORACLE POSTGRES MYSQL
```

Com o `TYPE` pode-se vereficar o tipo, se é ula lista ou não

* TIPO
  
```bash
TYPE 4545
```

Eu posso recuperar elementos individuais ou um intervalo, eu posso utilizar ele range. Vejam que eu posso definir aqui uma chave de início, uma chave de fim.

* Retorna intervalo
  
```bash
LRANGE 4545 0 3
```
![10](https://github.com/JulioMancini/NoSQL-chave-valor--Redis-e-EC2/assets/145502330/13471d4c-f8dc-419d-92a8-d26c2a9c27e2)

* Inserindo novos elementos no fim da lista
Essa ação é muito simples. Basta colocar RPUSH numero da chave e o elemento

 ```bash
RPUSH 4545 DB2
```

Podemos inserir Antes ou Depois de um determinado valor

* Insere antes de valor
 
 ```bash
LINSERT 4545 BEFORE FIREBIRD SQLITE
```

* Insere depois de valor

 ```bash
LINSERT 4545 AFTER ORACLE FIREBIRD
```
Vamos supor, então, que eu queira atualizar. Um elemento, o elemento da posição é indexado em zero

* Atualizar
  
 ```bash
LSET 4545 1 POSTGRESQL
```

Eu posso remover elementos também. Eu não preciso passar a posição do elemento porque ele vai remover o primeiro elemento

* Remove pelo inicio

 ```bash
LPOP 4545
```
Eu posso também remover pelo pelo fim.

* Remove pelo fim

```bash
RPOP 4545
```

## CRIANDO SETS

Agora vai vamos ver sets, que é uma coleção não ordenada, não repetida, é semelhante a uma lista, porém ela não tem uma ordenação. Então, ela não consegue inserir valores repetidos. Ela simplesmente vai ignorar se o valor tiver repetido.

* SETS - Coleção não ordenada, não repetida (empilhando elementos).

```bash
SADD 123 ELEMENTO1 ELEMENTO2 ELEMENTO3 ELEMENTO 4
```

Na mesma chave eu posso colocar mais elementos e vejam que diferente lá das listas.

```bash
SADD 123 ELEMENTO5 ELEMENTO6 ELEMENTO7 
```

Para recuperar os valores `SMEMBERS` e a chave

* Recupera valores
  
```bash
SMEMBERS 123 
```

* Número de Membros

```bash
SCARD 123 
```

* Verifica se um Valor é Membro

```bash
SISMEMBER 13 ELEMENTO1
```

* Removendo

```bash
SREM 123 ELEMENTO1
```

* Adicionando outro set

```bash
SADD 111 ELEMENTO8 ELEMENTO9 ELEMENTO10 
```

Podemos verificar a diferença entre dois conjuntos. Parra isso usamos o `SDIFF` A chave de um elemento é a chave do outro elemento que eu quero buscar a diferença.

```bash
SDIFF 123 111 
```

## CRIANDO ZSETS

tipo especial de conjunto, porém eles são ordenados e baseados em um escore. Então, além da chave e do valor, você define o score. Para criar basta colocar o ZADD + chave + peso + valor

* Ordenados baseados em score - não repetido

```bash
ZADD 1 0 ELEMENTO1
ZADD 1 5 ELEMENTO2
ZADD 1 4 ELEMENTO3 
```

* Número de Elementos

```bash
ZCARD 1 
```

* Índice de um membro

 ```bash
ZRANK 1 ELEMENTO3 
```

 * Conta membros com scores entre... retorna 3

```bash
ZCOUNT 1 0 5
```

* Retorna o score de um membro

```bash
ZSCORE 1 ELEMENTO3 
```

* Retorna Membros pelo Índice

```bash
ZRANGE 1 0 2 
```

* Remove

```bash
ZREM 1 ELEMENTO3
```

## CONTROLANDO TRANSAÇÕES

Lembrando que o conceito de transações é semelhante ao de um banco de dados relacional, porém que as palavras chave são um pouco diferentes.

1. MULTI:  Marca o inicio das transações
2. EXEC: Executa todos os comandos depois de MULTI
3. DISCARD: Descarta todos os comandos depois de MULTI

* iniciando o controle de transação

```bash
MULTI
```

Exemplo 

```bash
SET 145 "REDIS NOSQL"
SET 146 "MONGODB NOSQL"
```

DISCARD teste
  
```bash
SET 1213 "REDIS NOSQL"
SET 1214 "MONGODB NOSQL"
```
