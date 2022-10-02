FROM ubuntu:22.04

RUN apt-get update && apt-get install -y openjdk-11-jre-headless wget && \
    useradd -m -s /bin/bash hive

WORKDIR /tmp

RUN wget "https://repo1.maven.org/maven2/org/apache/hive/hive-standalone-metastore/3.1.2/hive-standalone-metastore-3.1.2-bin.tar.gz" && \
    tar -zxvf hive-standalone-metastore-3.1.2-bin.tar.gz && \
    mv apache-hive-metastore-3.1.2-bin /opt/ && \
    rm hive-standalone-metastore-3.1.2-bin.tar.gz && \
    ln -s /opt/apache-hive-metastore-3.1.2-bin /opt/apache-hive-metastore

RUN wget "https://dlcdn.apache.org/hadoop/common/hadoop-3.3.4/hadoop-3.3.4.tar.gz" && \
    tar xvf hadoop-3.3.4.tar.gz && \
    mv hadoop-3.3.4 /opt/ && \
    rm hadoop-3.3.4.tar.gz && \
    ln -s /opt/hadoop-3.3.4 /opt/hadoop

USER hive
WORKDIR /home/hive

ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
ENV HADOOP_HOME=/opt/hadoop
ENV HADOOP_CLASSPATH=${HADOOP_HOME}/share/hadoop/tools/lib/aws-java-sdk-bundle-1.12.262.jar:${HADOOP_HOME}/share/hadoop/tools/lib/hadoop-aws-3.3.4.jar

RUN /opt/apache-hive-metastore/bin/schematool -initSchema -dbType derby

ENTRYPOINT [ "/opt/apache-hive-metastore/bin/start-metastore" ]
