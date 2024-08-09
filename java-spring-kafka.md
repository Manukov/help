## Content

* [ABSwitchCluster](#abswitchcluster-class)
* [ConsumerFactory](#consumerfactory-class)
* [DefaultKafkaConsumerFactory](#defaultkafkaconsumerfactory-class)
* [KafkaAdmin](#kafkaadmin-class)
* [KafkaResourceFactory](#kafkaresourcefactory-class)
* [ProducerFactory](#producerfactory-class)
* [Topic](#topic)

### Topic

[content](#content) [topic](kafka.md#topic)





### ABSwitchCluster-class
ABSwitchCluster(org.springframework.kafka.core)

### ConsumerFactory-class
ConsumerFactory(org.springframework.kafka.core)

### DefaultKafkaConsumerFactory-class
DefaultKafkaConsumerFactory(org.springframework.kafka.core)

### KafkaAdmin-class
KafkaAdmin (org.springframework.kafka.core) - .. класс который позволяет добавлять топики в брокер

В Spring-приложении бин KafkaAdmin создается вручную и бины топиков создаются вручную.
В SpringBoot-приложении бин KafkaAdmin создается Spring Framework и необходимо только создать бины топиков.

<details> <summary>Методы</summary>

* createOrModifyTopics(NewTopic) - принимает параметром NewTopic и создает топик;
* describeTopics(String) - принимает параметром имя топика и возвращает описание топика;

``` java

```
</details>

<details> <summary>Пример: прерывание загрузки контекста</summary>
KafkaAdmin позволяет загружать ApplicationContext с проверкой доступности брокера. Если брокер недоступен при загрузке бинов топиков, то будет зарегистрировано сообщение
с ошибкой, но ApplicationContext продолжит загружаться (приложение поднимется) и позще можно програмно вызвать метод инициализации у бина KafkaAdmin чтобы попробовать 
повторно создать топики. Такое возвожно когда по умолчанию у бина KafkaAdmin установлено setFatallBrokerNotAvailable(false).

``` java
@Bean
public KafkaAdmin admin() {
    Map<String, Object> prop = new HashMap<>();
    prop.put(AdminClientCongif.BOOTSPTRAP_SERVER_CONFIG, "localhost:9092")
    
    KafkaAdmin admin = new KafkaAdmin(prop);    //аргументов конструктора передаем конфигурацию
    admin.setFatallBrokerNotAvailable(true);    //если брокер недоступен (топики не созданы), то прерываем дальнейшую загрузку ApplicationContext
    return admin;
}
```
</details>


### KafkaResourceFactory-class
KafkaResourceFactory (org.springframework.kafka.core)

### ProducerFactory-class
ProducerFactory (org.springframework.kafka.core)

### TopicBuilder
TopicBuilder (org.springframework.kafka.config) - это билдер для настроки и создания топика