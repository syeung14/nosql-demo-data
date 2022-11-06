# nosql-demo-data

### MongoDB
```shell
docker run --name mongo-demo -d -ti --rm -p 27017:27017 mongo:4.0

docker exec -it mongo-demo /bin/bash -c "mongo mongodb://127.0.0.1:27017/"

https://www.mongodb.com/try/download/atlascli

```

### Cassandra
```shell
docker run -d --name cassandra-demo cassandra

docker exec -it cassandra-demo /bin/bash -c "cqlsh"
or
docker exec -it cassandra-demo /bin/bash
cqlsh

```

### Redis
```shell
docker run --name redis-demo -p 6379:6379 -d redis

docker exec -it redis-demo redis-cli

docker run -v redisinsight:/db -p 8001:8001 redislabs/redisinsight:latest

```

### Neo4j
```shell
docker run \
    --name neo4j-demo \
    --detach \
    --publish=7474:7474 --publish=7687:7687 \
    --volume=$HOME/neo4j/data:/data \
    --volume=$HOME/neo4j/logs:/logs \
    --env NEO4J_dbms_memory_pagecache_size=4G \
    --env NEO4J_AUTH=none \
    neo4j:4.4.9
```

### InfluxDB
```shell
docker run -d --name influxdb-demo -p 8086:8086 -v influxdb:/var/lib/influxdb influxdb:1.8 

docker exec -it influxdb-demo /bin/bash -c "influx" 
```