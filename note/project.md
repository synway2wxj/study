* postgresql conn.prepareStatement
*            Service service = new Service();  call = service.createCall(); call.setTargetEndpointAddress(serviceUrl); call.setOperationName(new QName(namespace,methodName)); call.setReturnType(XMLType.XSD_BOOLEAN);
* org.apache.axis
* http://10.1.11.37:8080/ElasticSearchService/ESService?wsdl
* log4j
* @Inject
* @ModelAttribute
* category(Model model, Principal principal, @PageableDefault(size = 5) Pageable pageable, ModelMap modelMap, CasAuthenticationToken principal2,  @Valid Answer answer, BindingResult result,RedirectAttributes redirectAttributes)
* @RequestMapping(value = "/tags", method = RequestMethod.GET, produces = MediaType.APPLICATION_JSON_UTF8_VALUE)
* 		picContentType.add("image/jpeg");
		picContentType.add("image/pjpeg");
		picContentType.add("image/png");
		picContentType.add("image/x-png");
		picContentType.add("image/gif");
		picContentType.add("image/bmp");
* @RequestMapping(value = "/file/upload", method = RequestMethod.POST, produces = MediaType.TEXT_HTML_VALUE)
* @RequestMapping(value = "/answer/{answerId}", method = RequestMethod.POST, produces = "text/html;charset=utf-8")
* @Configuration
@EnableScheduling
* @Scheduled(cron = "0 30 1 * * ?")
* return "redirect:/error";
* HttpUtil.doHttpGet(query,elasticsearch_url_query1);
  CloseableHttpClient httpClient = HttpClients.createDefault();
  URL=URL.replace(" ","+");
  HttpGet httpGet=new HttpGet(URL);
  httpGet.addHeader("Content-Type","application/json; charset=utf-8");
  httpGet.setHeader("Accept", "application/json");
  HttpResponse response = httpClient.execute(httpGet);
  response.getStatusLine().getStatusCode();
  EntityUtils.toString(response.getEntity());
  
  httpPost.setEntity(new StringEntity(data, Charset.forName("UTF-8")));
  
  * @Bean
    public FilterRegistrationBean xssFilterRegistration() {
        FilterRegistrationBean registration = new FilterRegistrationBean();
        registration.setFilter(new XssFilter());//添加过滤器
        registration.addUrlPatterns("/*");//设置过滤路径，/*所有路径
        registration.setName("XssFilter");//设置优先级
        registration.setOrder(1);//设置优先级
        return registration;
    }
* LocalDateTime.ofInstant  LocalDateTime.parse
* IOUtils.closeQuietly(fInStream);
* timestamp = new Timestamp(format.parse(dateStr).getTime());
* Pattern pattern = Pattern.compile("<!\\[CDATA\\[");
        Matcher matcher = pattern.matcher(content);
* public class DataResult<T> implements Serializable
* MD5
* @Target(ElementType.PARAMETER)
@Retention(RetentionPolicy.RUNTIME)
@Documented
	
* @Configuration
@ConditionalOnClass({ freemarker.template.Configuration.class, FreeMarkerConfigurationFactory.class })
@AutoConfigureAfter(WebMvcAutoConfiguration.class)

* @ControllerAdvice
	@ExceptionHandler(InvalidDataAccessApiUsageException.class)
	HttpHeaders httpHeaders = new HttpHeaders();
	httpHeaders.setContentType(MediaType.APPLICATION_JSON_UTF8);
* return new ResponseEntity("数据库连接异常", status);
* URLEncoder.encode(((SimpleScalar) arguments.get(0)).getAsString(), "UTF-8");
* public class AttachmentDirective implements TemplateDirectiveModel
* public class CommonInterceptor implements HandlerInterceptor
* java8 Optional
@EnableConfigurationProperties(FreeMarkerProperties.class)
* WebSecurityConfigurerAdapter
* logging.level.root=WARN
logging.level.org.apache=INFO
logging.level.org.springframework=ERROR
logging.level.org.springframework.security=ERROR
logging.level.org.springframework.boot.context.web=ERROR
logging.level.org.hibernate.SQL=DEBUG
logging.file=${user.home}/.km/km.log
* spring.freemarker.settings.auto_import=web/macro/common.ftl as cmn, web/macro/home.ftl as h


***ttt
// 代理工厂
JaxWsProxyFactoryBean jaxWsProxyFactoryBean = new JaxWsProxyFactoryBean();
// 设置代理地址
jaxWsProxyFactoryBean.setAddress(address);

// 创建动态客户端
JaxWsDynamicClientFactory factory = JaxWsDynamicClientFactory.newInstance();
//登录验证
if (StringUtils.isNotEmpty(username)) {
    Authenticator.setDefault(new MyAuthenticator(username, password));
}
Client client = factory.createClient(wsdlUrl);

@EnableCaching
@EnableAsync
@EnableWs
@Async

$("#jobEditWrap").validate

Authenticator.setDefault(new MyAuthenticator(username, password));
JaxWsDynamicClientFactory factory = JaxWsDynamicClientFactory.newInstance();
QName service = new QName(namespace, servicename);
QName HTTPPort = new QName(namespace, httpport);
Client client = factory.createClient(wsdluri, service, HTTPPort);

HTTPConduit http = (HTTPConduit) client.getConduit();
HTTPClientPolicy httpClientPolicy = new HTTPClientPolicy();
httpClientPolicy.setConnectionTimeout(10000); // 连接超时，5分钟，数据来源于SAP接口方
httpClientPolicy.setAllowChunking(false); // 取消块编码
httpClientPolicy.setReceiveTimeout(180000); // 响应超时
http.setClient(httpClientPolicy);

@Bean
public Endpoint endpoint() {
EndpointImpl endpoint = new EndpointImpl(bus, wsDpmService);
endpoint.publish("/DpmService");
return endpoint;
}
@WebService(name = "xxx", // 暴露服务名称
        targetNamespace = "http://xxx/"// 命名空间,一般是接口的包名倒序
)
@WebMethod
@WebResult(name = "String")
@WebService(serviceName = "xxx", // 与接口中指定的name一致
        targetNamespace = "http://xxx/", // 与接口中的命名空间一致,一般是接口的包名倒
        endpointInterface = "xxx"// 接口地址
)

response.setContentType("image/png");
            outputStream = response.getOutputStream();
            outputStream.write(imgageBytes);
	    byte[] imgageBytes = HttpClient.getBytes(wechatUrl + "?scene_str=" + jobId);
	    
CloseableHttpClient httpclient = HttpClients.createDefault();
        try {
            // 创建httpget.
            HttpGet httpget = new HttpGet(url);
            // 执行get请求.
            CloseableHttpResponse response = httpclient.execute(httpget);
            try {
                // 获取响应实体
                HttpEntity entity = response.getEntity();
                // 打印响应状态
                System.out.println(response.getStatusLine());
                if (entity != null) {
                    return EntityUtils.toByteArray(entity);
                }
		
 // 创建默认的httpClient实例.
        CloseableHttpClient httpclient = HttpClients.createDefault();
        // 创建httppost
        HttpPost httppost = new HttpPost(url);
        UrlEncodedFormEntity uefEntity;
        try {
            uefEntity = new UrlEncodedFormEntity(params, "UTF-8");
            httppost.setEntity(uefEntity);
            System.out.println("executing request " + httppost.getURI());
            CloseableHttpResponse response = httpclient.execute(httppost);
@Query("select distinct(city) from xxx where province = ?1")
