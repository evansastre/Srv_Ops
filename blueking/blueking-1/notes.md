# Notes\_huangsl

## BlueKing proxy initial 

1.Proxy require centos7. 

2.Proxy temp open outbound. 

3.Network access: 

```text
GSE to proxy : port TCP:10020,58930,22 UDP:10020,10030 
proxy to GSE : port TCP:48533,58625,58725,58930,10020 UDP:10020,10030 
!proxy to Nginx: port TCP:80 
proxy to proxy : port TCP:58930,10020 UDP:10020,10030

agent to proxy: port TCP:48533,58625,59173,10020 UDP:10020,10030 
proxy to agent: port TCP:60020-60030,(windows)22,445 UDP：60020-60030 
agent to agent: port TCP:60020-60030 UDP：60020-60030 
```

4.Proxy check "/etc/yum.conf"  , enable kernel update, repo useful.

### How to restart blueking task service on gse

```text
cd /data/bkee/gse/server/bin 
./gsectl restart task
#./gse_task -f /data/bkee/etc/gse/task.conf
```

### Deploy test on  tencent cloud

ssh root@139.199.180.33 -p 22 XXXX 

address：[http://paas.blueking.com](http://paas.blueking.com) 

username：admin 

password：\*\*\*\*\*



ssh -p 36000 shilei@203.117.148.40

## controller 

./bkeec start \| stop \| status \| XXX



\#issue can not install agent

1.need add "admin" to business-operation member

2.check cert esb 

/data/bkee/cert

There are two Job server, we found one job gse cert is new while another not. So sync them to newer one, and restart job service.

Also need compare two open\_paas server.

```text
#on central controller machine
scp shilei@192.168.1.5:/data/bkee/cert/gse_job_api_client.truststore .
scp shilei@192.168.1.5:/data/bkee/cert/job_server.keystore .
scp shilei@192.168.1.5:/data/bkee/cert/job_server.truststore .

scp ./gse_job_api_client.truststore shilei@192.168.1.7:/home/shilei
scp ./job_server.keystore shilei@192.168.1.7:/home/shilei
scp ./job_server.truststore shilei@192.168.1.7:/home/shilei

scp ./gse_job_api_client.truststore shilei@192.168.1.4:/home/shilei
scp ./job_server.keystore shilei@192.168.1.4:/home/shilei
scp ./job_server.truststore shilei@192.168.1.4:/home/shilei

#on 192.168.1.7 &192.168.1.4  /home/shilei
mv ./gse_job_api_client.truststore /data/bkee/cert/
mv ./job_server.keystore /data/bkee/cert 
mv ./job_server.truststore /data/bkee/cert
```

3.need restart job  after update cert

```text
#on central controller machine
/data/install/bkeec stop job
/data/install/bkeec start job
```





