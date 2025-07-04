# Projeto Imersão DevOps - Alura Google Cloud

Este repositório documenta a jornada prática da Imersão DevOps da Alura. O objetivo principal foi aplicar um fluxo de trabalho DevOps completo a uma API em Python (FastAPI), desde a criação do ambiente com Docker até a automação do deploy na nuvem com GitHub Actions e Google Cloud.

A API base utilizada, que serve como objeto de estudo, foi fornecida pela equipe Alura e pode ser encontrada [aqui](https://github.com/guilhermeonrails/ellis)


## Tecnologias e Conceitos Aplicados
- Containerização: Uso de Docker e Dockerfile para criar um ambiente padronizado e isolado para a aplicação.

- Orquestração de Contêineres: Utilização do Docker Compose para simplificar a gestão do ambiente de desenvolvimento local.

- Integração Contínua (CI): Automação com GitHub Actions para construir e validar a imagem Docker a cada alteração no código.

- Deploy Contínuo (CD): Implantação da aplicação no Google Cloud Run, uma plataforma serverless para contêineres.

## 🌐 Aplicação em Produção
A API implantada como resultado deste projeto pode ser acessada através do seguinte link:

[https://api-escolar-354902248408.southamerica-east1.run.app/docs](https://api-escolar-354902248408.southamerica-east1.run.app/docs)

## Como Executar o Projeto Localmente
Para executar a aplicação no seu ambiente de desenvolvimento, você precisará ter o Git e o Docker (com Docker Compose) instalados.

1. Clone o repositório:
   ~~~
      git clone https://github.com/LucasRibasCardoso/demo-imersao-alura-devops.git
      cd demo-imersao-alura-devops
   ~~~
2. Suba o ambiente com Docker Compose:
   ~~~
   docker-compose up
   ~~~
3. Acesse a API: http://localhost:8000/docs


## O Pipeline DevOps
Este projeto implementa um pipeline DevOps completo, desde o código até a produção.

#### 1. Dockerização (```Dockerfile```)

   O arquivo ```Dockerfile``` contém o passo a passo para criar uma imagem executável da aplicação. Ele utiliza uma imagem base de Python, instala as dependências e define o comando para iniciar o servidor Uvicorn.

#### 2. Integração Contínua (GitHub Actions)

O workflow definido em ```.github/workflows/docker-image.yml``` automatiza a validação do projeto.

- Gatilho: É acionado a cada ```push``` ou ```pull``` request na branch ```main```.

- Ação: Ele constrói a imagem Docker usando o ```Dockerfile```. Cada build recebe uma tag única baseada no timestamp ```($(date +%s))```, garantindo um versionamento claro.
      
- Objetivo: Garantir que as novas alterações no código não quebrem a capacidade de construir uma imagem funcional da aplicação.

#### 3. Deploy Contínuo (Google Cloud Run)
O deploy final é feito manualmente através da CLI do Google Cloud, mas segue um processo automatizado na nuvem.

- Autenticação e Configuração: Os comandos ```gcloud auth login``` e ```gcloud config set project``` preparam o ambiente local para se comunicar com o projeto correto no GCP.

- Deploy: O comando ```gcloud run deploy``` envia o código para o Google Cloud Build, que constrói e armazena a imagem no Artifact Registry. Em seguida, o Google Cloud Run utiliza essa imagem para implantar uma nova versão da aplicação, disponibilizando-a através de uma URL HTTPS segura e escalável.




