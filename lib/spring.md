### spring
* @Configuration  @Bean(name="myBean") @Scope("prototype")  @ComponentScan("com.cn.spring")
AnnotationConfigApplicationContext context =new AnnotationConfigApplicationContext(MyConfig.class);
AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext("com.cn.spring");
* public class RunnableFactroy implements FactoryBean<Dog>  使用FactoryBean来装配bean，FactoryBean 是个特殊的Bean，专门是获取其他的Bean
* @InitBinder
　　public void initBinder(WebDataBinder binder) {

　　SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");
　　dateFormat.setLenient(false);
　　binder.registerCustomEditor(Date.class, new CustomDateEditor(dateFormat, false));

}
希望某个属性编辑器仅作用于特定的 Controller ，
可以在 Controller 中定义一个标注 @InitBinder 注解的方法
* 添加了一个AsyncRestTemplate ，支持REST客户端的异步无阻塞支持
* AsyncRestTemplate template = new AsyncRestTemplate();  
    //调用完后立即返回（没有阻塞）  
    ListenableFuture<ResponseEntity<User>> future = template.getForEntity("http://localhost:9080/spring4/api", User.class); 
    //设置异步回调  
    future.addCallback(new ListenableFutureCallback<ResponseEntity<User>>() {  
        @Override  
        public void onSuccess(ResponseEntity<User> result) {  
            System.out.println("======client get result : " + result.getBody());  
        }  
  
        @Override  
        public void onFailure(Throwable t) {  
            System.out.println("======client failure : " + t);  
        }  
    });  
* AsyncRestTemplate默认使用SimpleClientHttpRequestFactory，即通过java.net.HttpURLConnection实现；另外我们也可以使用apache的http components；使用template.setAsyncRequestFactory(new HttpComponentsAsyncClientHttpRequestFactory());设置即可
* <mirror>
           <id>alimaven</id>
           <mirrorOf>central</mirrorOf>
           <name>aliyun maven</name>
           <url>http://maven.aliyun.com/nexus/content/repositories/central/</url>
         </mirror>
* DO领域对象，即业务实体
* 用户发出请求（可能是填写表单），表单的数据在展示层被匹配为VO。
展示层把VO转换为服务层对应方法所要求的DTO，传送给服务层。
服务层首先根据DTO的数据构造（或重建）一个DO，调用DO的业务方法完成具体业务。
服务层把DO转换为持久层对应的PO
* Spring不仅仅对服务 端开发有用，任何Java应用都可受益于Spring的简洁、易测试和低耦合等特性
* 基于CGLIB的类代理不再要求类必须有空参构造器了
* Bean Validate新特性
支持跨参数验证（比如密码和确认密码的验证）和支持在消息中使用EL表达式，其他的还有如方法参数/返回值验证、CDI和依赖注入、分组转换等
* test部分提供了更便利的@sql标签来执行测试脚本的初始化、MockRestServiceServer对AyncRestTemplate支持、MockMvcConfigurer来全局配置MockMvc
* 配置类上的@Import以前只能引入配置类(注解了@Configuration等的类), 现在可以引入一般的组件了, 比如啥注解都没有的类
* @Lazy @Resource ScopedBean bean;
* @TransactionalEventListener
*  //当事务提交后, 才会真正的执行@TransactionalEventListener配置的Listener, 如果Listener抛异常, 方法返回失败, 但事务不会回滚
* @AliasFor(annotation = Component.class, attribute = "value")
    String beanName() default "";
* 鉴于WebSocket仅仅提供了一种低层次的API，急需高层次的抽象，因此Spring4.0在网页套接字之上提供了一个高层次的面向消息的编程模型，
该模型基于SockJS，并且包含了对STOMP协议的支持
