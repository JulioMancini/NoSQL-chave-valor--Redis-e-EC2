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
