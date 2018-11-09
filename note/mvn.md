* assertj-core
* assertj-guava
* joda-time
* guava
* commons-io
* commons-lang
* fastjson
* javax.inject
* javax.el-api
* javax.servlet-api
* postgresql
* axis
* javax.xml.rpc-api
* activation
* mail
* commons-discovery
* wsdl4j
* commons-jxpath
* commons-digester
* commons-collections
* commons-configuration
* log4j
* woodstox-core-asl
* cxf-rt-frontend-jaxws
* cxf-rt-transports-http
* druid
* spring-boot-starter-logging
* spring-boot-starter
* spring-boot-starter-test
* spring-boot-starter-freemarker
* jfreechart（图标生成工具）
* poi(办公文档转换工具)
* spring-boot-starter-tomcat
* spring-security-cas
* spring-security-taglibs
* cas-client-core exclusion commons-logging
* httpclient
* joda-time
* joda-time
* joda-time
* joda-time
* joda-time
* joda-time
* joda-time
* joda-time
* joda-time
* joda-time
* joda-time
* joda-time
* joda-time
* joda-time
* joda-time
* joda-time



* maven-compiler-plugin
* maven-source-plugin
* maven-release-plugin
* maven-war-plugin
* sonar-maven-plugin
* cxf-codegen-plugin
* spring-boot-maven-plugin
* tomcat7-maven-plugin

* ${basedir}/src/main/java
* <finalName>
* <directory>src/main/resources/${profiles.active}</directory>
*

* vo
* <endpoints
* logback
* hdfs

* logging.level.root=WARN
* logging.level.org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping=DEBUG
* logging.level.org.hibernate.SQL=DEBUG
* spring.jpa.properties.hibernate.dialect=com.hikvision.ipd.km.common.dialect.CustomOracleDialect
* spring.jpa.hibernate.ddl-auto=update
* spring.jpa.properties.hibernate.format_sql=true
* spring.freemarker.settings.auto_import=web/macro/common.ftl as cmn, web/macro/home.ftl as h
* spring.cache.guava.spec=maximumSize=500,expireAfterAccess=600s
* multipart.location=${user.home}/.km/files
multipart.max-file-size=50MB
multipart.max-request-size=50MB
* application.host=http://localhost
* @EnableAutoConfiguration(exclude={SecurityAutoConfiguration.class})
* sso

*         <profile>
            <id>debug</id>
            <build>
                <pluginManagement>

* JaxWsProxyFactoryBean factory = new JaxWsProxyFactoryBean();
        factory.setServiceClass(ElasticSearchWebService.class);
        factory.setAddress(url);
        this.elasticSearchWebService = (ElasticSearchWebService) factory.create();
        this.fileService = (FileService) factory.create();
        org.apache.cxf.endpoint.Client proxy = ClientProxy.getClient(this.fileService);
        HTTPConduit conduit = (HTTPConduit) proxy.getConduit();
        HTTPClientPolicy policy = new HTTPClientPolicy();
        policy.setReceiveTimeout(2400600);//请求超时时间 单位毫秒
        conduit.setClient(policy);
* json.getJSONArray("list").stream().map(t -> ((JSONObject) t).getString("deptCode")).collect(Collectors.toList());
* com.google.common.collect.Lists
*             <plugin>
                <groupId>org.apache.cxf</groupId>
                <artifactId>cxf-codegen-plugin</artifactId>
                <version>${cxf.version}</version>
                <configuration>
                    <sourceRoot>${basedir}/src/main/java</sourceRoot>
                    <wsdlOptions>
                        <wsdlOption>
                            <wsdl>${basedir}/src/main/resources/elasticSearchWebService.wsdl</wsdl>
                        </wsdlOption>
                        <wsdlOption>
                            <wsdl>${basedir}/src/main/resources/smsWebService.wsdl</wsdl>
                        </wsdlOption>
                        <wsdlOption>
                            <wsdl>${basedir}/src/main/resources/hrWebService.wsdl</wsdl>
                        </wsdlOption>
                        <wsdlOption>
                            <wsdl>${basedir}/src/main/resources/fileWebService.wsdl</wsdl>
                        </wsdlOption>
                        <wsdlOption>
                            <wsdl>${basedir}/src/main/resources/todoWebService.wsdl</wsdl>
                        </wsdlOption>
                    </wsdlOptions>
                </configuration>
                <executions>
                    <execution>
                        <id>generate-sources</id>
                        <phase>generate-sources</phase>
                        <goals>
                            <goal>wsdl2java</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
* <plugin>
                        <groupId>org.apache.tomcat.maven</groupId>
                        <artifactId>tomcat7-maven-plugin</artifactId>
                        <version>2.2</version>
                        <executions>
                            <execution>
                                <id>deploy</id>
                                <phase>install</phase>
                                <goals>
                                    <goal>redeploy</goal>
                                </goals>
                                <configuration>
                                    <username>admin</username>
                                    <password>admin</password>
                                    <url>http://10.1.44.250:8092/manager/text</url>
                                    <path>/</path>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
*   @Bean
  public ServletRegistrationBean dispatcherServlet() {
    return new ServletRegistrationBean(new CXFServlet(), "/soap/*");
  }
  @Bean(name = Bus.DEFAULT_BUS_ID)
  public SpringBus springBus() {
    return new SpringBus();
  }
  @Bean
  public WsService wsService() {
    return new WsServiceImpl();
  }
  
  @Bean
  public Endpoint endpoint() {
    EndpointImpl endpoint = new EndpointImpl(springBus(), wsService());
    endpoint.publish("/aaa");
    return  endpoint;
  }
*	@WebMethod
	@WebResult(name="String",targetNamespace="")




* <modules></modules>  <properties></properties>
*     <ciManagement>
        <system>jenkins</system>
        <url>http://10.7.12.13:8080/view/km/</url>
    </ciManagement>
*     <scm>
        <connection>scm:svn:https://192.0.0.230/OaApp/4.KM/4.Code/trunk/</connection>
         <!--给开发者使用的，类似connection元素。即该连接不仅仅只读--> 
        <developerConnection>scm:svn:https://192.0.0.230/OaApp/4.KM/4.Code/trunk/</developerConnection>
    </scm>
*     <repositories>
        <repository>
            <id>aliRepo</id>
            <name>aliRepo</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
            <releases>
                <enabled>true</enabled>
            </releases>
        </repository>
        <repository>
            <id>spring-snapshots</id>
            <name>Spring Snapshots</name>
            <url>http://repo.spring.io/snapshot</url>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
        </repository>
        <repository>
            <id>spring-milestones</id>
            <name>Spring Milestones</name>
            <url>http://repo.spring.io/milestone</url>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </repository>
        </repositories>
*     <distributionManagement>
        <repository>
            <id>hikvision</id>
            <url>http://10.1.11.30:81/nexus/content/repositories/hikvision/</url>
        </repository>
        <snapshotRepository>
            <id>hikvision</id>
            <url>http://10.1.11.30:81/nexus/content/repositories/snapshots/</url>
        </snapshotRepository>
    </distributionManagement>
* <dependencyManagement></dependencyManagement>
* <profiles></profiles>
* <relativePath></relativePath>

* <groupId>org.springframework.data</groupId>
            <artifactId>spring-data-commons</artifactId>
* <groupId>org.apache.tomcat.embed</groupId>
            <artifactId>tomcat-embed-core</artifactId>
* <groupId>net.sourceforge.jexcelapi</groupId>
            <artifactId>jxl</artifactId>
* <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
* relativePath元素中的地址–本地仓库–远程仓库 设定一个空值将始终从仓库中获取，不从本地路径获取，如<relativePath />
* <groupId>org.springframework.cloud</groupId>
* <groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-hystrix</artifactId>
* feign.hystrix.enabled=false		
* https://github.com/easonjim/spring-cloud-demo/tree/master/ZooKeeper
* <groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-actuator</artifactId>
* <artifactId>spring-cloud-starter-ribbon</artifactId>
* <artifactId>spring-cloud-starter-zookeeper-discovery</artifactId>
* <artifactId>spring-boot-starter-web</artifactId>
* <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-redis</artifactId>
			<exclusions>
				<exclusion>
					<groupId>org.springframework.boot</groupId>
					<artifactId>spring-boot-starter-tomcat</artifactId>
				</exclusion>
				<exclusion>
					<artifactId>org.springframework.data</artifactId>
					<groupId>spring-data-redis</groupId>
				</exclusion>
			</exclusions>
		</dependency>
* <groupId>io.github.openfeign</groupId>
			<artifactId>feign-core</artifactId>
* Feign的工作是将注释处理成一个临时的请求 在输出之前，参数以一种简单的方式应用于这些模板。尽管Feign仅限于支持基于文本的api，但它极大地简化了系统方面，比如重新播放请求。此外
* <groupId>org.projectlombok</groupId>  
     <artifactId>lombok</artifactId>  
* 为了能够得到实体Person类，还需要用到Feign提供的一个Gson解码器 
* <groupId>io.github.openfeign</groupId>
	<artifactId>feign-gson</artifactId>
* <groupId>org.apache.poi</groupId>
			<artifactId>poi</artifactId>
* <groupId>org.apache.poi</groupId>
			<artifactId>poi-ooxml</artifactId>
* <groupId>ch.qos.logback</groupId>
			<artifactId>logback-access</artifactId>
* <groupId>ch.qos.logback</groupId>
			<artifactId>logback-access</artifactId>
* <groupId>com.oracle</groupId>
			<artifactId>ojdbc</artifactId>
* <groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
* <groupId>org.springframework.data</groupId>
			<artifactId>spring-data-commons</artifactId>
* <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
			<exclusions>
				<exclusion>
					<groupId>org.apache.tomcat</groupId>
					<artifactId>tomcat-jdbc</artifactId>
				</exclusion>
			</exclusions>
		</dependency>
* <groupId>net.sf.ehcache</groupId>
			<artifactId>ehcache</artifactId>
* <groupId>com.alibaba</groupId>
			<artifactId>druid</artifactId>
* <groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
* <groupId>com.github.pagehelper</groupId>
			<artifactId>pagehelper-spring-boot-starter</artifactId>
			<artifactId>spring-cloud-starter-eureka</artifactId>
* <groupId>commons-fileupload</groupId>
            <artifactId>commons-fileupload</artifactId>
* <groupId>junit</groupId>
            <artifactId>junit</artifactId>
* <groupId>org.apache.httpcomponents</groupId>
            <artifactId>httpclient</artifactId>
* <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-aop</artifactId>
* <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger2</artifactId>
* <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger-ui</artifactId>
* <groupId>commons-io</groupId>
            <artifactId>commons-io</artifactId>
* <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-netflix</artifactId>
* Netflix的微服务大规模的应用，在技术上毫无保留的把一整套微服务架构核心技术栈开源了出来，叫做Netflix OSS
* Pivotal在Netflix开源的一整套核心技术产品线的同时，做了一系列的封装，就变成了Spring Cloud
* <groupId>org.springframework.session</groupId>
			<artifactId>spring-session-data-redis</artifactId>
* <groupId>org.springframework.session</groupId>
 8     <artifactId>spring-session</artifactId>
* <bean class="org.springframework.session.data.redis.config.annotation.web.http.RedisHttpSessionConfiguration">
20         <!-- 过期时间100分钟 -->
21         <property name="maxInactiveIntervalInSeconds" value="6000"></property>
22     </bean>
* <filter>
 2     <filter-name>springSessionRepositoryFilter</filter-name>
 3     <filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>
 4 </filter>
* <session-config>
10     <!--60*60*24-->
11     <session-timeout>86400</session-timeout>
12 </session-config>
* 粘性Session是指将用户锁定到某一个服务器上，比如上面说的例子，用户第一次请求时，负载均衡器将用户的请求转发到了A服务器上，如果负载均衡器设置了粘性Session的话，那么用户以后的每次请求都会转发到A服务器上，相当于把用户和A服务器粘到了一块，这就是粘性Session机制（缺乏容错性，如果当前访问的服务器发生故障，用户被转移到第二个服务器上时，他的session信息都将失效）
* 以Nginx为例，在upstream模块配置ip_hash属性即可实现粘性Session。
upstream mycluster{
    #这里添加的是上面启动好的两台Tomcat服务器
    ip_hash;#粘性Session
     server 192.168.22.229:8080 weight=1;
     server 192.168.22.230:8080 weight=1;
}
* 服务器session复制
原理：任何一个服务器上的session发生改变（增删改），该节点会把这个 session的所有内容序列化，然后广播给所有其它节点，不管其他服务器需不需要session，以此来保证Session同步
* 1设置tomcat ，server.xml 开启tomcat集群功能
* 2在应用里增加信息：通知应用当前处于集群环境中，支持分布式 
* session共享机制使用分布式缓存方案比如memcached、redis，但是要求Memcached或Redis必须是集群
* 不同的 tomcat指定访问不同的主memcached。多个Memcached之间信息是同步的，能主从备份和高可用。用户访问时首先在tomcat中创建session，然后将session复制一份放到它对应的memcahed上。memcache只起备份作用，读写都在tomcat上。当某一个tomcat挂掉后，集群将用户的访问定位到备tomcat上，然后根据cookie中存储的SessionId找session，找不到时，再去相应的memcached上去session，找到之后将其复制到备tomcat上
* memcached做主从复制，写入session都往从memcached服务上写，读取都从主memcached读取，tomcat本身不存储session
* 用开源的msm插件解决tomcat之间的session共享：Memcached_Session_Manager（MSM）
* JAVA memcached客户端：spymemcached.jar
* 1. 核心包，memcached-session-manager-{version}.jar
2. Tomcat版本对应的jar包：memcached-session-manager-tc{tomcat-version}-{version}.jar
序列化工具包：可选kryo，javolution,xstream等，不设置时使用jdk默认序列化
* https://blog.csdn.net/woaigaolaoshi/article/details/50902010
* 如果网站的访问量很大，把session存储到数据库中，会对数据库造成很大压力，还需要增加额外的开销维护数据库
* Terracotta的基本原理是对于集群间共享的数据，当在一个节点发生变化的时候，Terracotta只把变化的部分发送给Terracotta服务器，然后由服务器把它转发给真正需要这个数据的节点
这样对网络的压力就非常小，各个节点也不必浪费CPU时间和内存进行大量的序列化操作。把这种集群间数据共享的机制应用在session同步上，既避免了对数据库的依赖，又能达到负载均衡和灾难恢复的效果
* 就应用广泛性而言，第三种方式，也就是基于第三方缓存框架共享session，应用的最为广泛，无论是效率还是扩展性都很好。而Terracotta作为一个JVM级的开源群集框架，不仅提供HTTP Session复制，它还能做分布式缓存，POJO群集，跨越群集的JVM来实现分布式应用程序协调
* <groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-eureka</artifactId>
* <groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-zuul</artifactId>
* <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-eureka-server</artifactId>
* <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web-services</artifactId>
* <groupId>wsdl4j</groupId>
            <artifactId>wsdl4j</artifactId>
* <groupId>org.apache.cxf</groupId>
            <artifactId>cxf-spring-boot-starter-jaxws</artifactId>
* <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <version>1.5.1.RELEASE</version>
  </dependency>
 <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                   <!--fork :  如果没有该项配置，肯呢个devtools不会起作用，即应用不会restart -->
                    <fork>true</fork>
                </configuration>
</plugin>
* <plugin>
                <groupId>org.jvnet.jaxb2.maven2</groupId>
                <artifactId>maven-jaxb2-plugin</artifactId>
                <version>${wsdl.jaxb2.version}</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>generate</goal>
                        </goals>
                    </execution>
                </executions>
	<configuration>
                    <schemaLanguage>WSDL</schemaLanguage>
                    <generatePackage>com.hikvision.tms.ws</generatePackage>
                    <generateDirectory>${basedir}/src/main/java</generateDirectory>
                    <schemas>
                        <schema>
                            <fileset>
                                Defaults to schemaDirectory.
                                <directory>${basedir}/src/main/resources/wsdl</directory>
                                Defaults to schemaIncludes.
                                <includes>
                                    <include>*.wsdl</include>
                                </includes>
                                Defaults to schemaIncludes
                                <excludes>
                                <exclude>*.xs</exclude>
                                </excludes>
                            </fileset>
                            <url>http://localhost:8080/ws/countries.wsdl</url>
                        </schema>
                    </schemas>
                </configuration>
* <resource>
				<directory>src/main/java</directory>
				<includes>
					<include>**/*.xml</include>
				</includes>
			</resource>
			<resource>
				<directory>src/main/resources</directory>
				<includes>
					<include>**</include>
				</includes>
			</resource>
            </plugin>
