###	测试机器: qabb-qa-skynet2
###	安装gcc
	-	sudo yum -y install gcc make
	-	sudo yum -y install gcc gcc-c++
### 安装libunwind
	-	wget http://ftp.yzu.edu.tw/nongnu/libunwind/libunwind-1.1.tar.gz
	-	tar -xzvf libunwind-1.1.tar.gz
	-	./configure  --prefix=/opt/google-perftools/local/libunwind
	-	make
	-	sudo make install
### 安装 google-perfile
	-	wget https://github.com/gperftools/gperftools/releases/download/gperftools-2.5/gperftools-2.5.tar.gz
	-	tar -xzvf gperftools-2.5.tar.gz
	-	./configure --prefix=/opt/google-perftools/local/gperftools-2.5/
	-	make
	-	sudo make install
### java 进程启动的shell脚本中，增加如下环境变量:
	-	export LD_PRELOAD=/opt/google-perftools/local/gperftools-2.5/lib/libtcmalloc.so
	-	export HEAPPROFILE=/data/google-perftools/local/gzip # heap profile 位置
	-	export HEAP_PROFILE_ALLOCATION_INTERVAL=524288000 # 单位B，当前值 500MB，需要调小一些
	-	export HEAP_PROFILE_INUSE_INTERVAL=524288000 # 单位 B，当前是500MB，需要调小一些
### 通过shell脚本启动java进程
###	查看环境变量是否打进去
	-	cat /proc/${pid}/environ
	-	搜索是否包含: HEAP_PROFILE_ALLOCATION_INTERVAL
###	分析结果
	-	/opt/google-perftools/local/gperftools-2.5/bin/pprof --text /opt/java/bin/java gzip_18082.0002.heap
