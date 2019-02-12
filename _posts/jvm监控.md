# java 进程启动参数配置

-Dcom.sun.management.jmxremote.ssl=false 
-Dcom.sun.management.jmxremote.authenticate=false 
-Dcom.sun.management.jmxremote.port=${port} 
-Djava.rmi.server.hostname=${host_ip}

${host_ip} : java 进程所在主机ip
${port} : java 进程jmx 暴露的端口

示例:

```
java -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.port=7776 -Djava.rmi.server.hostname=10.9.161.139 -jar /data/users/app/log-generator/target/log-generator.jar
```


# JConsole 连接（Mac 电脑）

## 1. 控制台输出: jconsole, 回车

## 2. 远程进程中输入 ip:端口







