---
title: "Comandos de Docker"
date: 2021-08-22T02:40:51+09:00
description: Comandos mais utilizados de Docker de forma a evitar consultar a documentação e explicar o que o comando faz em Português.
draft: true
hideToc: false
enableToc: true
enableTocContent: true
tocPosition: inner
tags:
- docker
- research
series:
-
categories:
- infrastructure
- docker
image: images/infra/docker/logo.png
meta_image: images/infra/docker/logo.png
---

# Docker
Maneiras de utilizar o Docker:
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Play with Docker](https://labs.play-with-docker.com/)
	- Necessário conta no [Docker Hub](https://hub.docker.com/)
- [Kitematic](https://kitematic.com/)

## Docker file
```yaml
# File system constructs (folders, device files) no OS Kernel
# the container itself doesn't come packaged with its own kernel
# including node tools
FROM node:current-alpine

# Metadata
LABEL: org.opencontainers.image.title="Hello World!"

# Create directory in container image for app code
RUN mkdir -p /usr/src/app

# Copy app code (.) to /usr/src/app in container image
COPY . /usr/src/app

# Set wroking directory context
WORKDIR /usr/src/app

# Install dependencies from package.json
RUN npm install

# Command for container to execute
ENTRYPOINT ["node", "app.js "]
```

## Commands
### pull
Fazer download de imagem do repositório dockerhub
```zsh
docker pull [imageName]
```

### image
#### build (construir uma imagem)
```zsh
docker image build --tag [dockerhubId]/[repositoryName]:[imageName]
```
##### Exemplo
```zsh
docker image build --tag edscript/example-ctr:example .
```
O ponto(.) significa que os ficheiros para ser feito a build estão no diretório atual.

#### delete (apagar uma imagem)
```zsh
docker image rm [ [dockerhubId]/[repositoryName]:[imageName] | [imageId] ]
# alias: docker rmi [ [dockerhubId]/[repositoryName]:[imageName] | [imageId] ]
```
##### Exemplos
```zsh
docker image rm edscript/example-ctr:example
```
###### Flags
`-f` - Forçar a remoção do container sem ser necessário terminar
```zsh
# Remove a container that is running
docker image rm edscript/example-ctr:example -f
```

#### list (listar uma imagem)
```zsh
docker image ls
# alias: docker images
```

#### publish (publicar uma imagem)
Para realizar `push` é necessário estar logado
```zsh
docker image push [dockerhubId]/[repositoryName]:[imageName]
```
##### Exemplos
```zsh
docker image push edscript/example-ctr:example
```

### container

#### Flags
`-detach`, `-d` - Executar o container em background e fazer o output do ID do container
`--name` - Atribuír nome ao container
`--publish` , `-p` - Atribuír porta(s) ao host/container
```zsh
# Map port 8000 on the Docker host(laptop) to 8080 in the container(app)
# Any trafic on docker host port 8000 is going to sent to 8080 in the container
docker container run -p 8000:8080
```
`-it` - (Interactive and terminal) attach a uma shell dentro do container a correr em foreground(primeiro-plano)
```zsh
docker container run -it --name showing-container alpine <shell>
# Windows server <sheel> -it mcr.microsoft.com/powershell:nanoserver pwsh.exe
# Linux <sheel> -it alpine sh

Comando: / # exit  # Sair da shell e terminar o container
Comando: CTRL+P+Q # Sair da shell sem terminar o container
```

#### run (inicializar container)
```zsh
docker container run -d --name [containerName] -p [dockerPort]:[appPort] [dockerhubId]/[repositoryName]:[imageName]
```

#### start (arrancar container)
```zsh
docker container start [containerName | containerId]
```

#### stop (parar container)
```zsh
docker container stop [containerName | containerId]

docker container ls -a
 -----  CREATED         STATUS
        4 minutes ago   Exited (137) 35 seconds ago
```
##### Exemplos
```zsh
docker container stop web
```

#### remove (remover container)
Delete a container
```zsh
docker container rm [containerName | containerId]
```

#### list (listar containers)
```zsh
docker container ls
# alias: docker container ps
```
##### Exemplos
```zsh
docker container ls -a
```
`-a` - Lista todos os containers (em execução/paradaos)

### login
```zsh
docker login --username="<username>" --password="<password>"
```

## Buzzwords
`Container registries` - Repositório onde é guardado a imagem do container para poder ser partilhada e acessível de diferentes ambientes.
`Containerized app` - Aplicação executada num container
`Language Agnostic` - Docker funciona com multiplas linguagens de programação, não existe uma em específico.
`Declarative` - Descrever o estado desejado da aplicação num ficheiro config que é usado para fazer deploy e gerir a aplicação.

## Docker compose
Compose é uma ferramenta para correr aplicações Docker em vários containers. É utilizado um ficheiro **YAML** para configurar os serviços da aplicação. Com um simples comando é criado e executado todos os serviços que estão no configurados no ficheiro (compose file).
### up (executar)
Dentro do diretório com os ficheiros deve comparecer o ficheiro `docker-compose.yaml`
```zsh
docker-compose up
```

### down (parar)
Dentro do diretório com os ficheiros deve comparecer o ficheiro `docker-compose.yaml`
```zsh
docker-compose down
```
