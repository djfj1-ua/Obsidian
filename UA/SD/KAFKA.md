**Comando para ejecutar zookeeper**
````
.\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties``
````

**Comando para iniciar Kafka**
````
.\bin\windows\kafka-server-start.bat .\config\server.properties
````

**Comando para crear un Topic llamado 'test'**
````
.\bin\windows\kafka-topics.bat --create --topic test --bootstrap-server localhost:9092
````

**Comando para crear un producer**
````
.\bin\windows\kafka-console-producer.bat --topic test --bootstrap-server localhost:9092
````

**Comando para crear un consumer**
````
.\bin\windows\kafka-console-consumer.bat --topic test --bootstrap-server localhost:9092
````
