FROM kibana:5.6.6

RUN apt-get update && apt-get install -y netcat

COPY ./config/kibana.yml /opt/kibana/config/

COPY entrypoint.sh /tmp/entrypoint.sh

RUN chmod +x /tmp/entrypoint.sh

CMD ["/tmp/entrypoint.sh"]
