# 文件上传、下载
* 浏览器在上传的过程中是将文件以流的形式提交到服务器端的，如果直接使用Servlet获取上传文件的输入流然后再解析里面的请求参数是比较麻烦，所以一般选择采用apache的开源工具common-fileupload这个文件上传组件
1. <form action="${pageContext.request.contextPath}/servlet/UploadHandleServlet" enctype="multipart/form-data" method="post">
2. this.getServletContext().getRealPath("/WEB-INF/upload");
3. DiskFileItemFactory factory = new DiskFileItemFactory();//1、创建一个DiskFileItemFactory工厂
ServletFileUpload upload = new ServletFileUpload(factory);//2、创建一个文件上传解析器
upload.setHeaderEncoding("UTF-8");//解决上传文件名的中文乱码
if(!ServletFileUpload.isMultipartContent(request))//3、判断提交上来的数据是否是上传表单的数据
List<FileItem> list = upload.parseRequest(request);//4、使用ServletFileUpload解析器解析上传数据，解析结果返回的是一个List<FileItem>集合，每一个FileItem对应一个Form表单的输入项
String name = item.getFieldName();
//解决普通输入项的数据的中文乱码问题
String value = item.getString("UTF-8");
//value = new String(value.getBytes("iso8859-1"),"UTF-8");
System.out.println(name + "=" + value);
}else{//如果fileitem中封装的是上传文件
//得到上传的文件名称，
String filename = item.getName();
System.out.println(filename);
if(filename==null || filename.trim().equals("")){
continue;
}
//注意：不同的浏览器提交的文件名是不一样的，有些浏览器提交上来的文件名是带有路径的，如：  c:\a\b\1.txt，而有些只是单纯的文件名，如：1.txt
//处理获取到的上传文件的文件名的路径部分，只保留文件名部分
filename = filename.substring(filename.lastIndexOf("\\")+1);
//获取item中的上传文件的输入流
InputStream in = item.getInputStream();
//创建一个文件输出流
FileOutputStream out = new FileOutputStream(savePath + "\\" + filename);
//创建一个缓冲区
byte buffer[] = new byte[1024];
//判断输入流中的数据是否已经读完的标识
int len = 0;
//循环将输入流读入到缓冲区当中，(len=in.read(buffer))>0就表示in里面还有数据
 while((len=in.read(buffer))>0){
//使用FileOutputStream输出流将缓冲区的数据写入到指定的目录(savePath + "\\" + filename)当中
out.write(buffer, 0, len);
}
//关闭输入流
in.close();
//关闭输出流
 out.close();
//删除处理文件上传时生成的临时文件
item.delete();
 message = "文件上传成功！";
}

//监听文件上传进度
upload.setProgressListener(new ProgressListener(){
public void update(long pBytesRead, long pContentLength, int arg2) {
System.out.println("文件大小为：" + pContentLength + ",当前已处理：" + pBytesRead);
/**
* 文件大小为：14608,当前已处理：4096
文件大小为：14608,当前已处理：7367
文件大小为：14608,当前已处理：11419
文件大小为：14608,当前已处理：14608
*/
}
});

upload.setFileSizeMax(1024*1024);//设置上传单个文件的大小的最大值，目前是设置为1024*1024字节，也就是1MB
upload.setSizeMax(1024*1024*10);//设置上传文件总量的最大值，最大值=同时上传的多个文件的大小的最大值的和，目前设置为10MB

request.getRequestDispatcher("/listfile.jsp").forward(request, response);

fileName = new String(fileName.getBytes("iso8859-1"),"UTF-8");

response.setHeader("content-disposition", "attachment;filename=" + URLEncoder.encode(realname, "UTF-8"));
4. 为保证服务器安全，上传文件应该放在外界无法直接访问的目录下，比如放于WEB-INF目录下
5. 为防止文件覆盖的现象发生，要为上传文件产生一个唯一的文件名
6. 为防止一个目录下面出现太多文件，要使用hash算法打散存储
7. 要限制上传文件的最大值
8. 要限制上传文件的类型，在收到上传文件名时，判断后缀名是否合法
* 下载就是向客户端响应字节数据! 将一个文件变成字节数组, 使用 response.getOutputStream() 
来响应给浏览器
* request.getServletContext().getMimeType(“文件名”)获取MIME类型
* 如果需要提示用户保存，利用Content-Disposition进行一下处理，关键在于一定要加上attachment。 例如：Content-Disposition:attachment;filename=xxx
* // 火狐浏览器
            if (agent.contains("Firefox")) { 
                filename = "=?UTF-8?B?"
                        + new BASE64Encoder().encode(filename.getBytes("utf-8"))
                        + "?=";
                filename = filename.replaceAll("\r\n", "");
            // IE及其他浏览器
            } else { 
                filename = URLEncoder.encode(filename, "utf-8");
                filename = filename.replace("+"," ");
            }
* String filePath = request.getRealPath(fileAddre);//取系统当前路径

---
spring boot
* 	@Bean
	public MultipartResolver multipartResolver() {
		CommonsMultipartResolver resolver = new CommonsMultipartResolver();
		resolver.setDefaultEncoding("UTF-8");
		resolver.setResolveLazily(true);// resolveLazily属性启用是为了推迟文件解析，以在在UploadAction中捕获文件大小异常
		resolver.setMaxInMemorySize(40960);
		resolver.setMaxUploadSize(UtilParse.getBytesNum(MultipartProperties.pros.getFileSize()) * 1024);// 上传文件大小M
		return resolver;
	}
	/**
	 * Tomcat large file upload connection reset
	 */
	@Bean
	public TomcatServletWebServerFactory tomcatEmbedded() {
		TomcatServletWebServerFactory tomcat = new TomcatServletWebServerFactory();
		tomcat.addConnectorCustomizers((TomcatConnectorCustomizer) connector -> {
			if ((connector.getProtocolHandler() instanceof AbstractHttp11Protocol<?>)) {
				// -1 means unlimited
				((AbstractHttp11Protocol<?>) connector.getProtocolHandler()).setMaxSwallowSize(-1);
			}
		});
		return tomcat;
	}
 * List<MultipartFile> files = ((MultipartHttpServletRequest)request).getFiles("fileName");
 * Spring Boot默认文件上传大小为2M，多文档上传中总是出现文件大小超出限度
 @Bean  
    public MultipartConfigElement multipartConfigElement() {  
        MultipartConfigFactory factory = new MultipartConfigFactory();  
        //单个文件最大  
        factory.setMaxFileSize("10240KB"); //KB,MB  
        /// 设置总上传数据总大小  
        factory.setMaxRequestSize("102400KB");  
        return factory.createMultipartConfig();  
    }
 * response.setContentType("application/force-download");
response.setHeader("Content-Disposition", "attachment;fileName=" + filename);
* String filePath = request.getSession().getServletContext().getRealPath("file/");
* response.setContentType("application/x-msdownload");
//设置文件名
response.addHeader("Content-Disposition","attachment;fileName="+fileName);
resp.setHeader("content-type", "application/octet-stream");
resp.setContentType("application/octet-stream");
resp.setHeader("Content-Disposition", "attachment;filename=" + fileName);
* BodyBuilder builder = ResponseEntity.ok();
 // 内容长度
 builder.contentLength(file.length());
 // application/octet-stream ： 二进制流数据（最常见的文件下载）。
 builder.contentType(MediaType.APPLICATION_OCTET_STREAM);
 if (userAgent.indexOf("MSIE") > 0) {
               // 如果是IE，只需要用UTF-8字符集进行URL编码即可
               builder.header("Content-Disposition", "attachment; filename=" + filename);
       } else {
               // 而FireFox、Chrome等浏览器，则需要说明编码的字符集
               // 注意filename后面有个*号，在UTF-8后面有两个单引号！
               builder.header("Content-Disposition", "attachment; filename*=UTF-8''" + filename);
       }
* #单个文件最大值
spring.http.multipart.max-file-size=10MB
##一个请求多个文件的最大值
spring.http.multipart.max-request-size=10MB
升级到2.0后需要改成
spring.servlet.multipart.max-file-size=10Mb  
spring.servlet.multipart.max-request-size=10Mb
 @Bean
    MultipartConfigElement multipartConfigElement() {
        MultipartConfigFactory factory = new MultipartConfigFactory();
        //文件最大
        factory.setMaxFileSize("5MB");
        /// 设置总上传数据总大小
        factory.setMaxRequestSize("10MB");
        return factory.createMultipartConfig();
    }

 
# 乱码
* 当URL地址里包含非西欧字符的字符串时,系统会将这些非西欧转换成如图所示的特殊字符串,那么编码过程中可能涉及将普通字符串和这种特殊字符串的相关转换,这就是需要使用URLDecoder和URLEncoder类
* URLDecoder和URLEncoder它的作用主要是用于普通字符串和application/x-www-form-rulencoded MIME字符串之间的转换
* request.getParameter("name")之前会自动做一次解码的工作，而且是默认的ISO-8859-1，相当于调用了一次java.net.URLDecoder.decode(name, "ISO-8859-1")
java.net.URLDecoder.decode(name, "UTF-8")
* application/x-www-form-urlencoded 在发送前编码所有字符（默认）
* multipart/form-data 不对字符编码。每一个表单项分割为一个部件
* text/plain 空格转换为 “+” 加号，但不对特殊字符编码。
* Java采用Unicode码编码方式，中英文字符均采用16bit存储。既然存储英文信息是正确的
* 目前的编码格式很多，例如 GB2312、GBK、UTF-8、UTF-16 这几种格式都可以表示一个汉字
* 存储空间重要还是编码的效率重要
* GB2312
它的全称是《信息交换用汉字编码字符集 基本集》，它是双字节编码，总的编码范围是 A1-F7，其中从 A1-A9 是符号区，总共包含 682 个符号，从 B0-F7 是汉字区，包含 6763 个汉字。　
GBK（扩展GB2312）
全称叫《汉字内码扩展规范》，是国家技术监督局为 windows95 所制定的新的汉字内码规范，它的出现是为了扩展 GB2312，加入更多的汉字，它的编码范围是 8140~FEFE（去掉 XX7F）总共有 23940 个码位，它能表示 21003 个汉字，它的编码是和 GB2312 兼容的，也就是说用 GB2312 编码的汉字可以用 GBK 来解码，并且不会有乱码。
* GB18030（兼容GB2312）
全称是《信息交换用汉字编码字符集》，是我国的强制标准，它可能是单字节、双字节或者四字节编码，它的编码与 GB2312 编码兼容，这个虽然是国家标准，但是实际应用系统中使用的并不广泛
* 1.UTF-8国际编码，GBK中文编码。GBK包含GB2312，即如果通过GB2312编码后可以通过GBK解码，反之可能不成立;
2、web tomcat:默认是ISO8859-1，不支持中文的
3.java.nio.charset.Charset.defaultCharset() 获得平台默认字符编码；
4.getBytes() 是通过平台默认字符集进行编码
* response.setContentType("text/html;charset=utf-8");或者 response.setHeader("content-type","text/html;charset=UTF-8");告诉浏览器用utf-8解析
* 不管是使用httpclient，还是okhttp，都要设置传参的编码，为了统一，这里全部设置为utf-8
* spring.http.encoding.force=true
spring.http.encoding.charset=UTF-8
spring.http.encoding.enabled=true
server.tomcat.uri-encoding=UTF-8
