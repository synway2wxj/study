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
