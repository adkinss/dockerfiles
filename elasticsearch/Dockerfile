FROM itzg/ubuntu-openjdk-7

MAINTAINER itzg

RUN apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y wget && \
  apt-get clean

ENV ES_VERSION 1.4.2

RUN wget -qO /tmp/es.tgz https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-$ES_VERSION.tar.gz && \
  cd /usr/share && \
  tar xf /tmp/es.tgz && \
  rm /tmp/es.tgz

ENV ES_HOME /usr/share/elasticsearch-$ES_VERSION
RUN useradd -d $ES_HOME -M -r elasticsearch && \
  chown -R elasticsearch: $ES_HOME

RUN mkdir /data /conf && touch /data/.CREATED /conf/.CREATED && chown -R elasticsearch: /data /conf
VOLUME ["/data","/conf"]

ADD start /start

WORKDIR $ES_HOME
USER elasticsearch

EXPOSE 9200 9300

CMD ["/start"]
