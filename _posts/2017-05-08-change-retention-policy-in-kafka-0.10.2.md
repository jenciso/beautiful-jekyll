---
layout: post
published: true
title: Change retention policy in kafka 0.10.2
bigimg: /img/kafka_logo.png
---

This example is based in CentOS 7

Example: Change retention policy to 24hr

```sh
[root@dcbvm090dv601 kafka_2.12-0.10.2.0]# cd /etc/kafka_2.12-0.10.2.0
[root@dcbvm090dv601 kafka_2.12-0.10.2.0]# bin/kafka-topics.sh --alter --zookeeper localhost:2181 --topic metrics --config retention.ms=86400000      
WARNING: Altering topic configuration from this script has been deprecated and may be removed in future releases.
         Going forward, please use kafka-configs.sh for this functionality
Updated config for topic "metrics".
[root@dcbvm090dv601 kafka_2.12-0.10.2.0]# bin/kafka-topics.sh --zookeeper localhost:2181 --describe --topic metrics
Topic:metrics   PartitionCount:3        ReplicationFactor:1     Configs:retention.ms=86400000
        Topic: metrics  Partition: 0    Leader: 3       Replicas: 3     Isr: 3
        Topic: metrics  Partition: 1    Leader: 1       Replicas: 1     Isr: 1
        Topic: metrics  Partition: 2    Leader: 3       Replicas: 3     Isr: 3
[root@dcbvm090dv601 kafka_2.12-0.10.2.0]# 
```


