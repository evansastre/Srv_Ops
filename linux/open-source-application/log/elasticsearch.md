# elasticsearch

[ELK Doc](https://elasticsearch.cn/book/elasticsearch_definitive_guide_2.x/running-elasticsearch.html)

Install

```text
yum install java
```

[Download ELK](https://www.elastic.co/downloads/elasticsearch)

Unzip Elasticsearch

```text
tar xf ******
```

Run - can't use root 

```text
#blueking path:   /data/bkee_xxx/service/es
bin/elasticsearch      
bin/elasticsearch -d #keep running as backend process
```

Test

```text
curl http://localhost:9200
```

multiple instance

```text
vim /data/bkee_pb/service/es/config/elasticsearch.yml

#change marked config line
==========================================
#change
cluster.name: bkee-es
node.master: true
node.data: true
#change
node.name: es-2
node.attr.tag: cold
#change
path.data: /data/bkee_xxx/public/es/data
#change
path.logs: /data/bkee_xxx/logs/es
bootstrap.memory_lock: false
bootstrap.system_call_filter: false
network.host: "10.38.0.11"
#change 
http.port: 10004
#change 
transport.tcp.port: 9300
discovery.zen.ping.unicast.hosts: ["10.38.0.16", "10.38.0.11", "10.38.0.12"]
discovery.zen.minimum_master_nodes: 2
thread_pool.search.size: 1000
thread_pool.search.queue_size: 1000
thread_pool.bulk.queue_size: 1000
cluster.routing.allocation.same_shard.host: true
==========================================

#start
bin/elasticsearch 
#in blueking use bin/es.sh
```

















