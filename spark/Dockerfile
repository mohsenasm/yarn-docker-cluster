# for tpc-ds
#FROM alpine/git as git
#WORKDIR /root
#RUN git clone https://github.com/IBM/spark-tpc-ds-performance-test

# for scala
FROM portworx/hadoop-yarn:2.7.1

RUN yum install -y wget

# install spark
RUN wget http://archive.apache.org/dist/spark/spark-2.4.0/spark-2.4.0-bin-hadoop2.7.tgz && \
    tar zxvf spark-2.4.0-bin-hadoop2.7.tgz && \
    rm spark-2.4.0-bin-hadoop2.7.tgz && \
    mv spark-2.4.0-bin-hadoop2.7 /usr/local/spark && \
    echo "export PATH=$PATH:/usr/local/spark/bin" >> /root/.bashrc && \
    echo "export SPARK_HOME=/usr/local/spark" >> /root/.bashrc

# install nano for development
# RUN yum install -y nano less
RUN echo "alias l='ls -CF'" >> /root/.bashrc && \
    echo "alias ll='ls -alF'" >> /root/.bashrc

# config spark
RUN mkdir /tmp/spark-events && echo '\
spark.eventLog.enabled          true \n\
spark.eventLog.dir              /tmp/spark-events \n\
spark.history.fs.logDirectory   /tmp/spark-events \n\
spark.master    yarn' > /usr/local/spark/conf/spark-defaults.conf && echo '\
export HADOOP_CONF_DIR=/usr/local/hadoop/etc/hadoop \n\
export SPARK_MASTER_IP=localhost' >> /usr/local/spark/conf/spark-env.sh


# copy TPC-DS performance test
#COPY --from=git /root/spark-tpc-ds-performance-test /root/spark-tpc-ds-performance-test
#COPY tpcdsenv.sh /root/spark-tpc-ds-performance-test/bin/tpcdsenv.sh

ENTRYPOINT []
