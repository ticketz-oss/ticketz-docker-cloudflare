Instalação local do Ticketz
===========================

O Ticketz é basicamente composto por dois containers, eles podem ser instalados de diversas formas.

**A instalação seguindo este guia não instala o código fonte. Ela instala as imagens que foram compiladas pelo serviço Github Actions**, caso deseje fazer alterações no código é necessário seguir o guia de instalação a partir do fonte, conforme instruções no [Projeto Ticketz](https://github.com/ticketz-oss/ticketz).

Este repositório contém um exemplo para instalação local, utilizando
o protocolo http (sem criptografia), para ser utilizado no localhost ou até mesmo em uma rede local.

> ##### ATENÇÃO
> 
> A utilização em rede local sem criptografia pode expôr senhas e também a comunicação entre os usuários

Preparação do ambiente
----------------------

### Docker

#### Windows

Para execução no Windows é necessário ter instalado o [Docker Desktop](https://www.docker.com/products/docker-desktop/).

#### Linux

Para execução no Linux é necessário ter o Docker instalado. É recomendada a utilização do Docker a partir do projeto oficial.

A forma mais rápida de instalar o Docker no Linux é através do seguinte comando (estando como root):

```bash
curl -sSL https://get.docker.com | sh
```

### Download do projeto

O conteúdo deste repositório pode ser colocado em uma pasta, preferencialmente com o nome de `ticketz-docker-local`

Configuração
------------

Todos os comandos a seguir devem ser digitados estando dentro da pasta deste projeto, utilizando a linha de comando no Terminal do Linux como root ou no Windows Powershell.

Os arquivos `example.env-backend` e `example.env-frontend` devem ser copiados para `.env-backend` e `.env-frontend` respectivamente.

Para utilizar acessando como localhost isso é tudo o que precisa. Caso queira utilizar em rede local através de um IP interno (por ex. `192.168.0.10`) é necessário editar ambos os arquivos substituindo `localhost` pelo endereço desejado. Também é possível alterar a porta.

Execução
--------

Depois de copiados e configurados os arquivos `.env-backend` e `.env-frontend` basta executar o comando:

```bash
docker compose up -d
```

Em alguns minutos o sistema estará no ar no endereço configurado.

O login padrão é `admin@ticketz.host` e a senha é `123456`

Desligando o Serviço
--------------------

Caso deseje encerrar a execução do Ticketz basta digitar o comando:

```bash
docker compose down
```

Para inicializar novamente basta repetir o comando descrito no item anterior.

Atualizações
------------

### Atualização manual

Para atualizar o Ticketz basta abrir o Terminal do Linux ou Windows Powershell, posicionar-se na pasta de instalação e digitar a seguinte sequência de comandos:

```bash
docker compose pull

docker compose down

docker compose up -d
```

### Ativando atualizações automáticas

É possível ativar as atualizações automáticas, que serão executadas sempre que o projeto Ticketz tiver uma nova versão lançada.

Para ativar essa funcionalidade basta acessar o Terminal do Linux ou Windows Powershell, posicionar-se na pasta do projeto e digitar o seguinte comando:

```bash
docker compose up watchtower
```
