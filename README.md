Ticketz usando túnel Zero Trust da Cloudflare
=============================================

O Ticketz é basicamente composto por dois containers, eles podem ser instalados de diversas formas.

Este repositório contém um exemplo para instalação utilizando o serviço de
túnel "zero trust" da Cloudflare. Pode ser instalado em qualquer sistema
que suporte Docker

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

O conteúdo deste repositório pode ser colocado em uma pasta, preferencialmente com o nome de `ticketz-docker-cloudflare`

Se preferir pode baixar utilizando o git:

```
git clone https://github.com/ticketz-oss/ticketz-docker-cloudflare
```

Configuração da Cloudflare
--------------------------

### Pré requisito

Ter um domínio hospedado na Cloudflare - essa parte fica fora do escopo desse guia

### Criação do túnel

No painel inicial da Cloudflare, entrar em "Zero Trust" no menu da esquerda.

Selecionar a opção "Redes -> Túneis"

Clicar em "+ Criar um Túnel"

Selecionar o tipo "Cloudflared", nomear o túnel e salvar

O Túnel já estará criado, na tela seguinte será exibida uma lista de sistemas nos quais o túnel pode ser instalado... Clicar na opção "Docker"

Logo abaixo haverá um comando longo que deve ser copiado. Desse comando precisamos só a parte que vem após o "--token", será uma string longa de caracteres aleatórios. Ela deve ser salva para a configuração do sistema posteriormente.

### Criação do hostname

Voltando para a tela Redes -> Túneis, clicar sobre o nome do túnel recém criado e após isso em Editar.

Selecionar a aba "Nome do host público"

Clicar em "+ Adicionar um nome do host público"

Selecionar um nome de subdomínoi e o domínio para a sua aplicação.

O campo "caminho" fica vazio

O campo "serviço" seleciona "HTTP"

No campo "URL" preencher apenas com "frontend" 

Salvar as alterações

Está concluída a configuração na cloudflare.


Configuração
------------

Todos os comandos a seguir devem ser digitados estando dentro da pasta deste projeto, utilizando a linha de comando no Terminal do Linux como root ou no Windows Powershell.

Os arquivos `example.env-backend` e `example.env-frontend` devem ser copiados para `.env-backend` e `.env-frontend` respectivamente.

Nos arquivos `.env-backend` e `.env-frontend` é absolutamente necessário editar o nome do host para refletir o nome que deseja utilizar.

Criar um arquivo chamado `.env-cloudflared`, nesse arquivo preencher apenas uma linha com o token obtido da cloudflare, no seguinte formato:

```
TUNNEL_TOKEN=conteúdo do token
```

Execução
--------

Depois de copiados e configurados os arquivos `.env-backend`, `.env-frontend` e `.env-cloudflared` basta executar o comando:

```bash
docker compose up -d
```

Em alguns minutos o sistema estará no ar no endereço configurado.

O login é o email configurado no arquivo `.env-backend`, o padrão é `admin@ticketz.host` e a senha é `123456`

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
docker compose up watchtower -d
```
