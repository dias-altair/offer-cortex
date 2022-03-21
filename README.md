# Instalação do Agente

Atualmente a instalação e execução do agente somente pode ser realizada utilizando Docker. Logo abaixo haverá os passos para realizar a instalação e execução do agente.

## Pré-requisitos

Para a instalação e execução do agente, os seguintes pré-requisitos devem ser atendidos:

 - Docker instalado
 - Sistema Operacional Linux ou Windows 
 - Acesso a Internet

> **Obs:** No windows não execute os comandos no CMD, pois não irá funcionar. Utilize o Power Shell ou outro CLI compatível.

## 1 - Criar alias

O comando abaixo irá criar um alias no terminal para evitar que diversos comandos sejam executados para iniciar ou atualizar o agente.

    alias offerbot="
    docker stop offercortex.price || true &&
    docker stop offercortex.product || true &&
    docker container rm offercortex.price || true &&
    docker container rm offercortex.product || true &&
    docker pull diasaltair/offercortex.worker:latest &&
    docker run -d --name offercortex.price --env ASPNETCORE_ENVIRONMENT=CLUSTER --env SEARCH_MODE=PRICE diasaltair/offercortex.worker &&
    docker run -d --name offercortex.product --env ASPNETCORE_ENVIRONMENT=CLUSTER --env SEARCH_MODE=PRODUCT diasaltair/offercortex.worker &&
    docker update --restart unless-stopped offercortex.price &&
    docker update --restart unless-stopped offercortex.product"

## 2 - Execução do Agente

Após criar o alias, para executar o agente basta digitar o comando `offerbot` no terminal.
