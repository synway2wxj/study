* https://springcloud.cc/
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
* 服务注册与发现，配置，消息总线，服务网关，负载均衡，服务熔断，数据治理与监控
* 服务发现 - Netflix Eureka 
负载均衡 - Netfilx Ribbon
服务熔断 - Netfix Hystrix
服务网关  - Netflix Zuul
分布式配置 - Spring Cloud Config
* Netflix是美国流媒体提供商
* 需要对分布式服务进行主动内部保护，而常用的缓解或解决方案主要有熔断，隔离，限流及降级
* 熔断：参考电路保险丝断路／熔断，如电压过高，保险丝会熔断而避免发生火灾。分布式系统中的熔断，则某个服务调用异常慢或者大量超时，系统主动熔断，避免后续继续恶性循环等待，直接返回，快速释放资源，若目标服务之正常后则恢复服务可用性。注 ： 不忘吐槽一下我大a股的熔断，呵呵。隔离：隔离也很好理解，如病人隔离避免进一步传染；系统中如线程池隔离，信号量隔离限流：不同上述出错后的补救机制，限流则是事先预防模式，对于服务请求提前预设最高的QPS阀值，如有些框架用锁来实现降级（fallback）：服务降级则是针对整个分布式系统，当出现整体资源紧缺的情况下，主动关闭一些次级服务，以提升主服务响应，待整体性能恢复后再重新开启次级服务
* Spring Boot是由Pivotal团队提供的全新框架
* <!-- 引入jdbc 依赖 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <!-- 引入 mysql 数据库连接依赖-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
* @Repository
public class UserDao {

    @Autowired
    JdbcTemplate jdbcTemplate;

    public void save(User user) {
        String sql = "insert into t_user(user_name, password) values(?,?)";
        jdbcTemplate.update(sql, user.getUserName(), user.getPassword());
    }
}
*   <!-- 引入jpa 依赖 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
* #配置jpa
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jackson.serialization.indent_output=true
* @Entity
@Table(name="t_user")
public class User {
* public interface UserRepository extends CrudRepository<User, Integer>
* public class LinuxCondition implements Condition{

    @Override
    public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
        // return context.getEnvironment().getProperty("os.name").contains("Windows");
        return context.getEnvironment().getProperty("os.name").contains("Linux");
    }

    
}
*  @Bean
    @Conditional(WindowsCondition.class)
* @EnableConfigurationProperties(HelloServiceProperties.class)
@ConditionalOnClass(HelloService.class)
@ConditionalOnProperty(prefix = "hello", matchIfMissing = true, value = "enabled")
* @SpringBootApplication
@EnableZuulProxy
@EnableEurekaClient
@EnableDiscoveryClient
@EnableHystrix
@HystrixCommand(fallbackMethod = "hiError")
* @Component
public class MyFilter extends ZuulFilter
Object accessToken = request.getParameter("token");

RequestContext ctx = RequestContext.getCurrentContext();
        HttpServletRequest request = ctx.getRequest();
        log.info(String.format("%s >>> %s", request.getMethod(), request.getRequestURL().toString()));
        Object accessToken = request.getParameter("token");
        if(accessToken == null) {
            log.warn("token is empty");
            ctx.setSendZuulResponse(false);
            ctx.setResponseStatusCode(401);
            try {
                ctx.getResponse().getWriter().write("token is empty");
            }catch (Exception e){}

            return null;
        }
        log.info("ok");
* 服务并不能保证100%可用，如果单个服务出现问题，调用这个服务就会出现线程阻塞，此时若有大量的请求涌入，Servlet容器的线程资源会被消耗完毕，导致服务瘫痪。服务与服务之间的依赖性，故障会传播，会对整个微服务系统造成灾难性的严重后果，这就是服务故障的“雪崩”效应
* 在微服务架构中，一个请求需要调用多个服务是非常常见的
* 较底层的服务如果出现故障，会导致连锁故障。当对特定的服务的调用的不可用达到一个阀值（Hystric 是5秒20次） 断路器将会被打开。
* Feign是自带断路器的，在D版本的Spring Cloud之后，它没有默认打开  feign.hystrix.enabled=true
@FeignClient(value = "service-hi",fallback = SchedualServiceHiHystric.class)
* <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
* 公司架构和项目也全面拥抱了Spring Cloud
* Spring Cloud也不是没有缺点，小型独立的项目不适合使用
* Spring Cloud Config、Spring Cloud Netflix（Eureka、Hystrix、Zuul、Archaius...）、Spring Cloud Bus、Spring Cloud for Cloud Foundry、Spring Cloud Cluster、Spring Cloud Consul、Spring Cloud Security、Spring Cloud Sleuth、Spring Cloud Data Flow、Spring Cloud Stream、Spring Cloud Task、Spring Cloud Zookeeper、Spring Cloud Connectors、Spring Cloud Starters、Spring Cloud CLI
