* http://dubbo.apache.org/zh-cn/docs/user/quick-start.html
* http://dubbo.apache.org/zh-cn/docs/user/references/registry/redis.html
* Spring 的 Schema 扩展
* 接口需单独打包，在服务提供方和消费方共享
* 单一应用架构/垂直应用架构/分布式服务架构/流动计算架构
* 在大规模服务化之前，应用可能只是通过 RMI 或 Hessian 等工具，简单的暴露和引用远程服务，通过配置服务的URL地址进行调用，通过 F5 等硬件进行负载均衡
* 服务间依赖关系变得错踪复杂，甚至分不清哪个应用要在哪个应用之前启动，架构师都不能完整的描述应用的架构关系
* 服务的调用量越来越大，服务的容量问题就暴露出来，这个服务需要多少机器支撑？什么时候该加机器;要将服务现在每天的调用量，响应时间，都统计出来;要可以动态调整权重，在线上，将某台机器的权重一直加大，并在加大的过程中记录响应时间的变化，直到响应时间到达阈值，记录此时的访问量，再以此访问量乘以机器数反推总容量
* mvn dependency:tree > dep.log
* javassist.jar [2]: 如果 <dubbo:provider proxy="jdk" /> 或 <dubbo:consumer proxy="jdk" />，以及 <dubbo:application compiler="jdk" />，则不需要。
spring-context.jar [3]: 如果用 ServiceConfig 和 ReferenceConfig 的 API 调用，则不需要。
netty.jar [4]: 如果 <dubbo:protocol server="mina"/> 或 <dubbo:protocol server="grizzly"/>，则换成 mina.jar 或 grizzly.jar。如果 <protocol name="rmi"/>，则不需要
* Zookeeper注册中心 / Redis注册中心
* Dubbo协议:在大文件传输时，单一连接会成为瓶颈=====Rmi协议:偶尔会连接失败，需重建Stub=====Hessian协议:需hessian.jar支持，http短连接的开销大=====
* <dubbo:protocol/>	协议配置	用于配置提供服务的协议信息，协议由提供方指定，消费方被动接受
* Dubbo 将自动加载 classpath 根目录下的 dubbo.properties，可以通过JVM启动参数 -Ddubbo.properties.file=xxx.properties 改变缺省配置位置
* dubbo.application.name=foo等价于<dubbo:application name="foo" />
* dubbo.application.name=foo
dubbo.application.owner=bar
dubbo.registry.address=10.20.153.10:9090
* // 服务实现
XxxService xxxService = new XxxServiceImpl();
 
// 当前应用配置
ApplicationConfig application = new ApplicationConfig();
application.setName("xxx");
 
// 连接注册中心配置
RegistryConfig registry = new RegistryConfig();
registry.setAddress("10.20.130.230:9090");
registry.setUsername("aaa");
registry.setPassword("bbb");
 
// 服务提供者协议配置
ProtocolConfig protocol = new ProtocolConfig();
protocol.setName("dubbo");
protocol.setPort(12345);
protocol.setThreads(200);
 
// 注意：ServiceConfig为重对象，内部封装了与注册中心的连接，以及开启服务端口
 
// 服务提供者暴露服务配置
ServiceConfig<XxxService> service = new ServiceConfig<XxxService>(); // 此实例很重，封装了与注册中心的连接，请自行缓存，否则可能造成内存和连接泄漏
service.setApplication(application);
service.setRegistry(registry); // 多个注册中心可以用setRegistries()
service.setProtocol(protocol); // 多个协议可以用setProtocols()
service.setInterface(XxxService.class);
service.setRef(xxxService);
service.setVersion("1.0.0");
 
// 暴露及注册服务
service.export();


* // 当前应用配置
ApplicationConfig application = new ApplicationConfig();
application.setName("yyy");
 
// 连接注册中心配置
RegistryConfig registry = new RegistryConfig();
registry.setAddress("10.20.130.230:9090");
registry.setUsername("aaa");
registry.setPassword("bbb");
 
// 注意：ReferenceConfig为重对象，内部封装了与注册中心的连接，以及与服务提供方的连接
 
// 引用远程服务
ReferenceConfig<XxxService> reference = new ReferenceConfig<XxxService>(); // 此实例很重，封装了与注册中心的连接以及与提供者的连接，请自行缓存，否则可能造成内存和连接泄漏
reference.setApplication(application);
reference.setRegistry(registry); // 多个注册中心可以用setRegistries()
reference.setInterface(XxxService.class);
reference.setVersion("1.0.0");
 
// 和本地bean一样使用xxxService
XxxService xxxService = reference.get();

* 需要 2.5.7 及以上版本支持
* Service注解暴露服务,@Service(timeout = 5000)
* @Configuration
public class DubboConfiguration {

    @Bean
    public ApplicationConfig applicationConfig() {
        ApplicationConfig applicationConfig = new ApplicationConfig();
        applicationConfig.setName("provider-test");
        return applicationConfig;
    }

    @Bean
    public RegistryConfig registryConfig() {
        RegistryConfig registryConfig = new RegistryConfig();
        registryConfig.setAddress("zookeeper://127.0.0.1:2181");
        registryConfig.setClient("curator");
        return registryConfig;
    }
}
* 指定dubbo扫描路径,@SpringBootApplication @DubboComponentScan(basePackages = "com.alibaba.dubbo.test.service.impl")
* Reference注解引用服务:@com.alibaba.dubbo.config.annotation.Reference  public AnnotateService annotateService;
* @Configuration
public class DubboConfiguration {

    @Bean
    public ApplicationConfig applicationConfig() {
        ApplicationConfig applicationConfig = new ApplicationConfig();
        applicationConfig.setName("consumer-test");
        return applicationConfig;
    }

    @Bean
    public ConsumerConfig consumerConfig() {
        ConsumerConfig consumerConfig = new ConsumerConfig();
        consumerConfig.setTimeout(3000);
        return consumerConfig;
    }

    @Bean
    public RegistryConfig registryConfig() {
        RegistryConfig registryConfig = new RegistryConfig();
        registryConfig.setAddress("zookeeper://127.0.0.1:2181");
        registryConfig.setClient("curator");
        return registryConfig;
    }
}
* <dubbo:reference interface="com.foo.BarService" check="false" />
* <dubbo:consumer check="false" />
* <dubbo:registry check="false" />
* dubbo.reference.com.foo.BarService.check=false
dubbo.reference.check=false
dubbo.consumer.check=false
dubbo.registry.check=false
