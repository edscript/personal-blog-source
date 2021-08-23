---
title: "Pesquisa sobre o Docker"
date: 2021-08-21T02:40:51+09:00
description: O que realmente destaca o Docker? Porque motivos é tão falado? Para responder a estas questões realizei uma pesquisa. Neste artigo partilho o que faz o Docker ser tão único.
draft: false
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

# Docker...

Atualmente o Docker está no **hype** uns dizem que é pelos micro-serviços outros pelos recursos. Como não conhecia a tecnologia decidi por as mãos na massa e estudar um bocadinho de como a tecnologia funciona e o porquê de estar no hype. Acredito que no final deste artigo fiques com umas luzes para que serve o Docker.

## Um bocadinho de história 👴

Para perceber o motivo da existência do Docker vamos começar por contar um pouco da história dos servidores e como as aplicações eram executadas nos mesmos.

Hoje em dia é quase impossível distinguir o negócio e a aplicação que o "alimenta".

> No apllications, no businesses

### Anos 2000

Nesta altura os servidores corriam apenas uma aplicação.

![Um servidor para cada aplicação](/images/infra/docker/2000s.png)

Cada vez que o negócio desenvolvia uma aplicação era necessário comprar outro servidor. Os sysadmins tinham questões como:
- Que tipo de servidor a aplicação vai precisar ?
- O quão rápido precisa de ser ?

A resposta a estas questões... ninguém sabia. Com isto o departamento de TI compra um servidor rápido e despendioso, ningúem quer desempenho baixo, incapaz de correr a aplicação e potencialmente perder clientes e rendimentos, porque o departamento decidiu economizar num servidor que não era rápido o suficiente.
>O departamento comprou algo bom e rápido que  99 vezes em 100 era demasiado, tendo o servidor a correr entra 5/10% do que realmente era capaz.
![Recursos nos anos 2000](/images/infra/docker/2000s_resources.png)

### Máquinas virtuais
Os *mega* servidores um dia tornarão-se úteis 😂
Com a virtualização (*hypervisor*) podiamos rodar múltiplas aplicações num servidor.

>99 vezes em 100 apenas compravamos um servidor quando genuínamente precisavamos de um.

#### Contras
Para cada máquina virtual é necessário:
- Sistema Operativo (parte dos recursos do servidor CPU, RAM e storage, só para ser executada)
- Licença do Sistema Operativo
- Despesas adicionais opcionais (sysadmin)
	- Patching
	- Updates
	- Anti-vírus
- Tempo de inicialização comparado com um container
- Cada máquina pode ser um alvo de ataque

![Gasto de recursos com máquinas virtuais](/images/infra/docker/vms.png)

### Containers
Os containers interagem diretamenete com o Sistema Operativo do servidor, não existindo uma abstração do kernel como numa VM.

![Gasto de recursos com containers](/images/infra/docker/containers.png)

#### Diferenças entre VMs
**Hypervisors** virtualizam hardware (CPUs, RAM, networks...) enquanto os **containers** virtualizam o sistema operativo (cada um tem o seu processo, root file system, eth0...)

Cada **VM** num servidor partilha o mesmo hardware, cada **container** partilha o mesmo kernel do S.O e porque existe apenas um kernel os containers são mais pequenos, rápidos e mais "leves" que VMs.

![Diferenças entre VMs e containers](/images/infra/docker/vms_and_containers.png)

#### Funcionamento

O desenvolvimento durante muitos anos seguia o ditado "cada um faz da sua maneira", o Docker fornece uma maneira consistente de "entregar" o código em diferentes ambientes.
Através de uma `image` que é utilizado para construír um **container** e apenas de leitura (*read-only*), contém os ficheiros necesários (Sistema Operativo com o código da aplicação e o runtime para correr a aplicação), resumindo é um blueprint para correr um container.

O ``container`` é criada através de uma **image** com uma camada que permite escrever (*write*) dados. O motivo dos containers terem um tempo de inicialização tão curto é porque terem apenas esta camada de escrita, pois a `image` é que contém o software a correr.

O funcionamento está ser explicado de uma maneira muito abstrata e pode estar confusa. (*Futuramente irei escrever um artigo que explica as camadas, mas ainda estou a fundamentar o estudo* 👩‍🎓)

##### Benefícios
- Acelera o processo de desenvolvimento
	- Podemos ter vários tipos de programadores (Frontend, Backend) para configurar o ambiente localmente (database, cache, application), especialmente para quem trabalha remotamente pode ser dificíl, é preciso de ter as definições certas, versões certas. O Docker resolve isto através da criação de imagens que podem ser executadas com containers.
- Elimina conflitos de aplicações
	- Temos uma aplicação a correr numa versão específica de um framework e não pode ser atualizada, pois vai criar conflito com outras aplicações a correr nos servidores de produção. O Docker oferece containers isolados e cada um contém o framework que pode ser diferente de cada um.
- Consistência de ambientes
	- Mudar entre ambientes de desenvolvimento e produção pode ser um enorme problema. Com o Docker movemos apenas a imagem e executamos um container a ser executado.
- Entregar software mais rápido



## A empresa e a tecnologia

Existe a [tecnologia Docker]({{< relref "#containers" >}}) e a empresa Docker Inc que é autora da tecnologia.

### Docker Inc

Inicialmente chamada **dotcloud** no 2010 fornecia uma plataforma de desenvolvimento para a Amazon Web Services.

![Empresa dotcloud](/images/infra/docker/dotcloud.png)

Criaram ferramentas internas para criar a plataforma, estas ferramentas são os famosos containers. No ano 2013 a empresa com alguma dificuldades decidiu mudar de rumo, abriram o código dos projetos  internos "Docker" e passaram a ser designados de "Docker Inc". Ofereceram anos de trabalho, um projeto enorme que permite criar containers de uma maneira fácil e rápida, atualmente estão no negócio de "orquestração" e suporte a aplicações de containers (containerized apps) em escala com foco no mundo empresarial.