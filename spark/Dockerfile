FROM ubuntu:14.04

#install basic software needed for downloading and running Spark
RUN apt-get update && apt-get install -y wget software-properties-common ssh

#install Spark
RUN wget http://d3kbcqa49mib13.cloudfront.net/spark-2.1.0-bin-hadoop2.7.tgz && \
    tar xzvf spark-2.1.0-bin-hadoop2.7.tgz -C /usr/local/ && \
    ln -s /usr/local/spark-2.1.0-bin-hadoop2.7 /usr/local/spark && \
    rm spark-2.1.0-bin-hadoop2.7.tgz

#install java8
RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
ENV SPARK_HOME /usr/local/spark
ENV PATH $PATH:$SPARK_HOME/bin

##exposing ports for running and tracking Spark jobs
#8080: UI for all tracking jobs
#4040: current app tracking
#6066: port used for submitting jobs
#7077: port used by slave nodes
EXPOSE 8080 4040 6066 7077

VOLUME /data
VOLUME /apps

#run Spark (process from ./sbin/spark-daemon.sh) in the foreground
ENV SPARK_NO_DAEMONIZE=true