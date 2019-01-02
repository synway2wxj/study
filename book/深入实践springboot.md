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
* servletregistrationbean  filterregistrationbean
* jpa使用predicateBuilder构造一个查询参数
* enablecacheing
* rediscachemanager manager = new rediscachemanager(redistemplate);
manager.setdefaultexpiration(43200);
* 大量查询语句从原来的数据库服务器，转移到了高效的redis服务器中执行
* server.port:80
* server.tomcat.uri-encoding:UTF-8
* public final class VERSION {
    public static final int MajorVersion = 1;
    public static final int MinorVersion = 1;
    public static final int RevisionVersion = 7;
* public class TransactionTimeoutException extends SQLException
* public interface Constants {
* AtomicLongFieldUpdater
* private volatile long executeCount;
* volatile修饰的变量不允许线程内部缓存和重排序，即直接修改内存。所以对其他线程是可见的。但是这里需要注意一个问题，volatile只能让被他修饰内容具有可见性，但不能保证它具有原子性。比如 volatile int a = 0；之后有一个操作 a++；这个变量a具有可见性，但是a++ 依然是一个非原子操作，也就是这个操作同样存在线程安全问题
* 计算机在执行程序时，每条指令都是在CPU中执行的，而执行指令过程中，势必涉及到数据的读取和写入
* 由于程序运行过程中的临时数据是存放在主存（物理内存）当中的，这时就存在一个问题，由于CPU执行速度很快，而从内存读取数据和向内存写入数据的过程跟CPU执行指令的速度比起来要慢的多，因此如果任何时候对数据的操作都要通过和内存的交互来进行，会大大降低指令执行的速度。因此在CPU里面就有了高速缓存
* 如果一个变量在多个CPU中都存在缓存（一般在多线程编程时才会出现），那么就可能存在缓存不一致的问题
* 当CPU写数据时，如果发现操作的变量是共享变量，即在其他CPU中也存在该变量的副本，会发出信号通知其他CPU将该变量的缓存行置为无效状态，因此当其他CPU需要读取这个变量时，发现自己缓存中缓存该变量的缓存行是无效的，那么它就会从内存重新读取
* 也就是说，要想并发程序正确地执行，必须要保证原子性、可见性以及有序性。只要有一个没有被保证，就有可能会导致程序运行不正确
* 对于可见性，Java提供了volatile关键字来保证可见性。当一个共享变量被volatile修饰时，它会保证修改的值会立即被更新到主存，当有其他线程需要读取时，它会去内存中读取新值
* 在Java内存模型中，允许编译器和处理器对指令进行重排序，但是重排序过程不会影响到单线程程序的执行，却会影响到多线程并发执行的正确性
* 一旦一个共享变量（类的成员变量、类的静态成员变量）被volatile修饰之后，那么就具备了两层语义：
1）保证了不同线程对这个变量进行操作时的可见性，即一个线程修改了某个变量的值，这新值对其他线程来说是立即可见的。
2）禁止进行指令重排序
* volatile到底如何保证可见性和禁止指令重排序的
* 把代码块声明为 synchronized，有两个重要后果，通常是指该代码具有 原子性（atomicity）和 可见性
* 多个变量之间或者某个变量的当前值与修改后值之间没有约束。因此，单独使用 volatile 还不足以实现计数器、互斥锁或任何具有与多个变量相关的不变式
* volatile最适用一个线程写，多个线程读的场合；；如果有多个线程并发写操作，仍然需要使用锁或者线程安全的容器或者原子变量来代替；；volatile 允许多个线程执行读操作，因此当使用 volatile 保证读代码路径时，要比使用锁执行全部代码路径获得更高的共享度
* throw new IllegalArgumentException("logger can not be null")
* private final ReentrantReadWriteLock lock = new ReentrantReadWriteLock()
* private static final ThreadLocal<Boolean> privileged = new ThreadLocal()
* 虽然ThreadLocal能够解决上面说的问题，但是由于在每个线程中都创建了副本，所以要考虑它对资源的消耗，比如内存的占用会比不使用ThreadLocal要大
* 每个线程需要有自己单独的实例
实例需要在多个方法中共享，但不希望被多线程共享
* protected final AtomicLong checkCount = new AtomicLong();
* public interface ErrorCode {
    int SYNTAX_ERROR = 1001;
    int SELECT_NOT_ALLOW = 1002;
* ClassLoader ctxClassLoader = Thread.currentThread().getContextClassLoader();
* URL url = new URL(serverUrl);
            URLConnection conn = url.openConnection();
            conn.setDoOutput(true);
            conn.setConnectTimeout(5000);
* String ip = request.getHeader("x-forwarded-for");
if (ip == null || ip.length() == 0 || "unknown".equalsIgnoreCase(ip)) {
    ip = request.getHeader("Proxy-Client-IP");
}
if (ip == null || ip.length() == 0 || "unknown".equalsIgnoreCase(ip)) {
    ip = request.getHeader("WL-Proxy-Client-IP");
}
if (ip == null || ip.length() == 0 || "unknown".equalsIgnoreCase(ip)) {
    ip = request.getRemoteAddr();
}
* Thread newThread = new Thread(r, threadName);
        newThread.setDaemon(true);
* public <T> T unwrap(Class<T> iface) throws SQLException
* clob.getSubString(1L, (int)clob.length())
* public class DruidStatNamespaceHandler extends NamespaceHandlerSupport
*     @Resource(
        name = "druid-stat-interceptor"
    )
* static final AtomicLongFieldUpdater<SpringMethodStat> histogram_0_1_Updater
* public class BeanTypeAutoProxyCreator extends AbstractAutoProxyCreator implements InitializingBean, ApplicationContextAware
* private Map<ProfileEntryKey, ProfileEntryStat> entries = new LinkedHashMap(4)
* private static final Lock staticLock = new ReentrantLock();



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
