* 庞大且复杂/云计算/大数据/扩容/异常、降级和超时/基础架构演进、支付架构演进、移动端架构演进和混合云架构/分布式架构体系/数据库OceanBase/请求量和数据量
* HSF、TDDL、Notify
* 把系统部署在异地机房/异地多活架构/全量业务和全量数据/一致性和高可用性
* CDN到接入层、前端应用、后端服务、缓存、存储、中间件
* Fiddler抓SoapUI包
* 使用Python内部自带库去模拟发送http请求（替代web浏览器）
* http://www.hiktest.com/autodeploy/hitainstall
* 在RFID工具中按F5或菜单Tools->Search Keywords
* webstorm9.0.3激活码:
UserName:William 

===== LICENSE BEGIN ===== 
45550-12042010 
00001SzFN0n1bPII7FnAxnt0DDOPJA 
INauvJkeVJBuE5bqLEznccE4tet6tr 
RiyoMxDK8oDY93tx!ipPyGmqYYeWxS 
* ELK(ElasticSearch Logstash Kibana)
* @CrossOrigin(methods = { RequestMethod.GET, RequestMethod.POST }, origins = "*")
* <!-- 修改其他包的日志输出级别 -->
    <logger name="org.apache.zookeeper">
        <level value="WARN"/>
    </logger>

    <!-- root 默认日志配置 ， 注意这里的级别哈！小心生产环境用DEBUG，压爆你的磁盘！-->
    <root level="INFO">
        <appender-ref ref="logfile"/>
        <appender-ref ref="stdout"/>
    </root>
* application.yml application-dev.yml
* spring:
    application:
        name: index
    profiles:
      active: dev
* server:
    port: 9080
* hystrix:
  command:
      default:
          execution:
             isolation:
                  thread:
                      timeoutInMilliseconds: 10000
* logging:
  config: classpath:logback.xml
* eureka:
    client:
        serviceUrl:
            defaultZone: http://127.0.0.1:8761/eureka/
* spring:
    redis:
        host: 10.1.40.116
        port: 6379
        database: 1
* eureka:
    client:
        serviceUrl:
            defaultZone: http://127.0.0.1:8761/eureka/
#    instance:  
#        prefer-ip-address: true
    instance:
        hostname: ${spring.application.name}
        instance-id: ${spring.application.name}:${server.port}
        status-page-url: http://${spring.application.name}:${server.port}/swagger-ui.html
* @SpringBootApplication
* @ComponentScan
* @EnableDiscoveryClient
* @EnableFeignClients
* @EnableCaching
* @EnableCircuitBreaker
* Created by xxx on 2017/11/3.
* @NotNull(message = "请指定待调度的任务")
* public Result xxx(HttpServletRequest request, @RequestBody @Valid JobSchedulePO po, BindingResult check)
   if (check.hasErrors()) {
              return Result.FAILED(check.getAllErrors().get(0).getDefaultMessage());
          }
* private static final ObjectMapper MAPPER = new ObjectMapper();
* BeanUtils.copyProperties(dataResult.getData(), vo);
* <relativePath>../../../pom.xml</relativePath>
* <!-- 以下两条才能使 延迟加载有效 -->
		<setting name="aggressiveLazyLoading" value="false" />
		<setting name="lazyLoadingEnabled" value="true" />

		<setting name="cacheEnabled" value="true" />
		<setting name="multipleResultSetsEnabled" value="true" />
		<setting name="useColumnLabel" value="true" />
		<setting name="useGeneratedKeys" value="false" />
		<setting name="autoMappingBehavior" value="PARTIAL" />
		<setting name="defaultExecutorType" value="SIMPLE" />
		<setting name="defaultStatementTimeout" value="25000" />
		<setting name="safeRowBoundsEnabled" value="false" />
		<setting name="mapUnderscoreToCamelCase" value="false" />
		<setting name="localCacheScope" value="SESSION" />
		<setting name="jdbcTypeForNull" value="OTHER" />
		<setting name="lazyLoadTriggerMethods" value="equals,clone,hashCode,toString" />
		<!-- 打印sql日志 -->
		<!--<setting name="logImpl" value="STDOUT_LOGGING" />-->
* jpa:
        generate-ddl: true
        ddl-auto: update
        show_sql: true
        database: ORACLE
        properties:
            hibernate:
                dialect: org.hibernate.dialect.Oracle10gDialect
                naming:
                    physical-strategy: org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl
                ejb:
                   interceptor: com.xxx.xxx.db.listener.JpaSQLAdapter
* datasource:
        type: com.alibaba.druid.pool.DruidDataSource
        driver-class-name: oracle.jdbc.driver.OracleDriver
        connectionTimeout: 60000
        maximumPoolSize: 5
        initialSize: 5
        minIdle: 5
        maxActive: 20
        maxWait: 60000
        timeBetweenEvictionRunsMillis: 60000
        minEvictableIdleTimeMillis: 300000
        validationQuery: SELECT 1 FROM DUAL
        testWhileIdle: true
        testOnBorrow: false
        testOnReturn: false
        poolPreparedStatements: true
        maxPoolPreparedStatementPerConnectionSize: 20
*     jpa:
      properties:
        hibernate:
          default_schema: TMS_JOB
* eureka:
    client:
        serviceUrl:
            defaultZone: http://127.0.0.1:8761/eureka/
#    instance:  
#        prefer-ip-address: true
    instance:
        hostname: ${spring.application.name}
        instance-id: ${spring.application.name}:${server.port}
        status-page-url: http://${spring.application.name}:${server.port}/swagger-ui.html
* @EntityScan
* @EnableFeignClients
* @EnableTransactionManagement
* @HystrixCommand(fallbackMethod = "findNoBeginJobFallback")
* @HystrixCommand(commandProperties = {
            @HystrixProperty(name = "execution.isolation.t" +
                    "hread.timeoutInMilliseconds", value = "20000") })
* @Configuration
* @MapperScan(annotationClass=Repository.class,basePackages={"com.xxx.xxx.db"}, sqlSessionFactoryRef="sqlSessionFactory")
* fileName.replaceAll(" ", "-");
* response.setContentType("application/x-download");
* response.setHeader("Content-Disposition", "attachment;filename="+fileName);
* response.setContentType("application/json;charset=UTF-8");
* if((bytes[0] == 123 && bytes[bytes.length - 1] == 125) || bytes[0] == 91 && bytes[bytes.length - 1] == 93){
            return "application/json;charset=UTF-8";
        }
* String.format("%s_JobDBOtherController_findNoBeginJob_%s", Services.SERVICE_DB_JOB, BaseConstant.SYSTEM_THROWABLE)
* @RequestBody JobConditionDTO param,@RequestParam("userTeamId") Long userTeamId
* @Bean(name = "sqlSessionFactory")
	public SqlSessionFactoryBean setSqlSessionFactory(){
		SqlSessionFactoryBean bean = new SqlSessionFactoryBean();
		bean.setDataSource(dataSource);
		ClassPathResource resource = new ClassPathResource("mybatis/configuration.xml");
		bean.setConfigLocation(resource);
		PathMatchingResourcePatternResolver pathMatchingResourcePatternResolver = new PathMatchingResourcePatternResolver();
		try {
			List<Resource> resources = new ArrayList<>();
			resources.addAll(Arrays.asList(pathMatchingResourcePatternResolver.getResources("classpath*:com/xxx/xxx/db/**/dao/**/*MybatisDao.xml")));
			resources.addAll(Arrays.asList(pathMatchingResourcePatternResolver.getResources("classpath*:com/xxx/xxx/db/dao/**/*MybatisDao.xml")));
			resources.addAll(Arrays.asList(pathMatchingResourcePatternResolver.getResources("classpath*:com/xxx/xxx/db/**/dao/*MybatisDao.xml")));
			resources.addAll(Arrays.asList(pathMatchingResourcePatternResolver.getResources("classpath*:com/xxx/xxx/db/**/dao/**/*Mapper.xml")));
			resources.addAll(Arrays.asList(pathMatchingResourcePatternResolver.getResources("classpath*:com/xxx/xxx/db/dao/**/*Mapper.xml")));
			resources.addAll(Arrays.asList(pathMatchingResourcePatternResolver.getResources("classpath*:com/xxx/xxx/db/**/dao/*MybatisDao.xml")));
			bean.setMapperLocations(resources.toArray(new Resource[0]));
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		return bean;
	}
* @Bean
    public HttpMessageConverters getHttpMessageConverters(){
        return new WebMvcJSONConfigure().customConverters();
    }
* @Entity
@Table(name = "TMS_PROJECT_USER")
* @Id
    @Column(name = "ID", nullable = false, insertable = true, updatable = true,length = 10)
    @GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "JOB_PROJECT_USER_SEQ")
    @SequenceGenerator(sequenceName = "TMS_JOB_PROJECT_USER_SEQ", allocationSize = 1, name = "JOB_PROJECT_USER_SEQ")
* @Column(name = "USER_CONTACTER",length = 300)
* @ManyToOne(cascade={CascadeType.MERGE,CascadeType.REFRESH},optional=false)
  @ManyToOne(cascade={CascadeType.MERGE,CascadeType.REFRESH},optional=false)
    @JoinColumn(name="JOB_ID")
* @OneToMany(mappedBy="job",cascade={CascadeType.ALL})
        @OrderBy("scheduleTime DESC")
* @OneToOne(mappedBy = "job", cascade = {CascadeType.ALL})
* @JoinColumn(name="JOB_ID")
    @OneToOne(cascade={CascadeType.MERGE,CascadeType.REFRESH},optional=false)
* @Query("select t from SubJobTask t where t.customerProblemId = :customerProblemId")
* @Query("select jcr from JobCustomerReview jcr join jcr.job j where jcr.dataStatus = ?2 and rownum <= ?1 order by jcr.createDate desc")
