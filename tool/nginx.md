# nginx
* https://www.cnblogs.com/sybblogs/p/6085314.html
* https://blog.csdn.net/jiede1/article/details/81094916
* http://rpm.pbone.net/
* https://blog.csdn.net/mahoking/article/details/80058052
* https://www.cnblogs.com/wyd168/p/6636529.html


* http://nginx.org/en/download.html
* 启动(windows)：
1. 双击nginx.exe
2. cmd命令窗口，输入命令 nginx.exe 或者 start nginx
* 检查是否启动：
1. 访问http://localhost:80
2. cmd命令窗口，tasklist /fi "imagename eq nginx.exe"
* 关闭nginx：
1. 输入nginx命令  nginx -s stop(快速停止nginx)  或  nginx -s quit(完整有序的停止nginx)
2. 使用taskkill   taskkill /f /t /im nginx.exe
* 检查80端口是否被占用：netstat -ano | findstr 0.0.0.0:80 或 netstat -ano | findstr "80"
* 使用nginx代理服务器做负载均衡：
upstream proxy_test {
        ip_hash;  # ip_hash（訪问ip）每一个请求按訪问ip的hash结果分配。这样每一个訪客固定訪问一个后端服务器，能够解决session的问题
        # fair; # 按后端服务器的响应时间来分配请求。响应时间短的优先分配
        # url_hash; # 按訪问url的hash结果来分配请求，使每一个url定向到同一个后端服务器。后端服务器为缓存时比較有效
        # hash $request_uri; # 在upstream中加入hash语句。server语句中不能写入weight等其他的參数，hash_method是使用的hash算法
        # hash_method crc32; 
        server localhost:3000 weight=2;
        server localhost:3001 weight=1;
        
        # upstream还能够为每一个设备设置状态值，这些状态值的含义分别例如以下：
        # down 表示单前的server临时不參与负载.
        # weight 默觉得1.weight越大，负载的权重就越大。
        # max_fails ：同意请求失败的次数默觉得1.当超过最大次数时，返回proxy_next_upstream 模块定义的错误.
        # fail_timeout : max_fails次失败后。暂停的时间。
        # backup： 其他全部的非backup机器down或者忙的时候，请求backup机器。所以这台机器压力会最轻
    }
location = / {
            proxy_pass http://proxy_test;
        }
location / { 
            root  html; 
            index  index.html index.htm; 
            proxy_pass http://linuxidc; 
}
* 图片文件结尾的走文件服务器，动态页面走web服务器，只要你正则写的没问题，又有相对应的服务器解决方案，你就可以随心所欲的玩
* 如果被分发的服务器存在异常，他可以将请求重新转发给另外一台服务器，然后自动去除异常服务器
* Ip hash算法，对客户端请求的ip进行hash操作，然后根据hash结果将同一个客户端ip的请求分发给同一台服务器进行处理，可以解决session不共享的问题
* Nginx可以对不同的文件做不同的缓存处理，配置灵活，并且支持FastCGI_Cache，主要用于对FastCGI的动态程序进行缓存。配合着第三方的ngx_cache_purge，对制定的URL缓存内容可以的进行增删管理
* conf：
########### 每个指令必须有分号结束。#################
#user administrator administrators;  #配置用户或者组，默认为nobody nobody。
#worker_processes 2;  #允许生成的进程数，默认为1
#pid /nginx/pid/nginx.pid;   #指定nginx进程运行文件存放地址
error_log log/error.log debug;  #制定日志路径，级别。这个设置可以放入全局块，http块，server块，级别以此为：debug|info|notice|warn|error|crit|alert|emerg
events {
    accept_mutex on;   #设置网路连接序列化，防止惊群现象发生，默认为on
    multi_accept on;  #设置一个进程是否同时接受多个网络连接，默认为off
    #use epoll;      #事件驱动模型，select|poll|kqueue|epoll|resig|/dev/poll|eventport
    worker_connections  1024;    #最大连接数，默认为512
}
http {
    include       mime.types;   #文件扩展名与文件类型映射表
    default_type  application/octet-stream; #默认文件类型，默认为text/plain
    #access_log off; #取消服务日志    
    log_format myFormat '$remote_addr–$remote_user [$time_local] $request $status $body_bytes_sent $http_referer $http_user_agent $http_x_forwarded_for'; #自定义格式
    access_log log/access.log myFormat;  #combined为日志格式的默认值
    sendfile on;   #允许sendfile方式传输文件，默认为off，可以在http块，server块，location块。
    sendfile_max_chunk 100k;  #每个进程每次调用传输数量不能大于设定的值，默认为0，即不设上限。
    keepalive_timeout 65;  #连接超时时间，默认为75s，可以在http，server，location块。

    upstream mysvr {   
      server 127.0.0.1:7878;
      server 192.168.10.121:3333 backup;  #热备
    }
    error_page 404 https://www.baidu.com; #错误页
    server {
        keepalive_requests 120; #单连接请求上限次数。
        listen       4545;   #监听端口
        server_name  127.0.0.1;   #监听地址       
        location  ~*^.+$ {       #请求的url过滤，正则匹配，~为区分大小写，~*为不区分大小写。
           #root path;  #根目录
           #index vv.txt;  #设置默认页
           proxy_pass  http://mysvr;  #请求转向mysvr 定义的服务器列表
           deny 127.0.0.1;  #拒绝的ip
           allow 172.18.5.54; #允许的ip           
        } 
    }
}
* linux
* sudo nginx
* nginx -s reload(重启)|reopen(从新打开日志文件)|stop|quit(优雅停止nginx)
* nginx -t
* nginx -v
* nginx -h
* nginx -V 详细版本信息，包括编译参数
* nginx  -c filename  指定配置文件
* netstat -ntlp|grep 7443
* ps -ef |grep nginx
* whereis nginx
* ./nginx
* kill -term 主进程号  ---> 快速停止
* pkill -9 nginx   ---> 强制停止
* 301的含义是“永久重定向”，而302的含义是“临时重定向”
* 301跳转设置：
server {
listen 80;
server_name xxx.com;
rewrite ^/(.*) http://72xit.com/$1 permanent;
access_log off;
}
* 302跳转设置：
server {
listen 80;
server_name xxx.com;
rewrite ^/(.*) http://72xit.com/$1 redirect;
access_log off;
}
* rewrite regex URL [flag];
rewrite是关键字，regex是正则表达式，URL是要替代的内容，[flag]是标记位的意思，它有以下几种值：
last: 相当于Apache的[L]标记，表示完成rewrite
break: 停止执行当前虚拟主机的后续rewrite指令集
redirect: 返回302临时重定向，地址栏会显示跳转后的地址
permanent: 返回301永久重定向，地址栏会显示跳转后的地址
* 
if ($http_user_agent ~ MSIE) {
    rewrite ^(.*)$ /msie/$1 break;
} //如果UA包含"MSIE"，rewrite请求到/msid/目录下
 
if ($http_cookie ~* "id=([^;]+)(?:;|$)") {
    set $id $1;
 } //如果cookie匹配正则，设置变量$id等于正则引用部分
 
if ($request_method = POST) {
    return 405;
} //如果提交方法为POST，则返回状态405（Method not allowed）。return不能返回301,302
 
if ($slow) {
    limit_rate 10k;
} //限速，$slow可以通过 set 指令设置
 
if (!-f $request_filename){
    break;
    proxy_pass  http://127.0.0.1; 
} //如果请求的文件名不存在，则反向代理到localhost 。这里的break也是停止rewrite检查
 
if ($args ~ post=140){
    rewrite ^ http://mysite.com/ permanent;
} //如果query string中包含"post=140"，永久重定向到mysite.com
* $args： #这个变量等于请求行中的参数，同$query_string
$content_length： 请求头中的Content-length字段。
$content_type： 请求头中的Content-Type字段。
$document_root： 当前请求在root指令中指定的值。
$host： 请求主机头字段，否则为服务器名称。
$http_user_agent： 客户端agent信息
$http_cookie： 客户端cookie信息
$limit_rate： 这个变量可以限制连接速率。
$request_method： 客户端请求的动作，通常为GET或POST。
$remote_addr： 客户端的IP地址。
$remote_port： 客户端的端口。
$remote_user： 已经经过Auth Basic Module验证的用户名。
$request_filename： 当前请求的文件路径，由root或alias指令与URI请求生成。
$scheme： HTTP协议（如http，https）。
$server_protocol： 请求使用的协议，通常是HTTP/1.0或HTTP/1.1。
$server_addr： 服务器地址，在完成一次系统调用后可以确定这个值。
$server_name： 服务器名称。
$server_port： 请求到达服务器的端口号。
$request_uri： 包含请求参数的原始URI，不包含主机名，如：”/foo/bar.php?arg=baz”。
$uri： 不带请求参数的当前URI，$uri不包含主机名，如”/foo/bar.html”。
$document_uri： 与$uri相同。
* 301永久定向到新域名: 
server {
    listen 80;
    listen 443 ssl;
    server_name www.old-name.com old-name.com;
    return 301 $scheme://www.new-name.com;
}
以上代码实现了老域名301跳转到新域名上，假如网站要更换新域名的话使用此方法做301跳转
* http站点301跳转到https站点
server {
    listen 80;
    server_name www.mysite.com;
    return 301 https://www.mysite.com$request_uri;
}
* 和apache等web服务软件一样，rewrite的组要功能是实现RUL地址的重定向。Nginx的rewrite功能需要PCRE软件的支持，即通过perl兼容正则表达式语句进行规则匹配的
* rewrite    <regex>    <replacement>    [flag];
    关键字      正则        替代内容          flag标记
* last  #本条规则匹配完成后，继续向下匹配新的location URI规则
break  #本条规则匹配完成即终止，不再匹配后面的任何规则
redirect  #返回302临时重定向，浏览器地址会显示跳转后的URL地址
permanent  #返回301永久重定向，浏览器地址栏会显示跳转后的URL地址
* . 匹配除“\n”之外的任何单个字符，若要匹配包括“\n”在内的任意字符，请使用诸如“[.\n]”之类的模式
---
* location区段
1. 没有修饰符 表示：必须以指定模式开始：location /abc {}
2. =表示：必须与指定的模式精确匹配：location = /abc {}
3. ~ 表示：指定的正则表达式要区分大小写：location ~ ^/abc$ {}
4. ~* 表示：指定的正则表达式不区分大小写：location ~* ^/abc$ {}
5. ^~ 类似于无修饰符的行为，也是以指定模式开始，不同的是，如果模式匹配，那么就停止搜索其他模式了
5. @ 定义命名location区段，这些区段客户段不能访问，只可以由内部产生的请求来访问，如try_files或error_page
* 查询顺序和优先级
1. 带有“=“的精确匹配优先
2. 没有修饰符的精确匹配
3. 正则表达式按照他们在配置文件中定义的顺序
4. 带有“^~”修饰符的，开头匹配
5. 带有“~” 或“~*” 修饰符的，如果正则表达式与URI匹配
6. 没有修饰符的，如果指定字符串与URI开头匹配
* location /img/ {
    alias /var/www/image/;
}
访问/img/目录里面的文件时，ningx会自动去/var/www/image/目录找文件
* location /img/ {
    root /var/www/image;
}
访问/img/目录下的文件时，nginx会去/var/www/image/img/目录下找文件
* alias是一个目录别名的定义，root则是最上层目录的定义
* 还有一个重要的区别是alias后面必须要用“/”结束，否则会找不到文件的。。。而root则可有可无~~
* 安装nginx
1. tar -zxvf nginx-1.10.3.tar.gz
2. cd nginx-1.10.3 进入nginx的目录
3. ./configure 运行nginx配置文件(如果出现错误,可能缺少库文件,安装后再执行这一步)
4. su 进入root权限,回车后输入密码
5. cd / 进入到根目录
6. yum -y install gcc gcc-c++ autoconf automake 安装gcc和gcc-c++(-y安装时选择同意选项,autoconf automake 自动配置自动安装,出现complete安装成功)
7. yum -y install pcre pcre-devel 安装pcre库
8. yum -y install zlib zlib-devel 安装zlip库
9. ./configure 进入到nginx目录再运行一次,直到成功后
10. make 编译
11. make install 安装nginx
11. cd /usr/local->ls 查看是否有nginx,如果有则安装完成
12. cd nginx conf目录放着配置文件 htmL放着网页程序 logs放着日志文件 sbin放着nginx的启动程序
13. /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf 启动nginx
