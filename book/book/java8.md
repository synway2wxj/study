* java8
* java8的许多新特性，java7中许多未被关注的
* ajva程序员、软件设计师、架构师、软件开发者
* java8 java语言和库获得了新生
* 客户端的开发人员需要转到javafx api
* lambda是一段可以传递的代码，可以被执行一次货多次
* 参数 箭头(->) 一级一个表达式
* 如果一个lambda参数类型是可以被推倒的，可以省略它们的类型；甚至可以省略小括号；可以添加注解或者final
* 对于只包含一个抽象方法的接口，可以通过lambda表达式来创建该接口的对象
* 函数式接口的转换是你在java中用lambda能做的唯一一件事
* 为接口添加静态方法
* Lambda表达式的本质只是一个"语法糖"；由编译器推断并帮你转换包装为常规的代码,因此你可以使用更少的代码来实现同样的功能；允许你通过表达式来代替功能接口
 lambda表达式就和方法一样,它提供了一个正常的参数列表和一个使用这些参数的主体；Lambda表达式还增强了集合库。 Java SE 8添加了2个对集合数据进行批量操作的包: java.util.function 包以及java.util.stream 包
 * NetBeans 和IntelliJ IDEA 一类的工具和IDE就支持Java 8特性
 * (parameters) -> expression 或 (parameters) ->{ statements; }
 () -> 5不需要参数,返回值为 5 
 players.forEach((player) -> System.out.print(player + "; "));
 players.forEach(System.out::println);
 * Stream使用懒运算,他们并不会真正地读取所有数据,遇到像getFirst() 这样的方法就会结束链式语法
 * javaProgrammers  
          .stream()  
          .map(Person::getLastName)  
          .collect(toCollection(TreeSet::new));  
* 双冒号就是把方法当作参数传递给需要的方法，或者说是传递到stream()中去。换句话说java8双冒号运算符就是方法引用。方法引用又包括实例方法、静态方法。语法格式类名：：方法名
* 双冒号运算操作符是类方法的句柄，lambda表达式的一种简写，这种简写的学名叫eta-conversion或者叫η-conversion
* 把 x -> System.out.println(x) 简化为 System.out::println 的过程称之为 eta-conversion
* person -> person.getAge();
可以替换成
Person::getAge
x -> System.out.println(x)
可以替换成
System.out::println
() -> new ArrayList<>();
可以替换为
ArrayList::new
* 带参数的代码块；函数式接口；访问final变量
* 可以向接口添加默认和静态方法来提供具体实现；将代码块到处传递
* 对象::实例方法，类::静态方法====》提供参数的lambda表达式；类::实例方法===》第一个参数会成为执行方法的对象
* 方法引用不会独立存在，经常被用于转换函数式接口的实例
* 如果只有一条语句，编译器会自动将值返回；如果多条的话，需要手动return
* 构造方法引用： 类::new

　　静态方法引用：类::静态方法

　　实例方法引用：类::实例方法  或者  对象::实例方法
* Instant——它代表的是时间戳；LocalDate——不包含具体时间的日期；LocalTime——它代表的是不含日期的时间；LocalDateTime——它包含了日期及时间，不过还是没有偏移信息或者说时区；ZonedDateTime——这是一个包含时区的完整的日期时间，偏移量是以UTC/格林威治时间为基准的
* java中判断是否是某个节日或者重复事件，使用MonthDay类；MonthDay.of  MonthDay.from
* localTime.plusHours(2)
* Clock.
