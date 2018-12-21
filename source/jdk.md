# String
# IdentityHashMap
# LinkedHashMap 
# EnumMap
# SortedMap
# TreeMap
# WeakHashMap
# ConcurrentHashMap
# LinkedList
# PriorityQueue
# ArrayDeque
# ArrayList
# CopyOnWriteArrayList
CopyOnWriteArrayList通过在新增元素时, 复制一份新的数组出来, 并在其中写入数据, 之后将原数组引用指向到新数组.
其Add操作是在内部通过ReentrantLock进行锁保护, 防止多线程场景复制多份数组.
而Read操作内部无锁, 直接返回数组引用, 并发下效率高, 因此适用于读多写少的场景.
ArrayList在遍历的时候会check modCount是否发生变化, 如果一边读一边写就会抛异常
# LinkedList
# Stack
# HashSet
# NavigibleSet
# TreeSet
# SortedSet
# LinkedHashSet
# CopyOnWriteSet
# BitSet
# Observer
# Observable
# Runtime
# ClassLoader
# Process
# GregorianCalendar
# Timer
# wait notify
# PipedOutputStream 
# ThreadLocal
# ExecutorService Executors
# Callable Future
# ReentrantLock ReentrantReadWriteLock
# Condition
# Semaphore
信号量可以是一个线程获取, 另一个线程释放
# CyclicBarrier
多个线程阶段点同步
# CountDownLatch
线程通过等待计数器归零来实现同步   实现一个人/多个人等待一个人/多个人的完成
# Exchanger
两个线程间互相交换数据
# BlockingQueue
阻塞队列是一个线程存入数据, 一个线程取出数据
当一个线程读取数据时, 如果队列是空的, 则当前线程会进入等待状态.
如果队列满了, 当一个线程尝试写入数据时, 同样会进入等待状态.
# AtomicInteger
# volatile
# LockSupport
一个线程阻塞工具, 可以在任意位置让线程阻塞
# Locale
既然要做到国际化，那么首先肯定得知道是哪个语言或区域；本地化、数据获取、格式化
数据隔离和获取一般使用ResourceBundle类配合properties文件使用，实际使用中，一般会定义一些properties文件，文件名前缀相同，后缀跟一些本地化的信息
# NumberFormat
# DecimalFormat
# DateTimeFormatter
# MessageFormat
# FileWriter
当把数据保存到一个文本文件中时，应该照顾到本地的字符编码，这样，用户就可以用它们的其他程序打开这个文本文件
java是完全基于Unicode的，但是 os 一般有它们自己的字符编码，比如在 美国是 ISO-8859-1
字符编码是在 FileWriter 的构造器中指定的： out = newFileWriter(filename, “ISO-8859-1”)；
作为 coder， 要牢记你需要与java 编译器进行交互： 这种交互需要通过本地系统的工具来完成
使用中文版的记事本来写你的java 源代码文件， 但这样写出来的源代码不能随处使用；因为它们使用的是本地的字符编码；
只有编译后的class 文件才能随处使用， 因为它们会自动地使用 “modified UTF-8” 编码来处理标识符和字符串。
源文件： 本地编码；
类文件： modified UTF-8；
虚拟机： UTF-16；
可以用 -encoding 标记来设定你的源文件的字符编码， 如 ， javac -encoding Big5 Myfile.java
为了使你的源文件到处都可用， 必须使用普通 的 ASCII 编码： 也就是说， 你需要将所有 非ASCII 字符转换成等价的 Unicode 编码；
jdk 有一个工具 native2ascii ：可以用它来将本地字符编码转换为 普通 的 ASCII ， 这个工具直接将输入中的每一个非 ASCII 字符替换为 跟尾儿 \u 加上四位 16进制数字的Unicode值；
native2ascii Myfile.java Myfile.temp
native2ascii -reverse myfile.temp myfily.java
native2ascii -encoding Big5 myfile.java myfile.temp
# Date LocalDate LocalTime LocalDateTime Instant Period Duration
日期（Date）、时间（Time）、日期时间（DateTime）、时间戳（unix timestamp）
 LocalDate localDate3 = LocalDate.now(ZoneId.of("Asia/Kolkata"));
 LocalDate localDate4 = LocalDate.ofEpochDay(365);
 LocalDate localDate5 = LocalDate.ofYearDay(2017, 200);
 LocalTime specificSecondTime = LocalTime.ofSecondOfDay(10000);
 today = LocalDateTime.of(LocalDate.now(), LocalTime.now());
 LocalDateTime dateFromBase = LocalDateTime.ofEpochSecond(10000, 0, ZoneOffset.UTC);
 Instant类是用在机器可读的时间格式上的，它以Unix时间戳的形式存储日期时间
 新的时区类java.time.ZoneId是原有的java.util.TimeZone类的替代品。ZoneId对象可以通过ZoneId.of()方法创建，也可以通过ZoneId.systemDefault()获取系统默认时区
 LocalDate today = LocalDate.now();
 LocalDate.of(2014, Month.JANUARY, 1);
 LocalDate todayAsia = LocalDate.now(ZoneId.of("Asia/Kolkata"));
 LocalDate ofEpochDay = LocalDate.ofEpochDay(365);
 LocalDate.ofYearDay(2014, 100);
 LocalTime now = LocalTime.now();
 LocalTime.of(23, 25, 45, 20);
 LocalTime timeOfAsia = LocalTime.now(ZoneId.of("Asia/Kolkata"));
 LocalTime ofSecondOfDay = LocalTime.ofSecondOfDay(10000);
 LocalDateTime today = LocalDateTime.now();
 today = LocalDateTime.of(LocalDate.now(), LocalTime.now());
 LocalDateTime specificDate = LocalDateTime.of(2014, Month.JANUARY, 1, 10, 10, 30);
 LocalDateTime todayKolkata = LocalDateTime.now(ZoneId.of("Asia/Kolkata"));
 LocalDateTime dateFromBase = LocalDateTime.ofEpochSecond(10000, 0, ZoneOffset.UTC);
 Instant instant = Instant.now();
 Instant ofEpochMilli = Instant.ofEpochMilli(instant.toEpochMilli());
 Duration duration = Duration.ofDays(30);
 java.time.Duration类用于代表两个Instant对象之间的一段时间
 Instant timestamp = new Date().toInstant();
 Instant time = Calendar.getInstance().toInstant();
 Date dt = Date.from(Instant.now());
ZoneId zone = ZoneId.systemDefault();
LocalDateTime localDateTime = LocalDateTime.ofInstant(instant, zone);
LocalTime localTime = localDateTime.toLocalTime();
ZoneId zone = ZoneId.systemDefault();
Instant instant = localDateTime.atZone(zone).toInstant();
Java的java.util.Date和java.util.Calendar类易用性差，不支持时区，并且是可变的

