# tomcat部署
* tar –xvf file.tar //解压 tar包
tar -xzvf file.tar.gz //解压tar.gz
tar -xjvf file.tar.bz2   //解压 tar.bz2
tar –xZvf file.tar.Z   //解压tar.Z
unrar e file.rar //解压rar
unzip file.zip //解压zip
tar -xzf apache-tomcat-8.0.15.tar.gz
* mv apache-tomcat-7.0.76 tomcat_master
* hostname
* vi /etc/hosts
sudo vi /etc/hosts
* kill -9 14177
* /sbin/iptables -I INPUT -p tcp --dport 80 -j ACCEPT
* service iptables restart 
* /sbin/iptables -I INPUT -p tcp --dport 80 -j DROP(关闭端口)
* 默认连接配置：
<Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" URIEncoding="gbk" useBodyEncodingForURI="true" />
* 连接参数调优：
<Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" URIEncoding="gbk" useBodyEncodingForURI="true"
                               maxThreads="300" minSpareThreads="50"
maxSpareThreads="100" acceptCount="1000" />
* 非阻塞式IO配置：
<Connector port="8080" protocol="org.apache.coyote.http11.Http11NioProtocol"
               connectionTimeout="20000"
               redirectPort="8443" URIEncoding="gbk" useBodyEncodingForURI="true"/>
* 堆大小：
-Xms1024m –Xmx2048m 避免由于堆内存不足导致的内存溢出。
* 方法区大小：
-XX:PermSize=512m -XX:MaxPermSize=512m  避免由于加载 Jar包Class 过多导致的内存溢出
* 修改新生代和老年代的 GC策略：
-XX:+UseParNewGC -XX:+UseConcMarkSweepGC -XX:+CMSParallelRemarkEnabled -XX:+UseCMSCompactAtFullCollection -XX:+CMSClassUnloadingEnabled
* -XX:+UseParNewGC
新生代采用 ParNewGC 多线程收集器
-XX:+UseConcMarkSweepGC
老年代采用 CMS 收集器，降低 GC停顿时间
-XX:+CMSParallelRemarkEnabled
降低标记阶段的停顿时间
-XX:+UseCMSCompactAtFullCollection
CMS 基于标记- 清除，会产生碎片，通过此配置在 CMS 收集后做一次压缩整理
-XX:CMSFullGCsBeforeCompaction=0
配置多少次 CMS GC 后，做一次压缩整理，就不用每次都做压缩整理了
-XX:+UseCMSInitiatingOccupancyOnly -XX:CMSInitiatingOccupancyFraction=80
当老年代使用 80 ％后开始CMS 收集，默认值为 68% 。因为CMS 收集会有延迟，所以不能等到老年代占满时再收集
-XX:+CMSClassUnloadingEnabled
允许CMS 收集方法区 (PermGen) 。
JDK6 Update 3 及之前版本还需指定 -XX:+CMSPermGenSweepingEnabled参数
* VisualVM是JDK自带的性能监控工具，在JDK\bin目录下可以找到，可以监控JVM的内存、
CPU、线程等情况，使用很方便
