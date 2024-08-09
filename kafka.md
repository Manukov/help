


1. Скачиваем архив с Kafka
2. Запускаем ZooKeeper (отдельная сессия): ```bin\windows\zookeeper-server-start.bat zookeeper.properties```, где:
   * zookeeper.properties - настройки zooKeeper (\config\zookeeper.properties)
3. Запускаем Kafka (отдельная сессия): ```bin/kafka-server-start.bat config/server.properties```, где:
   * server.properties - настройки сервера kafks (\config\server.properties)
4. Создаем топик (отдельная сессия терминала): ```bin\windows\kafka-topics.bat --create --topic quickstart-events --bootstrap-server localhost:9092 -partitions 1 -replication-factor 1```, где:
   * ```--create --topic quickstart-events``` - создаем топик с именем quickstart-events
   * ```--bootstrap-server localhost:9092``` - хост + порт bootstrap-server
   * ```-partitions 1``` - одна партиция
   * ```-replication-factor 1``` - один
5. ююю


## Kafka

В состав Kafka (для windows) входят утилиты:
* 


## Content

* [Topic](#topic)

### Topic

Создание топика производиться при помощи утилиты "kafka-topic".


При попытке создания топика с таким же именем, получаем исключение TopicExistException: Topic 'name' already exists


[content](#content) 

### ZooKeeper