## ELK使用说明
### ELK概述
```
ELK，也就是Elasticsearch、Logstash、Kibana三者的结合，是一套开源的分布式日志管理方案.

更多详情，请见https://www.elastic.co/cn/

Elasticsearch：负责日志存储、检索和分析

LogStash：负责日志的收集、处理

Kibana：负责日志的可视化

以下都是我已经做好的docker镜像，可以下载自行学习
docker怎么装？这里我就不在具体描述了，可以google自行学习

```

### 主要内容有：
```
1. zookeeper安装
2. elasticsearch 安装
3. logstash 日志分析
4. 环境整合
```
#java sdk安装
```
yum install -y wget java-1.8.0-openjdk java-1.8.0-openjdk-devel && \
    echo "export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.151-1.b12.el7_4.x86_64" >> /etc/profile.d/java.sh && \
    echo "export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar" >> /etc/profile.d/java.sh && \
    echo "export PATH=$PATH:$JAVA_HOME/bin" >> /etc/profile.d/java.sh && \
    source /etc/profile.d/java.sh && \
    yum clean all
```
### 第一步:zookeeper安装
```
#安装
  cd /usr/local/src && \
    wget http://mirror.bit.edu.cn/apache/zookeeper/zookeeper-3.3.6/zookeeper-3.3.6.tar.gz && \
    tar -zxvf zookeeper-3.3.6.tar.gz && rm -rf zookeeper-3.3.6.tar.gz && \
    mv zookeeper-3.3.6 /usr/local/zookeeper
#启动 
/usr/local/zookeeper/bin/zkServer.sh start-foreground

```
### 第二步:elasticsearch 安装
```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.6.3.tar.gz
#安装
cd /usr/local/src &&\
     tar -xvf elasticsearch-5.6.3.tar.gz && \
     mv elasticsearch-5.6.3 /usr/local/elasticsearch && \
     chmod +x /usr/local/elasticsearch/bin/elasticsearch && \
     rm -rf elasticsearch-5.6.3.tar.gz

#创建elsearch组
groupadd elsearch && \
    useradd elsearch -g elsearch -p elasticsearch && \
    chown -R elsearch:elsearch  /usr/local/elasticsearch
#启动
su elsearch
/usr/local/elasticsearch/bin/elasticsearch
```
### 第三步: logstash 安装
```
cd /usr/local/src && \
wget https://download.elastic.co/logstash/logstash/logstash-2.4.1.tar.gz && \
     tar -xvf logstash-2.4.1.tar.gz &&\
     mv logstash-2.4.1 /usr/local/logstash &&\
     chmod +x /usr/local/logstash/bin/logstash && \
     rm -rf logstash-2.4.1.tar.gz
```

### 第四步: 环境整合
```
docker整合环境
镜像已经打包做好，直接docker pull 即可
docker-compose up -d

```

### 案例1
### elk+kafka日志系统
```

```