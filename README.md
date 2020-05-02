# docker-spark-hdfs-hive
Cluster de spark, hdfs y hive con docker para entorno de desarrollo local

Creación de un cluster con spark, hdfs y hive componiendo imágenes de docker mediante docker compose.

Todas las imágenes de docker provienen del repositorio: https://hub.docker.com/u/bde2020

## Arrancar cluster
```
docker-compose up
```

## Acceso a las diferentes piezas del cluster

* Spark master: http://localhost:8080
* Namenode: http://localhost:50070
* Datanode: http://localhost:50075
* Resource manager: http://<dockerhadoop_IP_address>:8088/

## Tips / How to's
### ¿Cómo conocer las ip's de las máquinas del cluster?
```
docker network inspect docker-spark-hdfs-hive_default
```

### ¿Cómo revisar los logs de las máquinas del cluster?
```
docker logs -f docker-spark-hdfs-hive_spark-master_1
docker logs -f docker-spark-hdfs-hive_spark-worker-1_1
```

### ¿Cómo acceder a la máquina del hdfs y trabajar con los ficheros?
```
docker exec -it namenode bash
hadoop fs -ls /user
```

## Hive
### ¿Cómo acceder a hive por command line?
```
docker exec -it  docker-spark-hdfs-hive_hive-server_1 bash
# /opt/hive/bin/beeline -u jdbc:hive2://localhost:10000
> CREATE TABLE test (a INT, b STRING);
```

### ¿Cómo acceder a hive con presto?
```
./presto.jar --server localhost:8085 --catalog hive --schema default
```

## Enviar aplicaciones spark al cluster
