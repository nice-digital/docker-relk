# Docker RELK stack

RELK stack (Rabbitmq, Elastic, Logstash, Kibana).  RabbitMQ is configured with an example exchange and queue together with a bindings. Logstash subscribes to this queue and sends messages onto elastic.  Then you can see messages appear in kibana.

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

#### Kibana initial setup
The first time you run this up you will be prompted to configure the kibana index pattern.  You can only proceed here once you have sent some data into the index (logstash-*).  Once at least one message is in there the index will have been created in elastic and you will be able to click the 'create' button. If this hasnt happened yet then you will see something like 'Unable to extract mapping...' and the button will be disabled! 

### Changing configuration files
If you are changing the configuration files for logstash/kibana/rabbitmq you will need to re-build:

```
docker-compose build
docker-compose up 
```

