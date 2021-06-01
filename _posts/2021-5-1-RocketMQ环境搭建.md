#部署RocketMQ

##一、RocketMQ简介
- RocektMQ是阿里巴巴在2012年开源的一个纯java、分布式、队列模型的第三代消息中间件，不仅在传统高频交易链路有着低延迟的出色表现，在实时计算等大数据领域也有着不错的吞吐。
2016年11月11号，双十一大促见证了RocketMQ低延迟存储架构的成功试水，99.996%的延迟落在了10ms以内，极个别由于GC引发的停顿在50ms以内，其高性能、低延时和高可靠的特性承载了近年来双十一17万笔/秒的交易峰值，在整个生产链路上都有着稳定和出色的表现。其在同年捐赠给Apache后正式进入孵化期。并于2017年9月RocketMQ正式从Apache社区正式毕业，成为Apache顶级项目。
- RocketMQ下载地址 [RocketMQ官网地址](http://rocketmq.apache.org/)

##二、部署RocektMQ
###1、下载
`wget https://www.apache.org/dyn/closer.cgi?path=rocketmq/4.8.0/rocketmq-all-4.8.0-bin-release.zip`
###2、解压
`unzip rocketmq-all-4.8.0-bin-release.zip`
###3、修改配置文件
```
根据机器配置
 vim runserver.sh  #修改runserver.sh文件
 JAVA_OPT="${JAVA_OPT} -server -Xms4g -Xmx4g -Xmn2g XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=320m"

 vim runbroker.sh #修改runbroker.sh文件
 #JAVA_OPT="${JAVA_OPT} -server -Xms8g -Xmx8g -Xmn4g"

 vim tools.sh  #修改tools.sh文件
 JAVA_OPT="${JAVA_OPT} -server -Xms256m -Xmx256m -Xmn256m -XX:PermSize=128m -XX:MaxPermSize=128m"
```
###4、启动namesrv
`nohup sh bin/mqnamesrv &`
###5、启动broker
`nohup sh bin/mqbroker -n localhost:9876  &`
###6、测试
```
 export NAMESRV_ADDR=localhost:9876
 
 sh bin/tools.sh org.apache.rocketmq.example.quickstart.Producer

 sh bin/tools.sh org.apache.rocketmq.example.quickstart.Consumer

```
##三、部署 rockermq console
```
docker pull styletang/rocketmq-console-ng
docker run --name rocketmq-console -dit -e "JAVA_OPTS=-Drocketmq.namesrv.addr=127.0.0.1:9876 -Dcom.rocketmq.sendMessageWithVIPChannel=false -server -Xms512m -Xmx512m -Xmn256m -XX:PermSize=128m -XX:MaxPermSize=128m" -p 8080:8080 styletang/rocketmq-console-ng bash
# 进入docker查看
docker exec -it rocketmq-console /bin/bash
```
![mq]({{ site.baseurl }}/images/mq.jpg)