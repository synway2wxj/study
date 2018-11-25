* 一、java7以前在switch中只能使用number或enum。现在可以使用string了
* 二、java7以前对某些资源的操作是需要手动关闭，如InputStream，Writes，Sockets，Sql等，需要在finally中进行关闭资源的操作，现在不需要使用finally来保证打开的流被正确关闭，现在是自动完成的，会自动释放资源,确保每一个资源在处理完成后都会关闭
* 任何实现了java.lang.AutoCloseable接口和java.io.Closeable接口的对象. 如果在try语句中写入了没有实现该接口的
* OutputStream fos = null;
		try {
			fos = new FileOutputStream("D:/file");
		} finally {
			fos.close();
* try(OutputStream fos = new FileOutputStream("D:/file");){
			// 不需要再次指明fos.close();
		}
*  三、java7以前在一个方法抛出多个异常时，只能一个个的catch，这样代码会有多个catch,显得很不友好，现在只需一个catch语句，多个异常类型用"|"隔开
* 泛型实例化类型自动推断
* 四、Java7前支持十进制（123）、八进制（0123）、十六进制（0X12AB） Java7增加二进制表示（0B11110001、0b11110001）
* 五、Java7中支持在数字中间增加'_'作为分隔符，分隔长int以及long（也支持double,float），显示更直观，如（12_123_456）
* 六、泛型实例化类型自动推断
* suppress异常
IOException readException = null;readException.addSuppressed(ex);
* ELProcessor el = new ELProcessor();
* FileChannel channel = FileChannel.open(Paths.get("my.txt")
* Path接口 DirectoryStream Files
* WatchService service = FileSystems.getDefault().newWatchService();
* jcmd -l列出所有的Java虚拟机
* jcmd pid VM.flags查看启动参数
* jcmd pid Thread.print 打印线程栈
* jcmd pid VM.uptime 查看虚拟机启动时间
* jcmd pid PerfCounter.print 查看性能统计
* jcmd pid VM.system_properties查看系统属性内容
* jcmd pid GC.class_histogram查看系统中类的统计信息
* jcmd pid GC.heap_dump D:d.dump 导出堆信息
* Java7提供的一个用于并行执行任务的框架，是一个把大任务分割成若干个小任务，最终汇总每个小任务结果后得到大任务结果的框架
RecursiveAction:用于没有返回结果的任务
RecursiveTask:用于有返回结果的任务
ForkJoinPool：任务ForkJoinTask需要通过ForkJoinPool来执行
CountTask leftTask = new  CountTask(start,middle);
CountTask rightTask = new  CountTask(middle+1,end);
//执行子任务
leftTask.fork();
rightTask.fork();
//等待子任务执行完，并得到执行结果
int leftResult = leftTask.join();
int rightResult = rightTask.join();
//合并子任务
sum = leftResult + rightResult;

if(task.isCompletedAbnormally())
{
    System.out.println(task.getException());
}
ForkJoinPool()  以Runtime.availableProcessors()方法的返回值作为parallelism参数来创建ForkJoinPool
* 异步执行        　 execute(ForkJoinTask)    　　　　 ForkJoinTask.fork
等待获取结果    　　invoke(ForkJoinTask)    　　　　  ForkJoinTask.invoke
执行,获取Future    submit(ForkJoinTask)  　　　　　　ForkJoinTask.fork(ForkJoinTask are Futures)




ForkJoinPool forkJoinPool = new ForkJoinPool();
CountTask task = new CountTask(1,6);
//执行一个任务
Future<Integer> result = forkJoinPool.submit(task);



* java5 
泛型（通配符/限制类型）public static <A extends Number> double sum(Box<A> box1,Box<A> box2)
枚举（EnumMap，switch枚举）
装箱拆箱
变长参数
注解（Inherited表示该注解是否对类的子类继承的方法等起作用，rentation表示annotation是否保留在编译过的class文件中还是在运行时可读）
foreach循环
静态导入（import static java.lang.System.out）
格式化（String.format("Duke's Birthday: %1$tm %1$te,%1$tY", c)）
/**
 * java.text.DateFormat
 * java.text.SimpleDateFormat
 * java.text.MessageFormat
 * java.text.NumberFormat
 * java.text.ChoiceFormat
 * java.text.DecimalFormat
 */
线程框架/数据结构（class SimpleThreadExceptionHandler implements Thread.UncaughtExceptionHandler  BlockingQueue q）
Arrays工具类/StringBuilder/instrument（Queue q = new LinkedList(); 采用它来实现queue；单线程StringBuilder线程不安全，在单线程下替换string buffer提高性能）

* 现在的Java SE版本中，不需要考虑用final去提升方法调用效率。只有在确定不想让该方法被覆盖时，才将方法设置为final
* string+="hello"的操作事实上会自动被JVM优化成
* 事实上，StringBuilder和StringBuffer类拥有的成员属性以及成员方法基本相同，区别是StringBuffer类的成员方法前面多了一个关键字：synchronized
* String a = "hello2"; 　　String b = "hello" + 2; 　　System.out.println((a == b));输出结果为：true。原因很简单，"hello"+2在编译期间就已经被优化成"hello2"，因此在运行期间，变量a和变量b指向的是同一个对象
* String a = "hello2"; 　  String b = "hello";       String c = b + 2;       System.out.println((a == c));
输出结果为:false。由于有符号引用的存在，所以  String c = b + 2;不会在编译期间被优化，不会把b+2当做字面常量来处理的，因此这种方式生成的对象事实上是保存在堆上的。因此a和c指向的并不是同一个对象
* String a = "hello2";   　 final String b = "hello";       String c = b + 2;       System.out.println((a == c));
输出结果为：true。对于被final修饰的变量，会在class文件常量池中保存一个副本，也就是说不会通过连接而进行访问，对final变量的访问在编译期间都会直接被替代为真实的值。那么String c = b + 2;在编译期间就会被优化成：String c = "hello" + 2
* Java的异常非为受检异常和非受检异常。由于在多线程中，run()方法无法继续向上显式抛出异常;;一旦一个线程抛出了非受检异常，JVM就会把它杀死，然后把捕获到的非受检异常传递给UncaughtExceptionHandler类对象类处理
*  { ArgumentIndex , FormatType , FormatStyle }
   number：调用NumberFormat进行格式化
  
   date：调用DateFormat进行格式化
   time：调用DateFormat进行格式化
   choice：调用ChoiceFormat进行格式化
          short
          medium
          long
          full
          integer
          currency
          percent
          SubformatPattern (子格式模式，形如#.##)
* # 数字 代表阿拉伯数字，每一个#表示一位阿拉伯数字，如果该位不存在则不显示        
* ChoiceFormat在构造方法中接收一个format数组和一个limits数组，这两个数组的长度必须相等 ChoiceFormat format = new ChoiceFormat(limits, formats);
相当于以数字为键，字符串为值的键值对。分别使用一组double类型的数组作为键，一组String类型的数组作为值，两数组相同索引值的元素作为一对


* JSR223脚本引擎
ScriptEngineManager manager = new ScriptEngineManager();
        //支持通过名称、文件扩展名、MIMEtype查找
        ScriptEngine engine = manager.getEngineByName("JavaScript");
* java9
* 1、Java 平台级模块系统
2、Linking
3、JShell : 交互式 Java REPL
4、改进的 Javadoc
5、集合工厂方法
6、改进的 Stream API
7、私有接口方法
8、HTTP/2
HttpClient client = HttpClient.newHttpClient();
HttpRequest req =
   HttpRequest.newBuilder(URI.create("http://www.google.com"))
              .header("User-Agent","Java")
              .GET()
              .build();
HttpResponse<String> resp = client.send(req, HttpResponse.BodyHandler.asString());
* 多版本兼容 JAR


很难真正地对代码进行封装, 而系统并没有对不同部分（也就是 JAR 文件）之间的依赖关系有个明确的概念
当启动一个模块化应用时， JVM 会验证是否所有的模块都能使用，这基于 `requires` 语句
创建针对应用程序进行优化的最小运行时映像而不需要使用完全加载 JDK 安装版本
* Set<Integer> ints = Set.of(1, 2, 3);
List<String> strings = List.of("first", "second");


* Java 平台级模块系统
* JAD：把java类文件反编译成java源代码
* 和程序中的其他补发一样，异常部分也需要经过仔细的考虑和设计；开发人员一般会花费大量的精力对程序的主要功能补发进行设计，二忽略异常的设计
一般来说，对于程序中可能出现的各种错误，都需要声明一个异常类与之对应；有些开发人员会选择一个大而全的异常类来表示各种不同类型的错误，利用这个异常的消息来区分不同的错误；不过异常的处理折需要
解析异常的消息格式来判断具体类型，应该换成不同的异常类；每个异常都需要包含尽量丰富的信息


