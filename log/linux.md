* mv A B 将目录A重命名为B
* mv /a /b/c  将/a目录移动到/b下，并重命名为c
*  /sbin/iptables -I INPUT -p tcp --dport 8080 -j ACCEPT
/etc/rc.d/init.d/iptables save
/etc/init.d/iptables restart
/sbin/iptables -L -n
* 1、/sbin/iptables -I INPUT -p tcp --dport 3306 -j ACCEPT
2、# /etc/init.d/iptables restart
3、# /etc/rc.d/init.d/iptables save
* 修改vim /etc/sysconfig/iptables文件，增加如下一行：
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 要开启的端口 -j ACCEPT
重启    iptables
命令：  service iptables restart
vi /etc/sysconfig/iptables
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT
/etc/init.d/iptables restart
/sbin/iptables -L -n
* firewall-cmd --zone=public --add-port=80/tcp --permanent
重启防火墙：
systemctl restart firewalld.service
systemctl stop firewalld.service

---
* netstat -an | grep 端口 或 netstat -tunlp |grep 端口 或 netstat -apn | grep 25
* 关闭端口号:iptables -A OUTPUT -p tcp --dport 端口号-j DROP
* 打开端口号：iptables -A INPUT -ptcp --dport  端口号-j ACCEPT
* 查看端口是否对外开放：
nc 127.0.0.1 25 #不是对外开放状态
* （1）通过vi /etc/sysconfig/iptables 进入编辑增添一条-A INPUT -p tcp -m tcp --dport 8889 -j ACCEPT 即可
（2）执行 /etc/init.d/iptables restart 命令将iptables服务重启
（3）保存 /etc/rc.d/init.d/iptables save
* 开放某一端口断：
编辑 /etc/sysconfig/iptables
-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 20:30-j ACCEPT
（一、 xx:yy   表示xx到yy之间的所有端口
二、 :xx    表示xx及以下所有端口
三、 xx:    表示xx以及以上所有端口）
最后重启防火墙： service iptables restart
* netstat -nupl  (UDP类型的端口)
netstat -ntpl  (TCP类型的端口)
netstat -anp 显示系统端口使用情况
lsof -i :port，使用lsof -i :port就能看见所指定端口运行的程序，同时还有当前连接。
* tar zxvf /bbs.tar.zip -C /zzz/bbs
* vi快捷键：
x 删除光标处的字符
dd 删除整行
u 撤销最后一次修改
a 在光标后插入文本
:e! 放弃所有修改，从上次保存开始处再编辑
:q! 不保存退出
/pattern：从光标开始处向文件尾搜索pattern
?pattern：从光标开始处向文件首搜索pattern
G    移到文件的最后一行
nG    移到文件的第n行
L    移到屏幕的最后一行
M    移到屏幕的中间一行
H    移到屏幕的第一行
:set ic    查找时忽略大小写
:set noic   查找时对大小写敏感
:set nu    每行前打印行号
:set showmode   显示是输入模式还是替换模式
:s/oldtext/newtext 用newtext替换oldtext
yy    将当前行的内容放入临时缓冲区
nyy    将n行的内容放入临时缓冲区
u    撤消最后一次修改
U    撤消当前行的所有修改
.    重复最后一次修改
:.=    打印当前行的行号
Ctrl+u：向文件首翻半屏 
Ctrl+d：向文件尾翻半屏 
Ctrl+f：向文件尾翻一屏 
Ctrl＋b；向文件首翻一屏 
nz：将第n行滚至屏幕顶部，不指定n时将当前行滚至屏幕顶部
*  cp -R file1 file2 file3 dir1 dir2
cp -P  /var/tmp/a.txt  ./temp/复制时保留文件的目录结构

# redis
* string、list、set、zset和hash
* http://redis.io/download  
* tar zxvf redis.tar.gz    cd redis    make(编译)    cd src  make install   ./redis-server   pkill redis-server  redis-cli 
redis-cli shutdown  netstat -tunpl|grep 6379
* 编译完成之后，可以看到解压文件redis中会有对应的src、conf等文件夹；；编译成功后，进入src文件夹，执行make install进行Redis安装；；首先为了方便管理，将Redis文件中的conf配置文件和常用命令移动到统一文件中；；mkdir -p /usr/local/redis/bin；；mkdir -p /usr/local/redis/ect
* 当Redis以守护进程方式运行时，Redis默认会把pid写入/var/run/redis.pid文件，可以通过pidfile指定pidfile /var/run/redis.pid
* 当 客户端闲置多长时间后关闭连接，如果指定为0，表示关闭该功能timeout 300
* 指定日志记录级别，Redis总共支持四个级别：debug、verbose、notice、warning，默认为verbose;loglevel verbose
* 启动redis服务需要从后台启动，并且指定启动配置文件，将daemonize属性改为yes；redis-server /usr/local/redis/etc/redis.conf
* 设置当本机为slav服务时，设置master服务的IP地址及端口，在Redis启动时，它会自动从master进行数据同步slaveof <masterip> <masterport>
* 当master服务设置了密码保护时，slav服务连接master的密码masterauth <master-password>
* 设置Redis连接密码，如果配置了连接密码，客户端在连接Redis时需要通过AUTH <password>命令提供密码，默认关闭requirepass foobared
* 指定是否在每次更新操作后进行日志记录，Redis在默认情况下是异步的把数据写入磁盘，如果不开启，可能会在断电时导致一段时间内的数据丢失。因为 redis本身同步数据文件是按上面save条件来同步的，所以有的数据会在一段时间内只存在于内存中。默认为no;appendonly no
* 指定更新日志条件，共有3个可选值： 
    no：表示等操作系统进行数据缓存同步到磁盘（快） 
    always：表示每次更新操作后手动调用fsync()将数据写到磁盘（慢，安全） 
    everysec：表示每秒同步一次（折衷，默认值）
appendfsync everysec
* 指定包含其它的配置文件，可以在同一主机上多个Redis实例之间使用同一份配置文件，而同时各个实例又拥有自己的特定配置文件
  include /path/to/local.conf
* ./redis-server /usr/local/redis/etc/redis.conf
* service redis start
service redis stop
* wget http://download.redis.io/releases/redis-2.8.3.tar.gz
* service iptables stop
  vi /etc/sysconfig/iptables
  -A INPUT -m state --state NEW -m tcp -p tcp --dport 6379 -j ACCEPT
  service iptables restart
* 需要gcc环境，如果没有执行命令安装gcc：yum install gcc-c++；；tar -zxvf redis-3.0.0.tar.gz；；进入解压目录编译，make；；make install PREFIX=/usr/local/redis；；./redis-server redis.conf；；安装ruby环境，yum install ruby，yum install rubygems，gem install redis-3.0.0.gem；；在local下创建redis-cluster文件夹，在该文件夹中创建6个redis实例，端口号从7001~7006；；修改redis01至redis06中的redis.conf 文件，将端口依次改为70001~7006，并打开cluster-enabled yes行前的注释；；./redis-trib.rb create --replicas 1 
 192.168.242.134:7001
 192.168.242.134:7002
 192.168.242.134:7003
 192.168.242.134:7004
 192.168.242.134:7005
 192.168.242.134:7006；；redis01/redis-cli -h 192.168.25.153 -p 7002 -c
* redis-trib.rb是redis官方推出的管理redis集群的工具，集成在redis的源码src目录下；；yum install ruby；；yum install rubygems      (ruby包的管理器,用来下载ruby的包)；；安装ruby包redis-3.3.0.gem；；执行gem install redis-3.0.0.gem命令安装；；redis-trib.rb  create--replicas 1  10.180.157.199:6379   10.180.157.200:6379   10.180.157.201:6379   10.180.157.202:6379  10.180.157.205:6379    10.180.157.208:6379 ；；mkdir redis-cluster ；；进入usr/local/redis，把redis-cli、redis-server、redis.conf复制到/usr/local/redis-cluster/redis01目录；；./redis-trib.rb  create --replicas  1  127.0.0.1:7001  127.0.0.1:7002  127.0.0.1:7003  127.0.0.1:7004  127.0.0.1:7005   127.0.0.1:7006；； redis01/redis-cli -h 192.168.25.153 -p 7002 –c
# rocketmq(http://rocketmq.apache.org/)
* RocketMQ默认采用长轮询的拉模式，单机支持千万级别的消息堆积;;rocketmq集群包括nameserver和broker，nameserver负责管理集群的列表信息，broker是真正作为消息承载和提供数据吞吐服务的；；日志，默认位置在：~/logs/rocketmqlogs/namesrv.log；；执行 jps 可以看到NamesrvStartup，就是nameserver进程；；nohup ./bin/mqbroker -n monchickey:9876 &；；可以先编辑bin/mqbroker会看到最后还是调用了bin/runbroker.sh，这里打开bin/runbroker.sh；；对于nameserver和broker日志位置都可以手动配置，具体配置文件就是conf下的logback_broker.xml和logback_namesrv.xml；；其中2m表示2个master，2s表示2个slave，sync表示同步刷盘，asyna表示异步刷盘和replication，默认情况下rocketmq是async模式的，这样性能会非常好，但是如果需要保证消息的可靠性，建议使用sync的方式；；这里第一个是集群名称，一个集群必须配置一个，默认就是DefaultCluster，然后brokerName是broker的名称，master的话brokerId为0，其余的slave依次是1,2,3往后排，然后brokerRole配置表示异步的往slave拷贝，如果是slave节点直接写SLAVE即可；；nohup bin/mqbroker -c ./conf/broker1.properties -n monchickey:9876 &；；bin/mqadmin clusterList -n monchickey:9876；；bin/mqadmin brokerStatus -c DefaultCluster -n monchickey:9876 
* 调整一下bin目录下的runbroker.sh 和 runserver.sh的参数
* export rocketmq=/soft/RocketMQ/rocketmq-rocketmq-all-4.2.0/distribution/target/apache-rocketmq  -server -Xms256m -Xmx256m -Xmn256m
  -server -Xms128m -Xmx128m -Xmn128m -XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=256m
* nohup sh mqnamesrv >/soft/RocketMQ/rocketmqlogs/mqnamesrv.log 2>&1 &
  nohup sh mqbroker -n localhost:9876 >/soft/RocketMQ/rocketmqlogs/broker.log 2>&1 &  
  sh bin/mqshutdown broker    //停止 broker
  sh bin/mqshutdown namesrv   //停止 nameserver
  查看集群情况 ./mqadmin clusterList -n 127.0.0.1:9876
  查看 broker 状态 ./mqadmin brokerStatus -n 127.0.0.1:9876 -b 172.20.1.138:10911
  查看 topic 列表 ./mqadmin topicList -n 127.0.0.1:9876
  查看 topic 状态 ./mqadmin topicStatus -n 127.0.0.1:9876 -t MyTopic
  查看 topic 路由 ./mqadmin topicRoute -n 127.0.0.1:9876 -t MyTopic
  安装web可视化客户端：https://github.com/apache/rocketmq-externals
  find -name application.properties 可以查看到两个文件都在rocketmq-console文件目录下
vim application.properties
  rocketmq.config.namesrvAddr=192.168.143.128:9876（ip1:port;ip2:port）
    编译(usr/local/rocketmq-externals-master/rocketmq-console/目录下)：：mvn clean package -Dmaven.test.skip=true
    java -jar rocketmq-console-ng-1.0.0.jar 启动 ---当终端断了该服务就会停止
    nohup java -jar rocketmq-console-ng-1.0.0.jar >>/soft/RocketMQ/rocketmqlogs/log.out 2>&1 &；；http://192.168.143.128:8080
    
unzip rocketmq-all-4.1.0-incubating-bin-release.zip
mv rocketmq-all-4.1.0-incubating /monchickey/
cd /monchickey/rocketmq-all-4.1.0-incubating/
* bin/mqbroker -c ./conf/2m-2s-sync/broker-a.properties -n rocket1:9876,rocket2:9876
bin/mqbroker -c ./conf/2m-2s-sync/broker-a-s.properties -n rocket1:9876,rocket2:9876
bin/mqbroker -c ./conf/2m-2s-sync/broker-b.properties -n rocket1:9876,rocket2:9876
bin/mqbroker -c ./conf/2m-2s-sync/broker-b-s.properties -n rocket1:9876,rocket2:9876
* jdk  maven rocketMQ　　
* tar zxf alibaba-rocketmq-3.2.4-beta1.tar.gz -C /usr/local/
cd /usr/local/
ln -s /usr/local/alibaba-rocketmq /usr/local/rocketmq
cd rocketmq/
hostname
vim conf/2m-noslave/broker-a.properties
vim bin/runbroker.sh
mkdir -p /data/rocketmq/store/commitlog
mkdir /data/logs
sed -i 's#${user.home}#/data#g' *.xml　　　　　　//将conf目录下所有xml文件中的${user.home}替换成/data
nohup sh mqnamesrv >/var/log/ns.log &
nohup sh mqbroker -c ../conf/2m-noslave/broker-a.properties > /var/log/mq.log 2>&1 &
# oracle
# nginx
* 安装nginx前，我们首先要确保系统安装了g++、gcc、openssl-devel、pcre-devel和zlib-devel软件
yum install gcc-c++
yum -y install zlib zlib-devel openssl openssl--devel pcre pcre-devel
wget https://nginx.org/download/nginx-1.11.3.tar.gz
我们一般安装linux软件都会在/usr/local目录下，然后进行解压编译安装：
tar -zxvf nginx-1.11.3.tar.gz
mv nginx-1.11.3 /usr/local/nginx-1.11.3
./configure --prefix=/usr/local/nginx（安装到/usr/local/nginx的nginx目录下）
make
make install
nginx -c nginx.conf或者./nginx
ps -ef|grep nginx
kill -quit xxx 或者 kill -term xxx
pkill -9 nginx
nginx -s reload

* listen：表示当前的代理服务器监听的端口，默认的是监听80端口。注意，如果我们配置了多个server，这个listen要配置不一样
server_name：表示监听到之后需要转到哪里去，这时我们直接转到本地，这时是直接到nginx文件夹内
location：表示匹配的路径，这时配置了/表示所有请求都被匹配到这里
root：里面配置了root这时表示当匹配这个请求的路径时，将会在这个文件夹内寻找相应的文件，这里对我们之后的静态文件伺服很有用
index：当没有指定主页时，默认会选择这个指定的文件，它可以有多个，并按顺序来加载，如果第一个不存在，则找第二个，依此类推
upstream中的server元素必须要注意，不能加http://，但proxy_pass中必须加
在upstream中的local_tomcat中配置多一个server
upstream local_tomcat {  
    server localhost:8080 weight=1;  
    server localhost:9999 weight=5;  
} 
* cd /usr/local/src
wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.39.tar.gz 
tar -zxvf pcre-8.37.tar.gz
cd pcre-8.34
./configure
make
make install
* cd /usr/local/src
wget http://zlib.net/zlib-1.2.11.tar.gz
tar -zxvf zlib-1.2.11.tar.gz
cd zlib-1.2.11
./configure
make
make install
* cd /usr/local/src
wget https://www.openssl.org/source/openssl-1.0.1t.tar.gz
tar -zxvf openssl-1.0.1t.tar.gz
* cd /usr/local/src
wget http://nginx.org/download/nginx-1.1.10.tar.gz
tar -zxvf nginx-1.1.10.tar.gz
cd nginx-1.1.10
./configure
make
make install
* apt-get install openssl
apt-get install libssl-dev
yum -y install openssl openssl-devel
* netstat -ano|grep 80
* ./nginx -t
./nginx -s reload
whereis nginx

# rpm
# aptget
# curl
# 重启加载
# 共享
# 定时任务
# kafaka
# memcache
# docker
# 端口
# mogodb
# linux自启动服务
