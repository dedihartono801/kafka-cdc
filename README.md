[CDC Kafka And Debezium]

## Run Container

```bash
$ docker-compose up -d
```

## Connect Debezium with mysql

```bash
curl --location 'http://localhost:8083/connectors' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--data '{
  "name": "mysql-connector",
  "config": {
    "connector.class": "io.debezium.connector.mysql.MySqlConnector",
    "tasks.max": "1",
    "database.hostname": "mysql",
    "database.port": "3306",
    "database.user": "root",
    "database.password": "opklnm123",
    "database.server.id": "1",
    "database.server.name": "mysql",
    "topic.prefix": "cdc" ,
    "database.include.list": "latihan",
    "database.history.kafka.bootstrap.servers": "kafka:9092",
    "database.history.kafka.topic": "schema-changes",
    "database.allowPublicKeyRetrieval": "true",
    "schema.history.internal.kafka.bootstrap.servers": "kafka:9092",
    "schema.history.internal.kafka.topic": "schema-changes"
  }
}'
```

## Check Status Connection

```bash
curl --location 'http://localhost:8083/connectors/mysql-connector/status'
```

## Delete Connection

```bash
curl --location --request DELETE 'http://localhost:8083/connectors/mysql-connector'
```
