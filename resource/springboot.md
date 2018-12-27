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

---
* [配置页](https://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html "配置页")
* logging.config
* logging.file
* logging.file.max-history
* logging.file.max-size
* logging.level.org.springframework=DEBUG
* logging.path=/var/log
* logging.pattern.console=
* logging.pattern.dateformat=yyyy-MM-dd HH:mm:ss.SSS
* logging.pattern.file
* logging.pattern.level=%5p

---
* spring.aop.auto=true
* spring.aop.proxy-target-class=true

---
* spring.application.name
* spring.autoconfigure.exclude

---
* spring.banner.charset=UTF-8
* spring.banner.location=classpath:banner.txt
* spring.banner.image.location=classpath:banner.gif
* spring.main.banner-mode=console

---
* spring.cache.ehcache.config
* spring.cache.jcache.config
* spring.cache.jcache.provider
* spring.cache.redis.cache-null-values=true
* spring.cache.redis.key-prefix
* spring.cache.redis.time-to-live
* spring.cache.redis.use-key-prefix=true

---
* spring.mail.host
* spring.mail.username
* spring.mail.password
* spring.mail.port

---
* spring.messages.basename=messages
* spring.messages.cache-duration

---
* spring.profiles.active
* spring.profiles.include

---
* spring.quartz.properties.*
* spring.quartz.startup-delay

---
* spring.task.execution.pool.core-size=8
* spring.task.execution.pool.keep-alive=60s
* spring.task.execution.pool.max-size
* spring.task.execution.pool.queue-capacity
* spring.task.execution.thread-name-prefix=task-
* spring.task.scheduling.pool.size=1
* spring.task.scheduling.thread-name-prefix=scheduling-

---
* server.address
* server.error.path=/error # Path of the error controller
* server.port=8080
* server.servlet.context-path
* server.servlet.application-display-name=application
* server.servlet.session.timeout=30m
* server.tomcat.accept-count=100
* server.tomcat.basedir
* server.tomcat.max-connections=10000
* server.tomcat.max-threads=200

---
* spring.http.encoding.charset=UTF-8
* spring.http.encoding.force-request
* spring.http.encoding.force-response

---
* spring.servlet.multipart.enabled=truespring.servlet.multipart.enabled=true
* spring.servlet.multipart.file-size-threshold=0B
* spring.servlet.multipart.location
* spring.servlet.multipart.max-file-size=1MB
* spring.servlet.multipart.max-request-size=10MB
* spring.servlet.multipart.resolve-lazily=false

---
* spring.jackson.date-format
* spring.jackson.time-zone
* spring.gson.date-format

---
* spring.mvc.async.request-timeout
* spring.mvc.date-format
* spring.mvc.servlet.load-on-startup=-1
* spring.mvc.servlet.path=/
* spring.mvc.static-path-pattern=/**
* spring.mvc.view.prefix
* spring.mvc.view.suffix

---
* spring.resources.add-mappings=true
* spring.session.timeout

---
* spring.session.jdbc.cleanup-cron=0 * * * * *

---
* spring.session.redis.cleanup-cron=0 * * * * *
* spring.session.redis.flush-mode=on-sav
* spring.session.redis.namespace=spring:session

---
* spring.webservices.path=/
* spring.webservices.servlet.load-on-startup=-1
* spring.webservices.wsdl-locations

---
* spring.security.user.roles
* spring.security.oauth2.client.provider.*

---
* spring.flyway.enabled=true
* spring.flyway.locations=classpath:db/migration
* spring.flyway.sql-migration-suffixes=.sql

---
* spring.data.rest.base-path

---
* spring.data.solr.host=http://127.0.0.1:8983/solr
* spring.data.solr.zk-host

---
* spring.datasource.name
* spring.datasource.password
* spring.datasource.platform=all
* spring.datasource.url
* spring.datasource.type

---
* spring.elasticsearch.jest.connection-timeout=3s
* spring.elasticsearch.jest.password
* spring.elasticsearch.jest.username
* spring.elasticsearch.jest.read-timeout=3s

---
* spring.jpa.hibernate.ddl-auto
* spring.jpa.generate-ddl=false
* spring.jpa.mapping-resources
* spring.jpa.show-sql=false
* spring.jpa.database
* spring.jpa.database-platform
* spring.jta.enabled=true
* spring.jta.transaction-manager-id
* spring.jta.atomikos.connectionfactory.borrow-connection-timeout=30
* spring.jta.bitronix.connectionfactory.acquire-increment=1
* spring.transaction.default-timeout

---
* spring.redis.database=0
* spring.redis.url
* spring.redis.host
* spring.redis.password
* spring.redis.port=6379

---
* spring.activemq.broker-url
* spring.activemq.user
* spring.activemq.password
* spring.rabbitmq.addresses

---
* spring.kafka.admin.client-id
* spring.rabbitmq.host

---
* spring.devtools.restart.additional-exclude
* spring.devtools.restart.additional-paths
* spring.devtools.remote.context-path

* spring.redis.timeout
