### Stand alone mode
in standalone mode you run a single Kafka Connect process and it stores it state on the filesystem
#### run in stand alone mode using
````
need change plugin.path value in connect-standalone.properties to the value of location of jar file
ex: plugin.path=libs,libs/s3_connector/kafka-connect-s3-10.2.2.jar

bin/connect-standalone.sh config/connect-standalone.properties
````
### Distributed mode
you will have many Connect worker 
#### run in distributed mode using
````
need change plugin.path value in connect-standalone.properties to the value of location of jar file
ex: plugin.path=libs,libs/s3_connector/kafka-connect-s3-10.2.2.jar

bin/connect-distributed.sh config/connect-distributed.properties
````
#### Note  
<em>before starting up Kafka connect make sure you have a Kafka cluster running.</em>
![kafka config](./distribute.png)

### after connect started, using curl to add connector
curl -X PUT -H "Content-Type: application/json" -d @name_of_connector.json http://localhost:8083/connectors/name_of_connector/config
the name of connector mush be the same with the name properties in config file


### Sample Config
````
name=s3sink-field
connector.class=io.confluent.connect.s3.S3SinkConnector
tasks.max=1  
topics=quickstart-events
key.converter=org.apache.kafka.connect.storage.StringConverter
value.converter=org.apache.kafka.connect.storage.StringConverter
s3.bucket.name=hungnv-public
s3.region=ap-northeast-1
#aws.access.key.id=<Acceess key>
#aws.secret.access.key=<Secret Key>
storage.class=io.confluent.connect.s3.storage.S3Storage
format.class=io.confluent.connect.s3.format.json.JsonFormat
#format.class=io.confluent.connect.s3.format.avro.AvroFormat
schema.generator.class=io.confluent.connect.storage.hive.schema.DefaultSchemaGenerator
partitioner.class=io.confluent.connect.storage.partitioner.DefaultPartitioner
schema.compatibility=NONE
key.converter.schemas.enable=false
value.converter.schemas.enable=false
flush.size=1
````

in Json format
````
{
  "name": "my_connector",
  "connector.class": "io.confluent.connect.s3.S3SinkConnector",
  "tasks.max": 2,  
  "topics": "quickstart-events",
  
  "key.converter": "org.apache.kafka.connect.converters.ByteArrayConverter",
  "value.converter": "org.apache.kafka.connect.json.JsonConverter",  
  "value.converter.schemas.enable": "false",   
  
  "s3.bucket.name": "hungnv-public",
  "s3.region": "ap-northeast-1",
  "storage.class": "io.confluent.connect.s3.storage.S3Storage",
  "aws.access.key.id": "AKIASIBNHJK2SGP2WBWA",
  "aws.secret.access.key": "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",
  
  "partitioner.class": "io.confluent.connect.storage.partitioner.DefaultPartitioner",  
  "format.class": "io.confluent.connect.s3.format.json.JsonFormat",  
  "flush.size": "1",
  "behavior.on.null.values": "ignore"
}
````
