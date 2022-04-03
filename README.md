# Azure Cosmos DB Setup Container

Instantiate the Azure Cosmos DB by creating databases and containers 

[![adasd](https://img.shields.io/badge/Docker_Hub-robinmanuelthiel/cosmos--db--setup:latest-blue?logo=docker)](https://hub.docker.com/r/robinmanuelthiel/cosmos-db-setup/)

```bash
docker run --rm robinmanuelthiel/speedtest:latest \
  --env CONNECTION_STRING=AccountEndpoint=https://cosmosdb:8081/;AccountKey=xxxxxxxxxxx \
  --env DATABASE_NAME=my-database \
  --env CONTAINER_NAME=my-container \
  --env CONTAINER_PARTITION_KEY=/id
```

## Setup Cosmos DB Emulator with Docker Compose 

```yaml
version: '3.6'
services:
  setup:
    build:
      context: ../../
      dockerfile: Dockerfile
    depends_on:
      - cosmosdb

  cosmosdb:
    image: mcr.microsoft.com/cosmosdb/linux/azure-cosmos-emulator
    hostname: cosmosdb
    container_name: cosmosdb
    mem_limit: 3g
    cpus: 2.0
    ports:
      - '8081:8081'
      - '10251:10251'
      - '10252:10252'
      - '10254:10254'
    environment:
      - AZURE_COSMOS_EMULATOR_PARTITION_COUNT=10
      - AZURE_COSMOS_EMULATOR_ENABLE_DATA_PERSISTENCE=true
```
