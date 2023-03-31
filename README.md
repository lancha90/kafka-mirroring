Run docker-compose
==================

```
docker-compose up -d
```

Connect to honeypod (3 tabs)
============================

```
docker exec -it <container-id> /bin/sh
```

Go to $KAFKA_HOME 
=================

```
cd /opt/bitnami/kafka
```

Copy config files
=================

- config/mirror-consumer.properties

- config/mirror-producer.properties


Crate topic
===========

```
bin/kafka-topics.sh --bootstrap-server target:9092 --topic  rpp-mirror --create --partitions 3 --replication-factor 1

bin/kafka-topics.sh --bootstrap-server source:9092 --topic  rpp-mirror --create --partitions 3 --replication-factor 1
```

Create a consumer (target)
==========================

```
bin/kafka-console-consumer.sh --bootstrap-server target:9092 --topic rpp-mirror
```

Create a producer (source)
==========================

```
bin/kafka-console-producer.sh --topic rpp-mirror --broker-list source:9092
```



Run mirroring tool
==================

```
bin/kafka-mirror-maker.sh --consumer.config config/mirror-consumer.properties --producer.config config/mirror-producer.properties --whitelist=".*"
```


Reference
=========

Kafka Image Doc - https://hub.docker.com/r/bitnami/kafka

Kafka Mirroring - https://aprenderbigdata.com/kafka-mirror-maker/#:~:text=Mirror%20Maker%20es%20una%20herramienta,fuente%20y%20un%20cl%C3%BAster%20destino.




