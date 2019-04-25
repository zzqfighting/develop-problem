###
org.apache.kafka.common.errors.UnsupportedVersionException: Cannot create a v0 FindCoordinator request because we require features supported only in 1 or later.

1.  原因：kafka版本过低
1.  解决：装1.0以上版本

###
kafka启动的时候大量报出如下异常
ERROR [KafkaApi-1003] Number of alive brokers '1' does not meet the required replication factor '3' for the offsets topic (configured via 'offsets.topic.replication.factor'). This error can be ignored if the cluster is starting up and not all brokers are up yet. (kafka.server.KafkaApis)

1.  原因：节点配置问题
1.  解决：加如下配置
offsets.topic.replication.factor={broker count}
transaction.state.log.replication.factor={broker count}
transaction.state.log.min.isr={broker count}