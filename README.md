# NoSQL-chave-valor--Redis-e-EC2
Projeto NoSQL com o objetivo de teste e aprendizado

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
podemos tstar a existencia da chave usando o exists. Ele retorna 1 se o a chave existe e 0 se não existe.

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
