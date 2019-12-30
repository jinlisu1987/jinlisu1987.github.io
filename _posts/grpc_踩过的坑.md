# Grpc 踩过的一些坑


##  问题: 服务端 返回 "too_many_pings"  error, 并且服务端断开链接

https://docs.factcast.org/setup/examples/grpc-config-keepalive/

https://github.com/pravega/pravega/issues/1867

https://erpeng.github.io/2019/08/15/grpc-go-keepalive-server/


## 问题: direct memory 申请失败，导致的OutOfDirectMemoryError
```
io.grpc.netty.shaded.io.netty.util.internal.OutOfDirectMemoryError: failed to allocate 16777216 byte(s) of direct memory (used: 1895825687, max: 1908932608)
	at io.grpc.netty.shaded.io.netty.util.internal.PlatformDependent.incrementMemoryCounter(PlatformDependent.java:725)
	at 
```
		
解决方法:
https://github.com/grpc/grpc-java/issues/4001
https://github.com/grpc/grpc-java/tree/master/examples/src/main/java/io/grpc/examples/manualflowcontrol


## 问题: 压测时，老年代内存使用量缓慢上涨，导致频繁full gc 

排查发现: 
System.setProperty("io.grpc.netty.shaded.io.netty.recycler.maxCapacityPerThread", "0");

