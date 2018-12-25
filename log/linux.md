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
# rocketmq
# oracle
# nginx
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
