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
