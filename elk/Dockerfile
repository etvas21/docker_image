#	Dockerfile to create elasticsearch image
#   docker build -t es:6.8.6 .
#   docker run --name es -v db_es:/var/lib/mysql -d -p 9200:9200  es:6.8.6


FROM  ubuntu:18.04
LABEL maintainer="etvas21@naver.com"

ENV	DEBIAN_FRONTEND=noninteractive

# To test elasticsearch
RUN   apt-get update  \
      && apt-get install -y curl  \
		  && apt-get install -y wget  \
      && apt-get install -y vim  \
      # Install "software-properties-common" (for the "add-apt-repository")
      && apt-get install -y software-properties-common
# Do not install tee, apt-utils
# May be this command is already installed in Ubuntu 18.04
#      && apt-get install -y tee \
#      && apt-get install -y --no-install-recommends apt-utils

# In order to enter Hangul
RUN   sed -i '$ a\set encoding=utf-8' /etc/vim/vimrc

# Add the "JAVA" ppa
RUN add-apt-repository -y ppa:webupd8team/java

# Install OpenJDK-8
RUN apt-get update \
    && apt-get install -y openjdk-8-jdk \
    && apt-get install -y ant \
    && apt-get clean

# Fix certificate issues
RUN apt-get update \
    && apt-get install ca-certificates-java \
    && apt-get clean \
    && update-ca-certificates -f

# Setup JAVA_HOME -- useful for docker commandline
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
RUN export JAVA_HOME

RUN 	groupadd -g 1000 elasticsearch && useradd elasticsearch -u 1000 -g 1000


#elasticsearch 6.x
RUN		wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | apt-key add -
RUN		apt-get	install apt-transport-https
RUN		echo "deb https://artifacts.elastic.co/packages/6.x/apt stable main" | tee -a /etc/apt/sources.list.d/elastic-6.x.list
RUN		apt-get update && apt-get install elasticsearch


#LOGSTASH
#RUN		apt-get	install apt-transport-https
#RUN		echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-5.x.list
#RUN		apt-get update && apt-get install logstash

WORKDIR	/usr/share/elasticsearch

RUN set -ex && for path in data logs config config/scripts; do \
        mkdir -p "$path"; \
        chown -R elasticsearch:elasticsearch "$path"; \
    done

# chage to because 6.x
COPY 	logging.yml /usr/share/elasticsearch/config/
COPY 	elasticsearch.yml /etc/elasticsearch/
# below line is to apply 2.x version
#COPY 	elasticsearch.yml /usr/share/elasticsearch/config/
#COPY 	logging.yml /usr/share/elasticsearch/config/

#Install analysis-nori
RUN		/usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-nori

USER 	elasticsearch

ENV 	PATH=$PATH:/usr/share/elasticsearch/bin

CMD 	["elasticsearch"]

EXPOSE	9200 9300
