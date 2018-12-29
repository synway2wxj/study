* <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>
* SpringBoot的配置方式有很多，它们的优先级如下所示：
1.命令行参数
2.来自java:comp/env的JNDI属性
3.Java系统属性（System.getProperties()）
4.操作系统环境变量
5.RandomValuePropertySource配置的random.*属性值
6.jar包外部的application-{profile}.properties或application.yml(带spring.profile)配置文件
7.jar包内部的application-{profile}.properties或application.yml(带spring.profile)配置文件
8.jar包外部的application.properties或application.yml(不带spring.profile)配置文件
9.jar包内部的application.properties或application.yml(不带spring.profile)配置文件
10.@Configuration注解类上的@PropertySource
11.通过SpringApplication.setDefaultProperties指定的默认属性
* @SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
* 修改banner（http://patorjk.com/software/taag网站生成字符）： 在src/main/resources下新建一个banner.txt
SpringApplication app = new SpringApplication(LilinlearnApplication.class);
app.setBannerMode(Banner.Mode.OFF);
app.run(args);
或者
new SpringApplicationBuilder(LilinlearnApplication.class)
.bannerMode(Banner.Mode.OFF)
.run(args);
* SpringBoot提倡零配置，即无XML配置，但实际上有些特殊的配置需要使用XML配置。我们可以通过Spring提供的@ImportResource来加载XML配置
@ImportResource({"classpath:some-context.xml","classpath:another-context.xml"})
* @PropertySource(value = "classpath:test.properties")
@ConfigurationProperties(prefix = "mail")
* 默认情况下，SpringBoot使用Logback作为日志框架
logging.file=D:/mylog/log.log
logging.level.org.springframework.web=DEBUG
* Profile是Spring针对不同环境不同配置的支持： 格式为：application-{profile}.properties
* 在application.properties中的各个参数之间也可以直接引用来使用
* 配置文件中${random} 可以用来生成各种不同类型的随机值:${random.value} ${random.int} ${random.long} ${random.uuid} ${random.int(10)}
${random.int[1024,2048]}
* oracle/mysql/derby/postgresql/sqlserver/h2;;通过druid提供的监控功能，可以实时观察数据库连接池和sql查询的工作情况
* 使用spring boot框架也能使用xml配置，只要在程序

# ApplicationListener<ContextRefreshedEvent>
# ApplicationEvent
# @FunctionalInterface
# static final
# CONFIGURABLE_WEB_ENVIRONMENT_CLASS
# static {
        Set<String> names = new HashSet();
        names.add("servletContextInitParams");
        names.add("servletConfigInitParams");
        names.add("jndiProperties");
        SERVLET_ENVIRONMENT_SOURCE_NAMES = Collections.unmodifiableSet(names);
    }
# Assert.notNull Assert.notEmpty
# throw new IllegalArgumentException("Invalid source type " + source.getClass());
# int var3 = sources.length;
# private static final Map<Class<?>, Class<?>> primitiveWrapperTypeMap = new IdentityHashMap(8);
# Thread.currentThread().getContextClassLoader();   ClassUtils.class.getClassLoader();   ClassLoader.getSystemClassLoader();
# Assert.notNull(name, "Name must not be null");
# clazz1.isAssignableFrom(clazz2)   class2是不是class1的子类或者子接口
# class SpringBootExceptionHandler implements UncaughtExceptionHandler
Thread.currentThread().setUncaughtExceptionHandler(currentHandler);
Thread.setDefaultUncaughtExceptionHandler(defaultHandler);
UncaughtExceptionHandler defaultHandler = new UncaughtExceptionHandler() {
			@Override
			public void uncaughtException(Thread t, Throwable e) {
				System.out.println("【默认的Handler处理异常信息】" + 'xxx');
			}
		};
if (this.exitCode != 0) {
                System.exit(this.exitCode);
            }
# Environment environment    PrintStream printStream
# static final String[] IMAGE_EXTENSION = new String[]{"gif", "jpg", "png
# environment.getProperty("spring.banner.location", "banner.txt");
# private static final Log logger = LogFactory.getLog(SpringApplication.class);
# public abstract class AnsiOutput
# private static Boolean ansiCapable;
# new ConcurrentReferenceHashMap(256)
# Collections.indexedBinarySearch(list, key);
# Collections.iteratorBinarySearch(list, key)
# <<      :     左移运算符，num << 1,相当于num乘以2
>>      :     右移运算符，num >> 1,相当于num除以2
>>>    :     无符号右移，忽略符号位，空位都以0补齐
# nextCand:
# WebServiceTemplateBuilder
# private static final class
# ReflectionUtils.findMethod
# private final MultiValueMap<Class<?>, ServletContextInitializer> initializers = new LinkedMultiValueMap();
#  @AliasFor("basePackages")
String[] value() default {};
@AliasFor("value")
String[] basePackages() default {};
# static {}
# public class DelegatingFilterProxyRegistrationBean extends AbstractFilterRegistrationBean<DelegatingFilterProxy> implements ApplicationContextAware
# String[] urlMapping = StringUtils.toStringArray(this.urlMappings)
# EnumSet<EnumTest> enumSet = EnumSet.noneOf(EnumTest.class);
# StringUtils.hasText
# @Bean  @Configuration @Order(-2147483647)
# OncePerRequestFilter
# 在servlet2.3中，Filter会经过一切请求，包括服务器内部使用的forward转发请求和<%@ include file=”/login.jsp”%>的情况;servlet2.4中的Filter默认情况下只过滤外部提交的请求，forward和include这些内部转发都不会被过滤，因此，为了兼容各种不同运行环境和版本，默认filter继承OncePerRequestFilter是一个比较稳妥的选择
# WebAsyncUtils.getAsyncManager(request)
# !contextPath.startsWith("/") || contextPath.endsWith("/")
# URLConnection connection = location.openConnection();   if (connection instanceof JarURLConnection)
# @Order标记从spring 2.0出现，但是在spring 4.0之前，@Order标记只支持AspectJ的切面排序。spring 4.0对@Order做了增强，它开始支持对装载在诸如Lists和Arrays容器中的自动包装（auto-wired）组件的排序;;1,2 等等。值越小拥有越高的优先级;;Spring提供了OrderUtils来获取Class的Order注解排序信息
# public interface WebServerFactoryCustomizer<T extends WebServerFactory> 
# MimeMappings.DEFAULT
# int result = 31 * result + ObjectUtils.nullSafeHashCode(this.getExceptionName());
