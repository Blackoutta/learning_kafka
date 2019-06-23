# Kafka Commands

## START ZOOKEEPER AND KAFKA SERVER

### Start Zookeeper

    zookeeper-server-start.sh config/zookeeper.properties

### Start Kafka server

    kafka-server-start.sh config/server.properties

---

## KAFKA TOPICS

### Create a topic

    kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic first_topic --create --partitions 3 --replication-factor 1

### Delete a topic

    kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic second_topic --delete

### View topic list

    kafka-topics.sh --zookeeper 127.0.0.1:2181 --list

### Describe a topic

    kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic new_topic2 --describe

---

## KAFKA CONSOLE PRODUCER

### Produce messages to a topic

    kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic first_topic

### Produce messages as key-value pairs

    kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic --property parse.key=true --property key.separator=,
    > key,value
    > another key,another value

### Set acks to all

    kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic first_topic --property acks=all

---

## KAFKA CONSOLE CONSUMER

### Read messages as a random consumer group

    kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic

### Read messages with a specified consumer group

    kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-application

### Read messages as key-value pairs

    kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning --property print.key=true --property key.separator=,

### Read all messages

    kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning

---

## KAFKA CONSUMER GROUPS

### View consumer group list

    kafka-consumer-groups.sh --bootstrap-server localhost:9092 --list

### Describe a consumer group

    kafka-consumer-groups.sh --bootstrap-server localhost:9092 --describe --group my-first-application

---

## Resetting Offsets

### Reset offsets to earliest

    kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group my-first-application --reset-offsets --to-earliest --execute --topic first_topic

### Shift offsets forward

    kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group my-first-application --reset-offsets --shift-by 2 --execute --topic first_topic

### Shift offsets backward

    kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group my-first-application --reset-offsets --shift-by -2 --execute --topic first_topic
