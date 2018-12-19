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


* https://docs.docker-cn.com/get-started
* 镜像是一种轻量级、可执行的独立软件包，它包含运行某个软件所需的所有内容，包括代码、运行时、库、环境变量和配置文件
* 容器是镜像的运行时实例 - 实际执行时镜像会在内存中变成什么。默认情况下，它完全独立于主机环境运行，仅在配置为访问主机文件和端口的情况下才执行此操作
* 容器在主机内核上以本机方式运行应用。与仅通过管理程序对主机资源进行虚拟访问的虚拟机相比，它们具有更好的性能特征。容器可以获取本机访问，每个容器都在独立进程中运行，占用的内存不超过任何其他可执行文件
* 将可扩展单位做成单个可移植的可执行文件，具有广泛的意义。它表示，CI/CD 可以将更新推送到分布式应用程序的任何部分，您无需担心系统依赖项，并且资源密度将增加。编排扩展动作将启动新的可执行文件而不是新的虚拟主机
* 如果要开始编写 Python 应用，您的第一项业务是将 Python 运行时安装到机器上。但是，这会导致机器上的环境必须如此，才能使应用按预期运行；对于运行应用的服务器来说，也同样如此。
* 借助 Docker，您只需将可移植的 Python 运行时抓取为镜像，而无需进行安装。然后，您的构建可以将基本 Python 镜像与应用代码包含在一起，从而确保应用、其依赖项及运行时都一起提供。这些可移植的镜像由 Dockerfile 定义
* 运行构建命令。这将创建 Docker 镜像，我们将使用 -t 对其进行标记，以使其具有友好名称: docker build -t friendlyhello .
* 运行应用，使用 -p 参数将机器的 4000 端口映射到容器暴露的 80 端口:docker run -p 4000:80 friendlyhello

---
* 计算、存储、网络 敏捷服务、规模处理 machine、compose、swarm、kubernetes、Mesos、CoreOS、DevOps、openstack
* 用户需求越来越多样、系统规模越来越大、运行软件越来越复杂
* 各种滑稽和配置引发的bug
* 在云时代，凭借虚拟化技术所构建的集群处理能力，Go语言实现的开源容器项目；docker容器的生态体系
* 对应用封装、分发、部署、运行生命周期进行管理，达到应用组件一次封装，到处运行的目的
* 每个容器内运行着一个应用，不通的容器相互隔离，容器质检可以网络通信；很多时候直接把容器当作应用本身没有任何问题
* 在云时代，开发者创建的应用必须要很方便地在网络上传播，之前应用直接运行在底层操作系统上，无法保证同一份应用在不通的环境中行为一致
* docker镜像类似于虚拟机镜像，可以将它理解为一个只读模板；docker提供了一套机制来创建和更新现有的镜像，用户甚至可以从网上下载一个已经做好的应用镜像，并直接使用
* docker容器类似于一个沙箱，docker利用容器来运行和隔离应用，容器是从镜像创建的应用运行实例；容器从镜像启动时，会在镜像的最上层创建一个可写层
* docker仓库类似于代码仓库，它是docker集中存放镜像文件的场所；每个仓库集中存放某一类镜像
* ubuntu、debian、centos、redhat
* uname -a   cat /proc/version
* apt-get install -y docker-engine
* sudo curl -sSL https://get.docker.com/ | sh
* sudo service docker start
* docker pull NAME[:TAG]
* docker pull registry.hub.docker.com/ubuntu:14.04
* 创建镜像：基于已有镜像容器创建，基于本地模板导入、基于dockerfile创建
* 在使用-d参数时，容器启动后悔进入后台，用户无法看到容器中的信息，页无法进行操作；这个时候需要进入容器进行操作：attach、exec、nsenter
