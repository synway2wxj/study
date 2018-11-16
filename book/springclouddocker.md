当当的dubbo扩张框架dubbox
很多sc研发资料
github上找了很多代码仔细研读
http://oschina.net/darkranger/spring-cloud-books
努力勤奋、独立思考、认真做事
CI、DI自动化流程和容器化部署
语法糖提高生产效率
感受它的优雅
项目越来越臃肿 docker Jenkins
用特定技术栈
归档包、war包 包含所有功能的应用程序 单体应用 模块化 整个系统的所有业务功能
每个服务运行在自己的系统中，服务间采用轻量级通信机制；服务围绕业务能力构建全自动部署；服务可用不同语言开发，使用不同的数据存储技术
每个服务为独立的业务开发，一个服务只关注某个特定的功能
rest或者其它通信协议
有图形计算需求，可以用neo4j，部分服务用java开发，部分服务用node.js开发
很多服务可能会使用的同样功能
将某个功能封装成组件
数据库设计
每个服务从开发、测试、构建、部署，都应当独立运行，不应该依赖其它服务
常用协议：rest、amqp、stomp、mqtt
使用合理的粒度划分微服务  领域驱动设计
自动化部署工具以及lass(基础设施即服务)、pass(平台即服务)、caas(容器即服务)的支持
服务器、交换机、路由器、存储阵列和其它网络组件 虚拟化就是将物理服务器分成更小的虚拟机，这些虚拟机只能访问物理机的部分资源
虚拟化技术如Xen, KVM, VMware和Hyper-V
微服务框架：dubbo dropwizard armada
微服务部署在pc、阿里云、aws等云计算平台都是可以的
敏捷开发（Developer workflow） 批量运算（Batch computing） PaaS，也就是平台即服务。相比于虚拟机，容器显然更适合PaaS
spring cloud程序非常适合在docker、paas上部署；所以又叫云原生应用
spring cloud支持使用eureka、zookeeper或consul
spring cloud也支持scala、groovy
maven 、 gradle   gradle init --type pom
spring data jpa作为持久层框架，使用H2作为数据库
创建项目：网页、sts、idea、spring boot cli
spring boot actuator提供了很多监控端点，可使用ip:port/endpoint
eureka.instance.prefer-ip-address=true标识将自己的ip注册到注册中心
微服务在消费远程api时总是使用本地缓存中的数据
使用---将application.yml文件分为三段
将微服务注册到需认证的eureka server上
http://user:password@EUREKA_HOST_HOST:EUREKA_PORT/euraka/
eureka.instance.metadata-map，这些元素局可以在远程客户端中访问
private discoveryClient discoveryClient
http//ip:port/eureka/apps
注销微服务：curl -v -X DELETE http://ip:port/eureka/apps/rest-api-test/itmuch:rest-api-test:9000
eureka.server.enable-self-preservation = false禁用自我保护模式
spring.cloud.inetutils.ignored-interfaces=docker0,veth.*
eureka.instance.prefer-ip-address=true
eureka.instance.ip-address:127.0.0.1
spring.cloud.inetutils.preferredNetworks = 192.168,10.0

eureka.client.healthcheck.enabled = true

private LoadBalancerClient loadBalancerClient;
当Ribbon和eurka而配合使用会将虚拟主机名映射成微服务的网络地址  虚拟主机名不能包含_
feign是netflix开发的声明式、模块化的http客户端
spring.cloud.inetutils.useOnlySiteLocalInterfaces = true
如果不想使用eureka，可使用service.ribbon.listOfServers属性配置服务器列表，还可使用url属性置顶请求的url
@feignclient(name="xxx",url="xxx")
还可以自定义feign的编码器/解码器、日志打印、设值为其添加拦截器，一些借口需要进行基于http basic的认证后才能调用
new basicauthrequestInterceptor(user,password)
feignconfiguration不能包含在主应用程序上下文的@componentscan中
feign builder api手动创建feign
@enablewebsecurity
@enableglobalmethodsecurity(prepostenabled=true)
Feign支持继承，使用继承，可将一些公共操作分组到一些父接口中，从而简化Feign的开发
通常情况下，不建议在服务器端与客户端质检共享接口
feign.compression.request.enabled=true
feign.compression.response.enabled=true
为每个feign客户端配置各自的logger.level对象，告诉feign记录那些日志none basic headers full
Logger.Level feignLoggerLevel(){
return Logger.Level.FULL;}
logging:level:com.xxx.xxx.UserFeignClient:DEBUG

eureka实现微服务的注册、发现，Ribbon实现客户端的负载均衡，Feign实现声明式API调用
为网络请求设值超时
如果对某个微服务的请求有大量超时，再去让新的请求访问该服务已经没有任何意义，只会无谓消耗资源
Hystrix是一个实现了超时机制和断路器模式的工具类库
Hystrix配置属性
http://ip:port/hystrix.stream
-hystrix-dashboard
@EnableHystrixDashboard
http://ip:port/hystrix
turbine聚合监控数据  /turbine.stream
某些微服务可能使用了防火墙/浏览器不友好的协议，直接访问会有问题
微服务网关封装了应用程序的内部结构，客户端只须跟网关交互
可在网关手机监控数据并将其推送到外部系统进行分析，易于认证 核心是一系列过滤器
身份认证、监控、动态路由、压力测试、负载分配、静态响应处理、多区域弹性
apache http client  restclient  okhttpclient
ribbon.restclient.enabled=true   ribbon.okhttp.enabled=true(zuul默认使用的http客户端是apache http client)
所有经过zuul的请求都会在Hystrix命令中执行
spring-cloud-starter-zuul一级包含了spring-boot-starter-actuator
http://localhost:8040/routes可以查看路由
zuul:routes: serviceId = /user/**
zuul:ignored-services:id1,id2
zuul:ignored-services:'*
zuul:routes:xxx:/user/**
zuul:routes:user-route:url:xxx path:xxx
路由前缀：zuul:prefix:/api
zuul:ignoredPatterns:/**/admin/**忽略敏感路径
longging:level:com.netflix:DEBUG
zuul.sensitive-headers：Cookie,Set-Cookie,Authorization 全局置顶敏感Header
zuul:ignored-headers:xxx,xxx 忽略Header
zuul.ignoreSecurity-Headers:false
小文件直接上传，大文件，需要为上来路径添加/zuul前缀，也可以使用zuul.servlet-path前定义前缀
如果使用zuul使用了Ribbon负载均衡，name对于超大的文件，需要提升超时设值
curl -F "file=@文件全名" localhost:8050/upload
小文件：curl -v -H "Transfer-Encoding: chunked" -F "file=@small.file" localhost:80/xxx/upload
上传大文件将超时时间设值长一些：
hystrix.command.default.execution.isolation.thread.timeoutInMilliseconds:60000
ribbon.ConnectTimeout:3000
        ReadTimeout:60000
pre:身份验证，记录调试信息、集群中选择请求的微服务
routing：构建发送给微服务的请求
post：为响应添加标准的http header、手机统计信息和指标
error
编写zuul的过滤器非常简单
zuul.SendResponseFilter.post.disable=true
zuul回退：实现zuulfallbackprovider，为那个微服务提供回退，并提供一个clienthttpresponse响应
使用sidecar整合非jvm微服务  @EnableSidecar
sidecar:port:8060
sidecar:health-uri:http://xxx/health.json(监控检查url)
eureka:instance:hostname:xxx
sidecar:hostname:xxx
ip-address:xxx
使用rxjava结合zuul来实现微服务请求的聚合
zipkin-autoconfigure-ui
