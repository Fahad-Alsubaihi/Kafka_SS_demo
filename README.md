# Kafka_SS_demo

## Description

Kafka & SingleStore commands Demo 
1- Create topic and schema for this topic 
## kafka commands:
Topic name:
```
demo_topic
```
Schema:
```
{
  "doc": "Sample schema to help you get started.",
  "fields": [
    {
      "doc": "The string is a unicode character sequence.",
      "name": "first_name",
      "type": "string"
    },
    {
      "doc": "The string is a unicode character sequence.",
      "name": "last_name",
      "type": "string"
    },
    {
      "doc": "The string is a unicode character sequence.",
      "name": "position",
      "type": "string"
    }
  ],
  "name": "DemoRecord",
  "namespace": "com.mycorp.mynamespace",
  "type": "record"
}
```
```
docker network ls
```
you will get an output like this:
```
NETWORK ID     NAME                    DRIVER    SCOPE
98842623c91b   bridge                  bridge    local
93b3993c71bc   cp-all-in-one_default   bridge    local
1a3f2ff21715   host                    host      local
5059222addc0   none                    null      local
```
copy the network name and past it in this command after (network=) like this:

```
docker run --rm -it --network=cp-all-in-one_default confluentinc/cp-kafka-connect bash
```
Producer:
```
kafka-avro-console-producer --bootstrap-server 172.18.0.3:9092  --property schema.registry.url=http://172.18.0.4:8081 --topic demo_topic --property value.schema.id=
```

Messages:
```
{"first_name":"Saleh", "last_name":"Alluhaidan", "position":"Developer"}
{"first_name":"Fahad", "last_name":"Alsubaihi", "position":"Developer"}
{"first_name":"Nawaf", "last_name":"Alrubayyi", "position":"Developer"}
{"first_name":"Ali", "last_name":"Alshehri", "position":"Developer"}
{"first_name":"Reem", "last_name":"Almedbil", "position":"Developer"}
{"first_name":"Rafeef", "last_name":"Almutairi", "position":"Developer"}
{"first_name":"Lamees", "last_name":"Abahussain", "position":"Developer"}
```
Consumer:
```
kafka-avro-console-consumer --bootstrap-server 172.18.0.3:9092 --property schema.registry.url=http://172.18.0.4:8081 --topic demo_topic --from-beginning --timeout-ms 5000 --max-messages 1000
```
## SS Commands:

```
Create database demo_DB;
```
```
Use demo_DB;
```
Create table:
```
Create table demo_table(
first_name varchar(50) ,
last_name varchar(50) ,
position varchar(50) );

```
Create pipeline:
```
CREATE PIPELINE demo_pipeline
As Load data KAFKA 'IP:9092/demp_topic'
Into table `demo_table`
FORMAT AVRO
SCHEMA REGISTRY 'IP:8081'
(
    `demo_table`.`first_name`<-`first_name`,
    `demo_table`.`last_name`<-` last_name`,
    `demo_table`.`position`<-`position`
);

```
Test pipeline:
```
TEST PIPELINE demo_pipeline;
```
Start pipeline:
```
START PIPELINE demo_pipeline;
```
Show data :)
```
Select*from demo_table;
```
