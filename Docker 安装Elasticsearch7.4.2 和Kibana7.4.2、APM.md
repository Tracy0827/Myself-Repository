### **Docker 安装Elasticsearch7.4.2 和Kibana7.4.2、APM**

#### 一、下载镜像文件

```
docker pull elasticsearch:7.4.2
docker pull kibana:7.4.2
docker pull docker.elastic.co/apm/apm-server:7.4.2			(很慢很慢)
```

[^需要注意的是版本最好统一]: 

```
mkdir -p ~/mydata/elasticsearch/config
mkdir -p ~/mydata/elasticsearch/data
mkdir -p ~/mydata/apm
chmod -R 777 ~/mydata/elasticsearch/  #授权不然启动不了
chmod -R 777 ~/mydata/apm/  #授权不然启动不了
echo "http.host: 0.0.0.0" >> ~/mydata/elasticsearch/config/elasticsearch.yml
```

apm-server.yml文件如下（创建完文件后需要执行    chmod go-w ~/mydata/apm/apm-server.yml    权限为-rw-r--r--即可 644）

```
apm-server:
  host: "0.0.0.0:8200"      #0.0.0.0 标识任何机器都可以访问

output.elasticsearch:
  hosts: ["127.0.0.1:9200"]   #elasticsearch地址
```

#### 二、接下来就可以启动容器了,以下出现的127.0.0.1最好换成自己的IP地址

1. 启动es

   ```
   docker run --name elasticsearch -p 9200:9200 -p 9300:9300 \
   -e "discovery.type=single-node" \
   -e ES_JAVA_OPTS="-Xms64m -Xmx256m" \
   -v ~/mydata/elasticsearch/config/elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml \
   -v ~/mydata/elasticsearch/data:/usr/share/elasticsearch/data \
   -v ~/mydata/elasticsearch/plugins:/usr/share/elasticsearch/plugins \
   -d elasticsearch:7.4.2
   ```

   验证是否启动成功：

   在浏览器输入：http://127.0.0.1:9200  如果显示如下内容怎说明安装成功

2. 启动apm

   ```
   docker run -d \
   --name apm-server \
   --link elasticsearch:elasticsearch \
   -v ~/mydata/apm/apm-server.yml:/usr/share/apm-server/apm-server.yml \
   -p 8200:8200 \
   -e "TZ=Asia/Shanghai" \
   docker.elastic.co/apm/apm-server:7.4.2
   ```

   

3. 启动kibana

   

   ```
   docker run --name kibana -e ELASTICSEARCH_HOSTS=http://127.0.0.1:9200 -p 5601:5601 \
   -d kibana:7.4.2
   ```

   验证是否启动成功：

   在浏览器输入：http://127.0.0.1:5601如果显示如下内容怎说明安装成功

4. 相关设置及说明

   #docker 更改自启动
   docker update xxx --restart=always

   - **APM agent**

     APM agent 是使用与服务相同的语言编写的开源库，可以像安装其他库一样将它们安装到服务中，agent 将检测服务的代码并在运行时收集性能数据和错误，这些数据缓冲一小段时间并发送到 APM server。

     **APM server**

     APM Server 是用 Go 编写的开源应用程序，通常运行在专用服务器上，默认监听端口 8200 ，并通过 JSON HTTP API 从 agent 接收数据，然后根据该数据创建文档并将其存储在 Elasticsearch 中。

     **Elasticsearch**

     Elasticsearch 是高可扩展的开源全文搜索和分析引擎，用于快速、近实时地存储、搜索和分析大量数据。此处用于存储 APM 性能指标并利用其聚合。

     **Kibana**

     Kibana 是开源的分析和可视化平台，旨在与 Elasticsearch 协同工作，可以通过 Kibana 搜索、查看 Elasticsearch 中存储的数据，此处用于可视化 Elasticsearch 中存储的 APM 数据。

   

