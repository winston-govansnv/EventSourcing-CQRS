"# EventSourcing-CQRS" 


# Project Title 
Hereunder is a brief description on the tools needed to run the application and how to run it.

## Table of Contents

- [Project Title](#project-title)
  - [Table of Contents](#table-of-contents)
  - [About](#about)
  - [Getting Started](#getting-started)
  - [Usage](#usage)

## About
The applicaiton provides an tempplte on how to organize an eventsourcing application using .Net. The readme also contains instructions on how to run the application.

## Getting Started
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.


## Usage
A step by step series of examples that tell you how to get a development env running.

#1. .NET 6 SDK

https://dotnet.microsoft.com/en-us/download/dotnet/6.0

#2. IDE or Code Editor

VS Code:
https://code.visualstudio.com/download

Visual Studio Community Edition:
https://visualstudio.microsoft.com/vs/community/

Rider:
https://www.jetbrains.com/rider/

#4. VS Code Extensions

C# for Visual Studio Code:
https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp

NuGet Package Manager:
https://marketplace.visualstudio.com/items?itemName=jmrog.vscode-nuget-package-manager

SQL Server (mssql):
https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql

#5. Postman

Download from:
https://www.postman.com/downloads/

#6. Docker

Download for Windows:
https://www.docker.com/products/docker-desktop

Once installed, check Docker version:
> docker --version


#8. Install or init docker compose 

https://docs.docker.com/compose/install

#9. Apache Kafka

Create docker-compose.yml file with contents:

version: "3.4"

services:
  zookeeper:
    image: bitnami/zookeeper
    restart: always
    ports:
      - "2181:2181"
    volumes:
      - "zookeeper_data:/bitnami"
    environment:
      - ALLOW_ANONYMOUS_LOGIN=yes
  kafka:
    image: bitnami/kafka
    ports:
      - "9092:9092"
    restart: always
    volumes:
      - "kafka_data:/bitnami"
    environment:
      - KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181
      - ALLOW_PLAINTEXT_LISTENER=yes
      - KAFKA_LISTENERS=PLAINTEXT://:9092
      - KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092
    depends_on:
      - zookeeper

volumes:
  zookeeper_data:
    driver: local
  kafka_data:
    driver: local
   
networks:
  default:
    external:
      name: mydockernetwork
    

The run by executing the following command:

> docker-compose up -d

#9. MongoDB

Run in Docker:
docker run -it -d --name mongo-container \
-p 27017:27017 --network mydockernetwork \
--restart always \
-v mongodb_data_container:/data/db \
mongo:latest

DU can use – Robo 3T to browse the MongoDB
https://robomongo.org/download

#9. Microsoft SQL Server

docker run -d --name sql-container \
--network mydockernetwork \
--restart always \
-e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=xxxxxxxx' -e 'MSSQL_PID=Express' \
-p 1433:1433 mcr.microsoft.com/mssql/server:2017-latest-ubuntu 

