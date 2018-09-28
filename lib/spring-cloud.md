* 服务发现（Eureka），断路器（Hystrix），智能路由（Zuul）和客户端负载均衡（Ribbon）;Eureka是Netflix服务发现的一种服务和客户端
* http://user:password@localhost:8761/eureka;对于更复杂的需求，可以创建一个带“@Bean”注解的“DiscoveryClientOptionalArgs”类型并且为它注入“ClientFilter”实例
* eureka.instance.[nonSecurePortEnabled,securePortEnabled]=[false,true]
* 不要在@PostConstruct方法或@Scheduled方法使用EurekaClient
* Spring Cloud已经支持Feign（一个REST客户端构建）跟Spring RestTemplate（使用逻辑Eureka服务标识符(VIPs)代替物理的URL）
* new SpringApplicationBuilder(Application.class).web(true).run(args);
* Eureka服务端没有后台存储，但是服务实例在注册里面全都得发送心跳去保持注册更新（在内存里操作）客户端们也有一份内存缓存着eureka的注册信息
* Netflix创建了一个库实现断路器模式，名为Hystrix  当调用一个特定的服务达到一定阈值(在Hystrix里默认是5秒内20个失败)，断路器开启并且调用没有成功的。开发人员能够提供错误原因和开启一个断路由回调
* @HystrixCommand(fallbackMethod = "defaultStores")  @HystrixCommand(fallbackMethod = "stubMyService",
    commandProperties = {
      @HystrixProperty(name="execution.isolation.strategy", value="SEMAPHORE")
    }
)
* Hystrix 指标流:org.springframework.boot.spring-boot-starter-actuator
* Ribbon是一个客户端负载均衡器，有很多控制HTTP和TCP客户端的行为，可使用@FeignClient注解
* REST客户端：Feign   Zuul是Netflix出品的一个基于JVM路由和服务端的负载均衡器   @EnableZuulProxy
* 使用@EnableZuulProxy同时引入了Spring Boot Actuator，默认将增加一个endpoint，提供http服务的/routes
