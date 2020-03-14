Spark Standalone集群搭建
---

[toc]

# 1.集群规划

|主机名|IP地址|服务器角色|
|:----|:-----|:------|
|node1|192.168.56.181|Master|
|node2|192.168.56.182|Worder|
|node3|192.168.56.183|Worker|


# 2.安装前提

```sh
$ tar -xvf spark-2.4.4-bin-hadoop2.7.tar -C /opt/spark-2.4.4
```


# 3.安装配置
## 3.1.配置slaves
```sh
$ cp slaves.template slaves
$ vim slaves

# 添加两个Worker
node2
node3
```

## 3.2.配置spark-env.sh
```sh
$ cp spark-env.sh.template spark-env.sh
$ vim spark-env.sh
# 在尾部添加如下内容
export SPARK_MASTER_IP=node1
export SPARK_MASTER_PORT=7077
export SPARK_WORKER_CORES=2
export SPARK_WORKER_MEMORY=3g
export SPARK_MASTER_WEBUI_PORT=8888 # 更改默认的8088端口
```

# 4.分发到Worker节点
```sh
$ scp -r ./spark-2.4.4 node2:`pwd`
$ scp -r ./spark-2.4.4 node3:$PWD
```

# 5.Master启动集群
```sh
$ cd $SPARK_HOME/sbin
$ ./start-all.sh
```