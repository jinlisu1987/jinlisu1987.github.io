# https://blog.csdn.net/define_us/article/details/82905330

# jstorm 心跳更新过程

## 心跳超时时间设置: nimbus.task.timeout.secs, 默认值: 240s

## task 中TaskHeartbeatTrigger上报心跳Tuple，到 topology master

###上报心跳之前，会先检查心跳是否超时，超时的话，打印错误包含 "Report error to /ZK/taskerrors/" 的ERROR级别日志，并将错误信息写入zk，用于jstorm ui业务展示task错误信息

## topology master 中 TaskHeartbeatUpdater 消费心跳Tuple，将每个拓扑的心跳信息发送给 nimbus

### 日志中包含关键字: "Update task heartbeat"

## nimbus 接收最新的心跳信息，更新内存中心跳状态，并写zk

### backtype.storm.generated.Nimbus.Processor.updateTaskHeartbeat 类 调用 com.alibaba.jstorm.daemon.nimbus.ServiceHandler#updateTaskHeartbeat 更新nimbusData 中心跳的状态

### nimbus 中MonitorRunnable 线程，会将nimbus内存中维护的nimbusData中心跳状态更新到zk的/taskbeats/topologyid
