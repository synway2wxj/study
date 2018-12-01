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

---
* 如果本机安装了多个Tomcat，不论点击谁的startup.bat，启动的都是CATALINA_HOME变量所指向的Tomcat。因为该原因，一般也不推荐配置这个环境变量
* 在Tomcat中可以运行多个站点，用户用浏览器访问Tomcat服务器中的每个站点的时候，就像在访问各自独立的服务器一样。所以我们可以说，各个站点是分别运行在Tomcat这个真实服务器上的一台虚拟主机上
一个Tomcat中可以配置多台虚拟主机，一个虚拟主机上可以运行一个网站。一个网站就可以认为是一台虚拟主机。
* <Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
Tomcat初始自带的一个虚拟主机localhost，并且外部访问所有应用资源所在的根目录是webapps
* 在Server.xml的<Host>标签中，添加<Context/>标签，就可以为该虚拟主机配置一个web应用了：<Context path="/news" docBase="E:\news" />
  缺省web应用的配置，即默认的web应用，当不写web应用路径时，默认访问的就是这个应用：<Context path="" docBase="E:\news" />
* 在 Tomcat/conf/Catalina/[Host] 目录下写一个xml文件，其中，xml文件的名字就是虚拟路径，在这个xml中可以添加标签，再在其中配置真实路径：
  conf/Catalina/localhost/news.xml：（这种修改方式不需要重启服务器，如果虚拟路径中有”/”，由于文件名不允许包含”/”，需要用”#”代替）
  <?xml version="1.0" encoding="utf-8"?>
  <Context docBase="E:\news" />
* 直接将web应用放置到虚拟主机管理的目录下，虚拟主机就可以找到这个web应用：
  直接将news文件夹放到 Tomcat/webapps 下；；只要将web应用文件夹的名称改为ROOT，这个web应用就是缺省应用。
  news
|-- ①
|-- WEB-INF ②
    |-- classes ③
    |-- lib ④
    |-- web.xml ⑤
  可以在WEB-INF的web.xml中设置主页的指向：
  <welcome-file-list>
    <welcome-file>
        hello.html
    </welcome-file>
  </welcome-file-list>
* 在conf/server.xml中<Engine>标签下添加一个<Host>标签，就可以新增一台虚拟主机了：
  name —— 指定虚拟主机的名称，浏览器通过这个名称访问虚拟主机
  appBase —— 虚拟主机管理的目录，放置在这个目录下的web应用，虚拟主机可以自动加载
  缺省虚拟主机可以通过在server.xml中engine标签上的defaultHost属性进行配置：<Engine name="Catalina" defaultHost="localhost">
* 给context元素设置reloadable属性为true，可以让Tomcat自动加载更新后的web应用，当java程序修改后可以不用重启，服务器自动重新加载。但会降低性能
* localhost/manager/html，可以进入主机内web应用的管理界面，在这之前需要在conf下的tomcat-users.xml添加管理用户：
  <role rolename="manager-gui"/>
  <user username="tomcat" password="tomcat" roles="manager-gui"/>
* <Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" />
  <Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />
1. 通过配置第1个Connector，客户端可以通过8080端口号使用http协议访问Tomcat。其中，protocol属性规定了请求的协议，port规定了请求的端口号，redirectPort表示当强制要求https而请求是http时，重定向至端口号为8443的Connector，connectionTimeout表示连接的超时时间  
2. 通过配置第2个Connector，客户端可以通过8009端口号使用AJP协议访问Tomcat。AJP协议负责和其他的HTTP服务器(如Apache)建立连接；在把Tomcat与其他HTTP服务器集成时，就需要用到这个连接器。之所以使用Tomcat和其他服务器集成，是因为Tomcat可以用作Servlet/JSP容器，但是对静态资源的处理速度较慢，不如Apache和IIS等HTTP服务器；因此常常将Tomcat与Apache等集成，前者作Servlet容器，后者处理静态资源，而AJP协议便负责Tomcat和Apache的连接。Tomcat与Apache
