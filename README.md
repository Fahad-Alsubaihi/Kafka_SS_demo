# Kafka_SS_demo

## Description

Kafka & SingleStore commands Demo 
1- Create topic and schema for this topic 
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
kafka-avro-console-producer --bootstrap-server IP:Port  --property schema.registry.url=http://IP:Port --topic demo_topic --property value.schema.id=
```

Messages:
```
```
