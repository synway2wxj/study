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

# 乱码
* 当URL地址里包含非西欧字符的字符串时,系统会将这些非西欧转换成如图所示的特殊字符串,那么编码过程中可能涉及将普通字符串和这种特殊字符串的相关转换,这就是需要使用URLDecoder和URLEncoder类
* URLDecoder和URLEncoder它的作用主要是用于普通字符串和application/x-www-form-rulencoded MIME字符串之间的转换
