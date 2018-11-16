FROM centos
MAINTAINER KINGKONG

ENV BUILD_ON 2018-11-11

COPY config /tmp
RUN yum install -y net-tools
RUN yum install -y openssh-server
RUN yum install -y openssh-clients
RUN yum install -y which

RUN mkdir /var/run/sshd

RUN ssh-keygen -A

ADD ./jdk-8u181-linux-x64.tar.gz /usr/local

ADD ./hadoop-2.8.5.tar.gz /usr/local

#ADD ./spark-2.3.0-bin-hadoop2.7.tgz /usr/local

ENV JAVA_HOME /usr/local/jdk1.8.0_181
ENV HADOOP_HOME /usr/local/hadoop-2.8.5
#ENV SPARK_HOME /usr/local/spark-2.3.0-bin-hadoop2.7

#ENV PATH

ENV PATH $JAVA_HOME/bin:$HADOOP_HOME/bin:$PATH
#:$SPARK_HOME/bin

RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa &&\
	cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
	chmod 600 ~/.ssh/authorized_keys	
	
COPY config /tmp


	#mv /tmp/masters $SPARK_HOME/conf/masters && \
	#cp /tmp/slaves $SPARK_HOME/conf/ && \
	#mv /tmp/spark-env.sh $SPARK_HOME/conf/spark-env.sh \
	
RUN cp /tmp/ssh_config ~/.ssh/config && \
	cp /tmp/profile /etc/profile && \
	cp /tmp/hadoop-env.sh $HADOOP_HOME/etc/hadoop/hadoop-env.sh && \
	cp /tmp/core-site.xml $HADOOP_HOME/etc/hadoop/core-site.xml && \
	cp /tmp/hdfs-site.xml $HADOOP_HOME/etc/hadoop/hdfs-site.xml && \
	cp /tmp/mapred-site.xml $HADOOP_HOME/etc/hadoop/mapred-site.xml && \
	cp /tmp/yarn-env.sh $HADOOP_HOME/etc/hadoop/yarn-env.sh && \
	cp /tmp/yarn-site.xml $HADOOP_HOME/etc/hadoop/yarn-site.xml && \
	cp /tmp/slaves $HADOOP_HOME/etc/hadoop/slaves && \
	mkdir -p /usr/local/hadoop2.7/dfs/data && \
	mkdir -p /usr/local/hadoop2.7/dfs/name && \
	cp /tmp/start-hadoop.sh ~/start-hadoop.sh && chmod 700 ~/start-hadoop.sh 
	#&& \
	#mv /tmp/restart-hadoop.sh ~/restart-hadoop.sh && chmod 700 ~/restart-hadoop.sh
	
RUN echo $JAVA_HOME
WORKDIR /root

#RUN /etc/init.d/sshd start
#RUN /usr/sbin/sshd-keygen -A
#RUN /usr/sbin/sshd
#RUN ssh-keygen -A


RUN chmod 700 start-hadoop.sh

RUN echo "root:123456" | chpasswd
EXPOSE 22
#RUN /usr/sbin/sshd
#CMD cat /tmp/hosts >> /etc/hosts
CMD ["/usr/sbin/sshd && cat /tmp/hosts >> /etc/hosts"]
#CMD /usr/sbin/sshd && /bin/bash
#CMD /usr/sbin/sshd && cat /tmp/hosts >> /etc/hosts
