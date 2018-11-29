# java生态圈
* 大多数人成为某领域顶级专家可能会有些难度，但应对日常工作，成长为资深研发工程师、技术专家、甚至成为小团队的Team Leader，其实并不难
多读书、多看报，多研究常用开源框架的源码
* 基础知识：java、spring、spring boot、spring cloud、ibatis、设计模式、Log日志
* 数据库：连接池、事务、分库分表、id生成器、DAO层接口性能监控、读写分离、sql技巧
* web容器/协议/网络：负载均衡、Nginx、tomcat、http协议、CDN
* 常用三方工具包：Google Guava、fastJson、log4J、commons-codec、commons-lang3、commons-io、Quartz、HttpClient、Javassist
* 中间件-RPC框架：dubbo、dubbox、motan、Thrift、RPC框架性能比较
* 中间件-MQ消息：ActiveMQ、RabbitMQ、Kafka、RocketMQ
* 缓存：redis、codis、memcache
* 搜索：Elasticsearch
* 分布式数据框架：cobar、Mycat、tsharding、tddl、sharding-jdbc
* 分布式协调服务：zookeeper
* 大数据：Hbase、Spark、Hadoop、Hive、Flink
* 配置管理：super-diamond、disconf、apollo
* 分布式文件系统：FastDFS
* 其它：数据库binlog的增量订阅&消费组件、数据库同步系统
* 系统架构：架构经验、经典案例、通用技术方案选型、编码前3000问
* 项目管理：论需求调研的重要性、项目生命周期、项目管理案例、代码规范、git常用命令、ab性能压测、maven仓库
* 运维：快速排查线上问题、、linux常用命令、、本地代码调试、Docker
* 个人成长：Tom的读书单、个人成长与职业规划
* 学习网站：infoQ、云栖社区、并发编程网、开源中国、stackoverflow、慕课网、网易云课堂、腾讯课堂、github 伯乐在线
* 程序员素养
* 常用软件工具：一致性hash算法
* 面试：java面试题、大数据面试题

---
* Java组件,组件其实就是一个应用程序块但是它们不是完整的应用程序,不能单独运行

---
* 越来越多的同学进入大数据行业，有的是底层的技术，有的是工程，有的是算法，有的是业务
* 在大数据时代，要想个性化实现业务的需求，还是得操纵各类的大数据软件，如：hadoop、hive、spark、hbase、jstorm
* 熟悉ETL/流失计算/图计算/机器学习各种原理
* 修改各种引擎的核心代码，这些包括：hadoop/spark/flink/strom/hive/hbase/kafka
* https://dangdangdotcom.github.io/dubbox/rest.html
* Hadoop核心：HDFS(分布式存储基石)/MapReduce(分布式计算基础)/YARN(Hadoop集群资源管家)/Flume(离线日志收集利器)/Hive(离线批处理必备工具)
Impala(速度更快的Hive)/Spark(更快更强更好用的MR)/Kafka(流数据集成神器)/Spark Streaming(实时计算引擎)/HBase(海量数据高速存取数据库)
Sqoop，Kettle(ETL神器)/Oozie，Azkaban(任务调度双星)/Elasticsearch(大数据全文检索引擎)/数据仓库搭建/数据可视化(Tableau和ECharts)
算法(数据挖掘，机器学习，深度学习)

---
* Spark：计算引擎，框架媒介，调用配置所处位置下的机器的硬件设施来实现调用配置。使用内存来存储数据，运算快，断电丢失。对应于Hadoop圈中的MapReduce
* Hbase：分布式、面向列的数据库，存储和读取媒介，一个非结构化数据存储的数据库
* Hadoop：分布式系统基础框架，管理者。MapReduce使用硬盘存储数据
* Storm：流式实时计算框架，实时处理大数据流。不同于Hadoop和Spark，Storm不进行数据的收集和存储工作，它直接通过网络实时的接受数据并且实时的处理数据
然后直接通过网络实时的传回结果
* Oozie：一个基于工作流引擎的开源框架\
* Azkaban: 跟上面很像，Linkedin开源的面向Hadoop的开源工作流系统，提供了类似于cron 的管理任务
* 大数据：量大类多的数据集
* 大数据的技术基础：MapReduce（分布式计算框架）、Google File System（分布式文件系统）和BigTable（数据存储系统）
* 结构化数据：数字、符号等数据
* 非结构化数据：文本、图像、声音、视频等数据
* 大数据分析：可视化分析（百度地图春节人口迁移大数据）、
数据挖掘算法（沃尔玛啤酒与尿布、推荐、广告）、
预测性分析能力（金融分析、股票预测、气象预测）、
语义引擎（siri）、数据质量管理（去假留真）
* 分布式计算：把一组计算机通过网络相互连接组成分散系统，然后将需要处理的大量数据分散成多个部分，交由分散系统内的计算机组同时计算，
最后将这些计算结果合并得到最终的结果
* HDFS：Hadoop的分布式文件系统组件，运行在通用硬件上，使大量数据分布式存储到成千上百台机器
* Hive、SparkSQL、Pig：数据仓库系统
* YARN：为不同任务分配资源
* MLlib：Spark机器学习组件
* 大数据，首先你要能存的下大数据；存的下数据之后，你就开始考虑怎么处理数据(MapReduce / Tez / Spark,
MapReduce是第一代计算引擎，Tez和Spark是第二代)
* Map阶段，几百台机器同时读取这个文件的各个部分，分别把各自读到的部分分别统计出词频;;Reducer机器A将从Mapper机器收到所有以A开头的统计结果
* 有了MapReduce，Tez和Spark之后，程序员发现，MapReduce的程序写起来真麻烦。他们希望简化这个过程。这就好比你有了汇编语言，
虽然你几乎什么都能干了，但是你还是觉得繁琐;于是就有了Pig和Hive;Pig是接近脚本方式去描述MapReduce，Hive则用的是SQL;
它们把脚本和SQL语言翻译成MapReduce程序，丢给计算引擎去计算，而你就从繁琐的MapReduce程序中解脱出来;有了Hive之后，人们发现SQL对比Java有巨大的优势;
Hive逐渐成长成了大数据仓库的核心组件。甚至很多公司的流水线作业集完全是用SQL描述;发现，Hive在MapReduce上跑，真**慢
* 于是Impala，Inceptor，Presto，Drill诞生了（当然还有无数非著名的交互SQL引擎);三个系统的核心理念是，MapReduce引擎太慢，因为它太通用，太强壮，太保守
* Hive on Tez / Spark和SparkSQL。它们的设计理念是，MapReduce慢，但是如果我用新一代通用计算引擎Tez或者Spark来跑SQL，那我就能跑的更快
* 底层HDFS，上面跑MapReduce／Tez／Spark，在上面跑Hive，Pig。或者HDFS上直接跑Impala，Inceptor，Drill，Presto。这解决了中低速数据处理的要求
* Streaming（流）计算。Storm是最流行的流计算平台。流计算的思路是，如果要达到更实时的更新，我何不在数据流进来的时候就处理了？比如还是词频统计的例子，
我的数据流是一个一个的词，我就让他们一边流过我就一边开始统计了。流计算很牛逼，基本无延迟，
但是它的短处是，不灵活，你想要统计的东西必须预先知道，毕竟数据流过就没了，你没算的东西就无法补算了
* 还有一个有些独立的模块是KV Store，比如Cassandra，HBase，MongoDB以及很多很多很多很多其他的;KV Store就是说，我有一堆键值，
我能很快速滴获取与这个Key绑定的数据。比如我用身份证号，能取到你的身份数据。这个动作用MapReduce也能完成，但是很可能要扫描整个数据集
* 还有一些更特制的系统／组件，比如Mahout是分布式机器学习库，Protobuf是数据交换的编码和库，ZooKeeper是高一致性的分布存取协同系统;
另外一个重要组件是，调度系统。现在最流行的是Yarn。你可以把他看作中央管理，好比你妈在厨房监工，哎，你妹妹切菜切完了，你可以把刀拿去杀鸡了。
只要大家都服从你妈分配，那大家都能愉快滴烧菜
* 大数据生态圈就是一个厨房工具生态圈。为了做不同的菜，中国菜，日本菜，法国菜，你需要各种不同的工具。
而且客人的需求正在复杂化，你的厨具不断被发明，也没有一个万用的厨具可以处理所有情况，因此它会变的越来越复杂

---
* 文件存储：Hadoop HDFS、Tachyon、KFS
* 离线计算：Hadoop MapReduce、Spark
* 流式、实时计算：Storm、Spark Streaming、S4、Heron、
* K-V、NOSQL数据库：HBase、Redis、MongoDB
* 资源管理：YARN、Mesos
* 日志收集：Flume、Scribe、Logstash、Kibana
* 消息系统：Kafka、StormMQ、ZeroMQ、RabbitMQ
* 查询分析：Hive、Impala、Pig、Presto、Phoenix、SparkSQL、Drill、Flink、Kylin、Druid
* 分布式协调服务：Zookeeper
* 集群管理与监控：Ambari、Ganglia、Nagios、Cloudera Manager
* 数据挖掘、机器学习：Mahout、Spark MLLib
* 数据同步：Sqoop
* 任务调度：Oozie

---
* 从生态圈来说：Hadoop生态圈、Spark生态圈、Storm
* 从任务类型来说：离线(批处理)、实时(流处理)
Hadoop是用来做离线任务处理的，Spark是既能做离线任务又能做实时任务的处理，其中Spark Streaming是用来实时处理数据的，
但是Spark Streaming只是一定意义上的实时，实际是很小的批量处理，而Storm则是真正意义上的实时流处理系统，来一条数据就会处理一条数据
* 从语言上来说：Java、Scala、Python、Go
大数据的大多数框架都是用Java编写的，这样编程的时候用Java自然能更简单，Storm也是用Java实现的
Spark生态圈是用Scala来实现的，Scala的语法简洁，代码量少
Python已经作为作为AI时代的首选语言，而且Spark也支持Python
Go语言是为大数据分布式而生的，Docker，K8S都是由Go打造的

---
* 云计算会在短则五年、长则十年的时间里将大部分运维的饭碗抢走；；从业务运维一步步转行去做云计算
* PaaS云代表了云计算的未来，PaaS云的优势浓缩成一个词就是——按需付费
* PaaS云彻底降低企业人力成本，选择用云主机只是省掉了扎网线的人力，但选择对象存储省掉的是存储架构师
* 互联网、物联网在各个行业得到了广泛应用，行业应用所产生了大量数据，这些数据的存储和管理已成了“互联网+”企业争夺的战略高地，云计算的市场规模随之扩大
* 第一阶段，中小企业通过云计算实现从“无”到“有”的IT功能；第二阶段，云计算成为企业级用户IT核心应用的补充资源（云服务器已逐渐获得企业和开发者信任）；
第三阶段，在原生应用、人工智能和物联网驱动下，云计算成为企业IT的核心资源
* 当前，大多数企业正处于云计算的第二阶段，越来越多的企业开始选择将业务部署到云服务器，借助云服务器独特的弹性、可扩展性、高可用性，谋求业务提升
* 大数据、人工智能、物联网等新技术的快速发展
* 云计算拥有“无限”的计算和存储资源池，但当面对广泛分布的大量终端及其所采集的海量数据时，也不可避免会遇到诸如核心网络拥堵、高延迟以及可靠性无法保证的难题
为此，作为云计算的延伸扩展，雾计算(Fog Computing)的概念应运而生。雾计算的原理是通过使用边缘网络中的设备，让基于云的服务可以离物联网和传感器更近。
通过雾计算，可以将一些并不需要放到云上的数据在网络边缘层直接进行处理和存储，提高数据分析处理的效率，降低时延，减少网络传输压力，提升安全性
* 不同工作负载运行在不同云上并被独立管理的多云模式将在2018成为主流，同时真正的混合云将开始涌现
* 云的好处之一就是易于使用增量的资源，并按消费模式付费
* 以前，额外计算资源的单位是一个实例或虚拟机。现在一个“函数”已经变成了一个更小的“使用”单位。
把云资源管理和按需扩展资源的责任放在了云服务提供商身上，既节约成本，又减轻IT运维的压力。而且根据消费支付对于已经紧张的预算来说更不敏感

---
* 云计算是一种通过网络以服务的方式提供动态可伸缩的IT资源的计算模式(可度量服务/资源池/按需自助服务/快速弹性)
* 云计算的应用模式：laas(Infrastructure as a Serivce) 基础设施 Infrastructure(网络、计算、存储、机房、环境、电源、散热和制冷)
Paas(Platform as a Service) 系统平台 Platform(应用服务器、应用框架、编程语言)
Saas(Software as a Service) 软件 Software(应用)
* 云计算的价值：智能资源调度(业务负载均衡、通过热迁移实现节能减排)
提高资源利用率(资源共享、分时共享)
分布式计算存储(分布式计算、分布式存储)
* 云计算机构关键技术：
```
超大规模资源调度算法
异构集成技术
应用无关的可靠性保障技术
单VM及多VM的弹性伸缩技术
计算近端IO性能加速技术
网络虚拟化技术
应用管理自动化技术
```
* 云计算是一种基于互联网的计算方式，通过这种方式，共享的软硬件资源和信息可以按需求提供给计算机和其它设备。云计算依赖资源的共享以达成规模经济
* 云是网络、互联网的一种比喻说法，计算可以理解为计算机，因此云计算的基本模型，就是远程计算服务：用户通过网络连接到计算机上，获取计算服务
* 1．计算能力。用户的个人计算机一台智能配置一颗CPU，但云计算远程调用的计算机集群可能有成百上千颗CPU，计算能力天壤之别。
2. 弹性的计算资源。个人电脑想要增加内存，只能重新买一根内存条来安装。而云计算的弹性伸缩能力，可以做到点下鼠标，内存就变成了8G。
3. 低廉的使用成本。由于规模效应，以及按需使用的分配原则，硬件成本低，资源闲置率也低，所以也进一步降低了云计算的使用成本
* 云计算提供的服务目前有三种方式：IaaS层，PaaS层以及SaaS层
1. IaaS(Infrastructure-as-a- Service)：基础设施即服务，常见形式是硬件服务器租用。阿里巴巴、腾讯、京东云鼎提供的就是IaaS层为主的云计算服务。
IaaS层的云服务配置灵活，但使用起来更为复杂，适合大型的、后台处理业务复杂的项目选用。IaaS层的服务目前基本已全面收费
2. PaaS(Platform-as-a- Service)：平台即服务，常见形式是提供Web托管的应用引擎;PaaS层是最适合多数开发者选用的云计算服务。
PaaS层可以被理解为在IaaS层提供的硬件服务之上，还额外搭建好了服务器环境、中间件、数据库等。开发者用户只需要将网页代码上传部署，
网站就可以运行起来了，既降低了IT运维成本，还省去了大量的开发与运维工作量。PaaS平台目标的产品包括：京东云擎（JAE)、BAE、SAE
3. SaaS(Software-as-a- Service)：软件即服务，常见的形式是提供Web端应用，按需购买使用，著名的CRM服务提供商Salesforce就是此类代表。
国内提供SaaS服务的包括阿里云、京东电商云、新浪云商店
* 云计算的演进历程：并行计算、分布式计算、网格计算
* CRM：Customer Telationship Management，客户关系管理
* IaaS：Infrastructure as a Service，基础设施即服务
* PaaS：Platform as a Service，平台即服务
* SaaS：Software as a Service ，软件即服务
* EC2：Elastic Compute Cloud，弹性计算云
* IDC：International Data Center，互联网数据中心
* TC：Thin Client，瘦客户端
* ECS：Elastic Compute Service，弹性计算服务
* SLB：Service Load Balancer，负载均衡
* RDS：Relationship Database Service，关系型数据库服务
* OSS：Open Storage Service，开发存储服务
* CDN：Content Delivery Network， 内容分发网络
* ICP：Internet Content Provider，互联网内容提供商
* DC：Data Center，数据中心
* 谷歌声称它的任务是编辑全球的信息，让这些信息在全球的任何地方都能访问和使用
* 提供资源的网络被称为“云”。“云”中的资源在使用者看来是可以无限扩展的，并且可以随时获取，按需使用，随时扩展，按使用付费。
这种特性经常被称为像水电一样使用IT基础设施
* 广义云计算是指服务的交付和使用模式，指通过网络以按需、易扩展的方式获得所需的服务。这种服务可以是IT和软件、互联网相关的，也可以是任意其他的服务
* 资源池称为“云”。“云”是一些可以自我维护和管理的虚拟计算资源，通常为一些大型服务器集群，
包括计算服务器、存储服务器、宽带资源等等。云计算将所有的计算资源集中起来，并由软件实现自动管理，无需人为参与。
这使得应用提供者无需为繁琐的细节而烦恼，能够更加专注于自己的业务，有利于创新和降低成本
* 云计算是一个系统、复杂的工程，各个层面相互配合，软硬结合，不断积累才能够构建出稳定、可靠、高速、安全的云计算基础设施

---
# node.js
* Nodejs是一个高性能JavaScript脚本运行环境，内部基于Chrome V8脚本引擎。它相当于把在浏览器中执行JavaScript脚本的功能抽取出来，作为一个单独的程序，可在桌面端命令行等环境中使用
* NPM是nodejs包管理器(nodejs package manager)，目前已为全球最大的开源脚本仓库
* 文件操作/网络操作/进程管理/异步编程/
* 构建工具：grunt、gulp、bower、browserify、webpack
* 测试代码：Mocha、Jasmine、Chai、Tape、Karma、Selenium、phantomjs
* webpack
* angularjs
* react
* gulp
* bower
* typescript
* vue
* es5、es6
* sass
* less
* VS Code

---
* npm init
* npm install –g typescript
* npm install –g typings
* npm config set registry https://registry.npm.taobao.org
* React是一个前端mvvm框架，它可以使前端开发更加组件化，更加有利于前端控件的维护和共用
* JSX语法是一种语法糖，它允许直接将HTML结构代码写在javascript脚本中，将html代码和javascript代码混合写在一起
* TypeSciprt是一门脚本语言，它算是Javascript的增强版，它扩展Javascript的类库，增加了面向对象特性。当然它最大的特点是兼容Javascript，它可以将自己的代码编译成Javascript代码
* Node核心模块：
1. 文件系统：fs、path
2. TCP：net、HTTP、HTTPS
3. 域名解析：DNS
4. 测试断言：assert
5. node的调试器：node debug server.js，我们可以在语句中添加debugger来设置断点调试
* 三种主流的Node程序：
1. web：Express Koa
2. 命令号工具和后台程序
3. 桌面程序：Atom就是用nodejs的Electron写的
* 项目技术栈
1. 服务端：Node.js >=7.9.0
2. 数据库：MongoDB >=3.4
3. WEB框架：Express 4.0
4. 模板引擎：ejs
5. JS和UI库：jquery,layui
6. Ajax库：axios
├─config(配置文件)
├─models(对象模型)
├─node_modules(依赖)
├─public(静态资源)
│  └─res
│      ├─layui(前端框架layui)
│      │  ├─css
│      │  ├─font
│      │  ├─images
│      └─static│          ├─css
│          ├─images
│          ├─js
│          └─lib
├─router(路由)
└─views(视图模板)
    ├─admin(后台管理)
    └─html(前端展示)
* Jade+Node.js+Express+mongoDB+Bower+Gulp+Yeoman的组合开发Web应用
* 安装脚手架及创建基于webpack项目：
cnpm install vue
cnpm install –global vue-cli
vue init webpack my-project
cd my-project
cnpm install
cnpm run dev
* 随着不同终端(Pad/Mobile/PC)的兴起，对开发人员的要求越来越高；为了提升开发效率，前后端分离的需求越来越被重视，后端负责业务/数据接口，前端负责展现/交互逻辑，同一份数据接口，我们可以定制开发多个版本；
* 基于NodeJS的前后端分离方案；所有用到的展现数据都是后端通过异步接口(AJAX/JSONP)的方式提供的，前端只管展现
* 接口通常是按照展现逻辑来提供的，有时候为了提高效率，后端会帮我们处理一些展现逻辑，这就意味着后端还是涉足了View层的工作，不是真正的前后端分离；前端：负责View和Controller层。后端：只负责Model层，业务处理/数据

# Web 研发模式演变
* 简单明快的早期时代( Web 1.0 时代，非常适合创业型小项目，不分前后端，经常 3-5 人搞定所有开发)，页面由 JSP、PHP 等工程师在服务端生成，浏览器负责展现。基本上是服务端给什么浏览器就展现什么，展现的控制在 Web Server 层
* 后端为主的 MVC 时代。MVC 是个非常好的协作模式，从架构层面让开发者懂得什么代码应该写在什么地方。为了让 View 层更简单干脆，还可以选择 Velocity、Freemaker 等模板，使得模板里写不了 Java 代码。前后端协作有两种模式：一种是前端写 demo，写好后，让后端去套模板。淘宝早期包括现在依旧有大量业务线是这种模式。不足是还需要后端套模板，有可能套错，套完后还需要前端确定，来回沟通调整的成本比较大。另一种协作模式是前端负责浏览器端的所有开发和服务器端的 View 层模板开发，支付宝是这种模式。好处是 UI 相关的代码都是前端去写就好，后端不用太关注，不足就是前端开发重度绑定后端环境，环境成为影响前端开发效率的重要因素。Controller，页面路由等功能本应该是前端最关注的，但却是由后端来实现。Controller 本身与 Model 往往也会纠缠不清，看了让人咬牙的代码经常会出现在 Controller 层
* Ajax 带来的 SPA 时代。2004 年 Gmail 像风一样的女子来到人间，很快 2005 年 Ajax 正式提出，加上 CDN 开始大量用于静态资源存储，于是出现了 JavaScript 王者归来的 SPA （Single Page Application 单页面应用）时代。前后端的关键协作点是 Ajax 接口。类似 Spring MVC，这个时代开始出现浏览器端的分层架构。client(view/model/controller),server(service,db)。API Blueprint 等方案来约定和沉淀接口。SPA 应用大多以功能交互型为主，JavaScript 代码过十万行很正常
* 前端为主的 MV* 时代。为了降低前端开发复杂度，除了 Backbone，还有大量框架涌现，比如 EmberJS、KnockoutJS、AngularJS 。前端工作在浏览器端，后端工作在服务端。清晰的分工，可以让开发并行，测试数据的模拟不难，前端可以本地开发。后端则可以专注于业务逻辑的处理，输出 RESTful 等接口。代码不能复用。比如后端依旧需要对数据做各种校验。全异步，对 SEO 不利。往往还需要服务端做同步渲染的降级方案。SPA 不能满足所有需求，依旧存在大量多页面应用。URL Design 需要后端配合，前端无法完全掌控
* Node 带来的全栈时代。随着 Node.js 的兴起，JavaScript 开始有能力运行在服务端
1. Front-end UI layer 处理浏览器层的展现逻辑。通过 CSS 渲染样式，通过 JavaScript 添加交互功能，HTML 的生成也可以放在这层
2. Back-end UI layer 处理路由、模板、数据获取、cookie 等。通过路由，前端终于可以自主把控 URL Design，这样无论是单页面应用还是多页面应用，前端都可以自由调控。后端也终于可以摆脱对展现的强关注，转而可以专心于业务逻辑层的开发
3. 通过 Node，Web Server 层也是 JavaScript 代码，这意味着部分代码可前后复用，需要 SEO 的场景可以在服务端同步渲染，由于异步请求太多导致的性能问题也可以通过服务端来缓解
* var Client = require('node-rest-client').Client
* 传统的SPA模式：所有用到的展现数据都是后端通过异步接口(AJAX/JSONP)的方式提供的，前端只管展现
npm install express-generator -g
express progressive
cd progressive
npm install
npm start
app.set('view engine', 'jade');
router.get('/', function(req, res, next) {
  // 假设这里我为了获取 title 的值，对 sql 进行了查询，然后把title的值插入到模板引擎中
  res.render('index', { title: 'Express' });
});
* Backbone, EmberJS, KnockoutJS, AngularJS, React, Vue
* 前端使用 vue-cli 生成脚手架，通过安装 axios 进行 ajax 数据请求便可以得到返回的数据。
* 一台 mock 服务器，最好能同步服务端接口的 mock。当然，现在网上也已经有了成熟的解决方案，比如 easy-mock 。他可以很好地支持Swagger，这是一个重磅级特性，通过 Swagger 只需1秒就能创建好项目所有的 Mock 接口
* 
后端	                                          前端
提供数据	                                      接收数据，返回数据
处理业务逻辑	                                   处理渲染逻辑
Server-side MVC架构	                             Client-side MV* 架构
代码跑在服务器上	                                代码跑在浏览器上
* 代码量越来越大，我们需要校验的表单也会越来越多;服务端任需要进行校验来达到数据的可靠性;;
![前后端分离](https://upload-images.jianshu.io/upload_images/3808719-f00519f507aadd8f.png "前后端分离")
* java：服务层、提供数据接口、维持数据稳定、封装业务逻辑
node.js：转发数据串接服务，路由设计，控制逻辑，渲染页面，体验优化
html+js+css：dom操作、公用模板、路由
* nodejs中间层作接口转发，作数据处理，而不用担心数据返回问题
* 页面性能优化 和 SEO，把首屏渲染任务交给nodejs做，次屏的渲染依然走浏览器；服务器端渲染对页面直接进行拼接html字符串
* 淘宝：先产生页面框架，然后发起多个异步请求
在NodeJS端使用 Bigpiper 技术，合并请求，降低负担，分批输出，不影响体验。同时可以拆分大接口为独立小接口，并发请求。串行 => 并行，大幅缩短请求时间
* yarn add vue-meta-info
npm install vue-meta-info --save
npm install cors --save
* 前端的工作：实现整一个前端页面以及交互逻辑，以及利用ajax与nodejs服务器（中间层)交互
后端的工作：提供API接口，利用redis来管理session,与数据库交互
* nodejs前端服务器的职责：
1. 作为静态文件服务器，当用户访问网站的时候，将index.html以及其引入的js、css、fonts以及图片返回给用户
2. 负责将客户端发来的ajax请求转发给后台服务器
3. 将开发完的前端代码，利用webpack打包成静态压缩文件
4. 在服务器上，利用pm2负载均衡器来执行以下的代码来开启服务器:
* Node应用中有一层Model Proxy与服务端进行通讯。这一层主要目前是抹平我们对不同接口的调用方式，封装一些view层需要的Model。
Node层还能轻松实现原来vmcommon,tms（引用淘宝内容管理系统）等需求
* Node层要使用什么框架由开发者自己决定。不过推荐使用express+xTemplate的组合，xTemplate能做到前后端公用
* 可以使用Node轻松实现我们想要的输出方式:JSON/JSONP/RESTful/HTML/BigPipe/Comet/Socket/同步、异步，想怎么整就怎么整，完全根据你的场景决定
* 以前服务端为什么能识别用户呢？对，是session，每个session都存在服务端，浏览器每次请求都带着sessionId（就是一个字符串），于是服务器根据这个sessionId就知道是哪个用户了；；那么问题来了，用户很多时，服务器压力很大，如果采用分布式存储session，又可能会出现不同步问题
* 在用户第一次登录成功后，服务端返回一个token回来，这个token是根据userId进行加密的，密钥只有服务器知道，然后浏览器每次请求都把这个token放在Header里请求，这样服务器只需进行简单的解密就知道是哪个用户了。这样服务器就能专心处理业务，用户多了就加机器
* token = Jwts.builder().setSubject(name).claim("roles", "user").setIssuedAt(new Date()).signWith(SignatureAlgorithm.HS256, "base64EncodedSecretKey").compact();
