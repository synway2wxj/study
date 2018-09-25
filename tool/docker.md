#docker
---
* 让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux 机器上，便可以实现虚拟化
* Web 应用、后台应用、数据库应用、大数据应用比如 Hadoop 集群、消息队列等等都可以打包成一个镜像部署
* Docker 容器通过 Docker 镜像来创建，Docker 镜像是用于创建 Docker 容器的模板；容器是独立运行的一个或一组应用；Docker 仓库用来保存镜像
* Ubuntu、CentOS、Windows、MacOS
* 启动服务：sudo service docker start，运行：docker run hello-world
* Docker 允许你在容器内运行应用程序， 使用 docker run 命令来在容器内运行一个应用程序（docker run -i -t -d -P ubuntu:15.10 /bin/echo "Hello world"）
* docker stop，docker ps，docker logs -f，docker status，docker port， docker top，docker start，docker search
* docker run -d -p 5000:5000 training/webapp python app.py
* docker pull ubuntu:13.10；下载完成后，我们可以直接使用这个镜像来运行容器
* docker run -d -p 127.0.0.1:5000:5000/udp --name runoob training/webapp python app.py
* Docker 执行 docker run 之后，先在当前操作系统的基础上，虚拟化了一个精简版的linux(仅仅包含系统运行的最精简功能)，然后加载我们的Nginx镜像。当Nginx镜像加载到我们的虚拟Linux环境中时，相当于在系统里执行了一个脚本，而这个脚本就是Nginx。由于默认的Nginx 是不作为守护进程运行的。所以当Docker内监听到80端口的请求后，完成之后，就退出了Nginx的进程。该容器内只有一个进程，并且是非守护的，执行完请求进程就销毁了。那么这个容器也就没有存在的必要了，所以Docker 中这个服务也就停掉了。这也就是我们执行 docker top 看不到当前运行的容器的原因
* -i 保证容器的stdin开启-t 为容器生成一个tty终端，在命令的最后加一个/bin/bash来保证可以交互。但是实际上，nginx并没有运行，导致我以为容器的端口绑定不是持久化的
* docker exec -it c0462d5e1878 bash
