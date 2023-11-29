---
layout: "post"
title: "大数据"
date: "2023年6月5日15:53:04"
categories: algorithm
tags: [Computer Language, algorithm, basic, bigData]
---

# Hadoop

内存寻址时间比IO寻址快10w倍

单机处理大数据的Io速度太慢，内存也太小

大数据技术关心的重点： 
 - 分而治之
 - 并行计算
 - 计算向数据移动
 - 数据本地化读取 

## HDFS

Hadoop Distributed File System 分布式文件系统，与其他的分布式文件系统相比，Hadoop能更好的支持分布式计算。

### 存储模型

- 文件线性按字节切割成块（block），具有offset, id
- 文件与文件的block大小可以不一样
- 一个文件除最后一个block，其他block大小一致
- block的大小依据硬件的I/O特性调整
- block被分散存放在集群的节点中，具有location
- Block具有副本(replication),没有主从概念，副本不能出现在同一个节点
- 副本是满足可靠性和性能的关键
- 文件上传可以指定block的大小和副本数，上传后只能修改副本数
- 一次写入多次读取，不支持修改
- 支持追加数据



