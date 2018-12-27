* https://www.zcool.com.cn/ 站酷

### mybatis
* /**
 * 避免MyBatiis重复生成的工具类
 *
 * @author:wmyskxz
 * @create:2018-06-14-上午 9:50
 */
public class OverIsMergeablePlugin extends PluginAdapter {
    @Override
    public boolean validate(List<String> warnings) {
        return true;
    }

    @Override
    public boolean sqlMapGenerated(GeneratedXmlFile sqlMap, IntrospectedTable introspectedTable) {
        try {
            Field field = sqlMap.getClass().getDeclaredField("isMergeable");
            field.setAccessible(true);
            field.setBoolean(sqlMap, false);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return true;
    }
}
<plugin type="cn.wmyskxz.blog.util.OverIsMergeablePlugin"/>
### 启动方式
* 运行Spring Boot的3种方式:运行启动类的main方法 使用spring-boot:run命令  打成jar包后使用java -jar xx.jar命令
### 热部署
* <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
热部署开关，false即不启用热部署
spring.devtools.restart.enabled: true
指定热部署的目录
spring.devtools.restart.additional-paths: src/main/java
指定目录不更新
spring.devtools.restart.exclude: test/*
1. idea，需要改以下两个地方:File > Settings > Compiler-Build Project automatically
ctrl + shift + alt + / > Registry > 勾选Compiler autoMake allow when app running
2. 生产环境devtools将被禁用，如java -jar方式或者自定义的类加载器等都会识别为生产环境
打包应用默认不会包含devtools，除非你禁用SpringBoot Maven插件的excludeDevtools属性
Thymeleaf无需配置spring.thymeleaf.cache: false，devtools默认会自动设置
### 国际化
* basename：默认的扫描的国际化文件名为messages，即在resources建立messages_xx.properties文件，可以通过逗号指定多个，如果不指定包名默认从classpath下寻找
* cacheSeconds：加载国际化文件的缓存时间，单位为秒，默认为永久缓存
* fallbackToSystemLocale：当找不到当前语言的资源文件时，如果为true默认找当前系统的语言对应的资源文件如messages_zh_CN.properties，如果为false即加载系统默认的如messages.properties文件
* spring:
    messages:
        fallbackToSystemLocale: false
        basename: i18n/common, i18n/login, i18n/index
* 添加语言解析器，并设置默认语言为US英文;LocaleResolver接口有许多实现，如可以从session、cookie、Accept-Language header、或者一个固定的值来判断当前的语言环境，下面是使用session来判断：@Bean
public LocaleResolver localeResolver() {
    SessionLocaleResolver sessionLocaleResolver = new SessionLocaleResolver();
    sessionLocaleResolver.setDefaultLocale(Locale.US);
    return sessionLocaleResolver;
}
* 添加切换语言过滤器：private LocaleChangeInterceptor localeChangeInterceptor() {
    LocaleChangeInterceptor localeChangeInterceptor = new LocaleChangeInterceptor();
    localeChangeInterceptor.setParamName("lang");
    return localeChangeInterceptor;
}
@Override
public void addInterceptors(InterceptorRegistry registry) {
    registry.addInterceptor(localeChangeInterceptor());
}
然后页面通过访问指定的url?lang=zh_CN进行切换
### mock
@RunWith(SpringRunner.class)
@SpringBootTest
@AutoConfigureMockMvc
public class LoginTest {
    @Autowired
    private MockMvc mockMvc;

    @Test
    public void loginTest() throws Exception {
        mockMvc.perform(MockMvcRequestBuilders.get("/login").accept(MediaType.APPLICATION_JSON))
                .andExpect(status().isOk())
                .andExpect(content().string(equalTo("success")));
    }
}
### 常见问题
1. spring boot默认会加载org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration类，在Application类上增加@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})       或者    配置dataSource
2. Application启动类放的位置不对，要将Application放在最外层，也就是要包含所有子包。springboot会自动加载启动类所在包下及其子包下的所有组件
@SpringBootApplication(exclude = { 
DataSourceAutoConfiguration.class, 
DataSourceTransactionManagerAutoConfiguration.class, HibernateJpaAutoConfiguration.class})
3. 方式一：使用注解@ComponentScan(value=”com.yoodb.blog”)，其中，com.yoodb.blog为包路径。
方式二：将启动类Application放在上一级包中，注意的是Application启动类必须要保证在包的根目录下
在Repository配置类前面添加注解@EntityScan('entity对应的包路径')
### 部署至tomcat
<groupId>org.springframework.boot</groupId> 
  <artifactId>spring-boot-starter-tomcat</artifactId> 
  <scope>provided</scope> 
 </dependency>
public class Application extends SpringBootServletInitializer { 
 @Override
 protected SpringApplicationBuilder configure(SpringApplicationBuilder application) { 
 return application.sources(Application.class); 
 } 
 public static void main(String[] args) throws Exception { 
 SpringApplication.run(Application.class, args); 
 } 
}
### 乱码
不管是使用httpclient，还是okhttp，都要设置传参的编码，为了统一，这里全部设置为utf-8
spring.http.encoding.force=true
spring.http.encoding.charset=UTF-8
spring.http.encoding.enabled=true
server.tomcat.uri-encoding=UTF-8
produces="text/plain;charset=UTF-8"
# 深入实践spring boot
* 不再需要xml配置；；整合第三方技术；；2014年4月；；开发人员、系统设计师、架构师；；配置好开发环境：jdk、idea、maven、gradle、git，<localRepository></ocalRepository>，置顶git.exe；；https://start.spring.io；；项目创建、运行、发布；；tomcat默认开启了8080端口；；spring-boot-maven-plugin打包插件
* 通过导入starter模块，可以将许多程序依赖包自动导入工程；；使用parent pom可以更容易的管理依赖的版本和使用默认配置，工程中的模块也可以很方便地继承；；spring导入了整个springframework依赖以及autoconfigure、logging、slf4j、jackson、tomcat插件，这些都是一个web项目可能需要用到的东西
* @springbootapplication；；@restcontroller
* 使用数据库是开发基本应用的基础
