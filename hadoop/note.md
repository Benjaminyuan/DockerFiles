## 环境搭建
### docker
* docker pull harisekhon/hadoop
* docker run -it -p 8042 -p 8088 -p 19888 -p 50070 -p 50075 harisekhon/hadoop:latest 
## 操作
> hadoop和unix文件操作基本一致，在开头需要加上 `hadoop fs`
## dockerfile 参考
* [参考链接](https://zhuanlan.zhihu.com/p/59758201)

## 启动
* hadoop namenode -format
* start-all.sh
* hdfs dfsadmin -report 查看节点状态

## 坑
* `workers`和`slavers`文件区别
  > hadoop 3.0后worker代替了slavers