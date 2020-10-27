FROM ubuntu:16.04
RUN cp /etc/apt/sources.list /etc/apt/sources_init.list && rm /etc/apt/sources.list
RUN echo  "deb http://mirrors.aliyun.com/ubuntu/ xenial main \n\ 
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial main \n\ 
    deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main \n\ 
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main \n\ 
    deb http://mirrors.aliyun.com/ubuntu/ xenial universe \n\ 
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial universe \n\ 
    deb http://mirrors.aliyun.com/ubuntu/ xenial-updates universe \n\ 
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates universe \n\ 
    deb http://mirrors.aliyun.com/ubuntu/ xenial-security main \n\ 
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main \n\ 
    deb http://mirrors.aliyun.com/ubuntu/ xenial-security universe \n\ 
    deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security universe" > /etc/apt/sources.list
CMD [ "add-apt-repository" ,"ppa:openjdk-r/ppa" ]
RUN apt-get update && apt-get install -y openjdk-8-jdk 
RUN apt-get install -y scala && apt install -y vim \
    && apt-get install -y net-tools \
    && apt-get install -y openssh-server \
    && apt-get install -y openssh-client 
RUN cd ~
RUN sh -c '/bin/echo -e "\n"' | ssh-keygen -t rsa -P "" \
    && touch ~/.ssh/authorized_keys \
    && chmod 600 ~/.ssh/authorized_keys \
    && cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys \
    && service ssh start
RUN echo "service ssh start" >> ~/.bashrc
RUN wget https://mirrors.tuna.tsinghua.edu.cn/apache/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz \
    && tar -zxvf hadoop-3.3.0.tar.gz -C /usr/local/ \
    && cd /usr/local/ \
    && mv hadoop-3.3.0 hadoop 

ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 
ENV HADOOP_HOME=/usr/local/hadoop 
ENV JRE_HOME=$JAVA_HOME/jre    
ENV CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib    
ENV PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$JAVA_HOME/bin 
ENV HADOOP_COMMON_HOME=$HADOOP_HOME 
ENV HADOOP_HDFS_HOME=$HADOOP_HOME 
ENV HADOOP_MAPRED_HOME=$HADOOP_HOME 
ENV HADOOP_YARN_HOME=$HADOOP_HOME 
ENV HADOOP_INSTALL=$HADOOP_HOME 
ENV HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native 
ENV HADOOP_CONF_DIR=$HADOOP_HOME 
ENV HADOOP_LIBEXEC_DIR=$HADOOP_HOME/libexec 
ENV JAVA_LIBRARY_PATH=$HADOOP_HOME/lib/native:$JAVA_LIBRARY_PATH 
ENV HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
ENV HDFS_DATANODE_USER=root 
ENV HDFS_DATANODE_SECURE_USER=root 
ENV HDFS_SECONDARYNAMENODE_USER=root 
ENV HDFS_NAMENODE_USER=root 
ENV YARN_RESOURCEMANAGER_USER=root 
ENV YARN_NODEMANAGER_USER=root
WORKDIR /usr/local/hadoop/etc/hadoop

RUN echo "export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 \n\
        export HDFS_NAMENODE_USER=root \n\
        export HDFS_DATANODE_USER=root \n\
        export HDFS_SECONDARYNAMENODE_USER=root \n\
        export YARN_RESOURCEMANAGER_USER=root \n\
        export YARN_NODEMANAGER_USER=root " >> hadoop-env.sh
COPY config/* /tmp/

WORKDIR /usr/local/hadoop

ENV HADOOP_HOME=/usr/local/hadoop

RUN cp /tmp/ssh_config ~/.ssh/config && \
    cp /tmp/hdfs-site.xml $HADOOP_HOME/etc/hadoop/hdfs-site.xml && \ 
    cp /tmp/core-site.xml $HADOOP_HOME/etc/hadoop/core-site.xml && \
    cp /tmp/mapred-site.xml $HADOOP_HOME/etc/hadoop/mapred-site.xml && \
    cp /tmp/yarn-site.xml $HADOOP_HOME/etc/hadoop/yarn-site.xml && \
    cp /tmp/workers $HADOOP_HOME/etc/hadoop/workers && \
    chmod +x $HADOOP_HOME/sbin/start-dfs.sh && \
    chmod +x $HADOOP_HOME/sbin/start-yarn.sh 

EXPOSE 22
