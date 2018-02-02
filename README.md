# Docker RELK stack

RELK stack (Rabbitmq, Elastic, Logstash, Kibana) powered by docker compose.
RabbitMQ is configured with an exchange and queue together with a binding. Logstash subscribes to this queue and sends messages onto elastic.  Then you can see messages appear in kibana.

This project has taken influence from these two great github repos which deserve credit:
[docker-elk](https://github.com/deviantony/docker-elk)
[docker-rabbitmq-example](https://github.com/jonathandandries/docker-rabbitmq-example)

See the subfolders for specific configuration of each component

### Requirements

* [docker](https://docs.docker.com/install/)
* [docker-compose](https://docs.docker.com/compose/)
* [docker-machine](https://docs.docker.com/machine/)

### Usage

Check that docker has **more than 2GB** of available memory to run the stack by checking the `Total Memory` variable:

```bash
docker info
```

If you need to change your docker configuration to increase it: 
- Docker for Windows 
  - Open Docker for Windows settings 
  - [Go to the Advanced setting](https://docs.docker.com/docker-for-windows/#advanced) and increase available memory
- Docker Toolbox 
  - Open VirtualBox Manager
  - Select the `default` docker VM
  - Select `Settings` -> `System` -> `Motherboard`
  - Increase the available `Base Memory`

Run the stack in the foreground **or** backgroung

```bash
docker-compose up    # foreground
docker-compose up -d # backgroung
```

Get the docker host IP address:

```bash
docker-machine ip
```

Send messages to the AMQP URI:

```
amqp://[docker-ip]:5672
```

#### Use admin consoles

Get the docker host IP address:

```bash
docker-machine ip
```

For Kibana Admin in your browser go to the address: 
`http://[docker-ip]:5601` e.g.: http://192.168.99.100:5601

For RabbitMQ admin in your browser go to the address: 
`http://[docker-ip]:5601` e.g.: http://192.168.99.100:15672. 
Use the following user and password: `guest:guest`

For RabbitMQ api documentation in your browser go to the address: 
`http://[docker-ip]:15672/api/` e.g.: http://192.168.99.100:15672/api/. 

To check that Elastic is running:
`http://[docker-ip]:9200` e.g.: http://192.168.99.100:9200 and check that elastis is working

For Elastic admin in your browser go to the address: 
`http://[docker-ip]:5601/app/kibana#/dev_tools` e.g.: http://192.168.99.100:5601/app/kibana#/dev_tools

#### Kibana initial setup

The first time you run this up you will be prompted to configure the kibana index pattern. 
You can only proceed here once you have sent some data into the index (logstash-\*).

Once at least one message is in there the index will have been created in elastic and you 
will be able to click the 'create' button. If this hasnt happened yet then you will 
see something like 'Unable to extract mapping...' and the button will be disabled! 

#### Changing configuration files
If you are changing the configuration files for logstash/kibana/rabbitmq you will need to re-build:

```bash
docker-compose build
docker-compose up 
```
