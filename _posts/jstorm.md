调整 worker 中jvm参数的方式:

worker 参数装置过程:

com.alibaba.jstorm.daemon.supervisor.SyncProcessEvent#getWorkerMemParameter

增加一些额外参数，注意调整内存等无效哦，原因看读上面类的源码, 
topology.worker.childopts: " -XX:+UnlockCommercialFeatures -XX:+FlightRecorder "

修改配置后，需重启supervisor 
