# Docker RELK stack

RELK stack (Rabbitmq, Elastic, Logstash, Kibana) powered by docker compose.
RabbitMQ is configured with an exchange and queue together with a binding. Logstash subscribes to this queue and sends messages onto elastic.  Then you can see messages appear in kibana.

This project has taken influence from these two great github repos which deserve credit:
[docker-elk](https://github.com/deviantony/docker-elk)
[docker-rabbitmq-example](https://github.com/jonathandandries/docker-rabbitmq-example)

See the subfolders for specific configuration of each component

### Requirements
* docker
* docker-compose


### Usage

Run everything up in the foreground:
```
docker-compose up 
```

Run stack up in the backgroung
```
docker-compose up -d
```

Now send messages to the AMQP URI:
```
amqp://localhost:5672
```

#### Kibana initial setup
The first time you run this up you will be prompted to configure the kibana index pattern.  You can only proceed here once you have sent some data into the index (logstash-*).  Once at least one message is in there the index will have been created in elastic and you will be able to click the 'create' button. If this hasnt happened yet then you will see something like 'Unable to extract mapping...' and the button will be disabled! 

### Changing configuration files
If you are changing the configuration files for logstash/kibana/rabbitmq you will need to re-build:

```
docker-compose build
docker-compose up 
```

