
# 堆外内存垃圾回收

 1） full gc 的时候，会同时进行堆外内存垃圾回收。但 System.gc() 只是建议jvm进行垃圾回收，至于是否回收，不一定。一般触发时间：jvm 比较空闲或内存不足
 时候，不得不进行垃圾回收。堆内存由JVM自己管理，堆外内存必须要由我们自己释放；
 堆内存的消耗速度远远小于堆外内存的消耗，但要命的是必须先释放堆内存中的对象，才能释放堆外内存，但是我们又不能强制JVM释放堆内存。
 使用-XX:+DisableExplicitGC(禁止代码中显示调用GC)一定要小心，存在潜在的内存泄露风险。
 
 参考: https://www.cnblogs.com/moonandstar08/p/5107648.html
 
 2) 调用函数部分回收堆外内存
 
   java.nio.ByteBuffer buffer = ByteBuffer.allocateDirect(1024 * 1024 * 200);  
   
   ((sun.nio.ch.DirectBuffer)byteBuffer).cleaner().clean(); 

   参考: http://www.cnblogs.com/xing901022/p/5215458.html

# 非堆内存
  jvm 除了堆内存之外的内存，称之为非堆内存。
  
  https://www.cnblogs.com/duanxz/p/3520829.html
