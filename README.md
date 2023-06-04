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
      "name": "role",
      "type": "string"
    }
  ],
  "name": "DemoRecord",
  "namespace": "com.mycorp.mynamespace",
  "type": "record"
}
```
Producer:
```
kafka-avro-console-producer --bootstrap-server IP:9092  --property schema.registry.url=http://IP:8081 --topic demo_topic --property value.schema.id=
```

Messages:
```
{"first_name":"Saleh", "last_name":"Alluhaidan", "role":"Developer"}
{"first_name":"Fahad", "last_name":"Alsubaihi", "role":"Developer"}
{"first_name":"Nawaf", "last_name":"Alrubayyi", "role":"Developer"}
{"first_name":"Ali", "last_name":"Alshehri", "role":"Developer"}
{"first_name":"Reem", "last_name":"Almedbil", "role":"Developer"}
{"first_name":"Rafeef", "last_name":"Almutairi", "role":"Developer"}
{"first_name":"Lamees", "last_name":"Abahussain", "role":"Developer"}
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
role varchar(50) );

```
Create pipeline:
```
CREATE PIPELINE demo_pipeline
As Load data KAFKA ‘IP:9092/demp_topic’
Into table ‘demo_table’
FORMAT AVRO
SCHEMA REGISTRY 'IP:8081'
(
    ` demo_table `.` first_name ` <- ` first_name `,
    ` demo_table `.` last_name ` <- ` last_name `,
    ` demo_table `.` role ` <- ` role `
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
