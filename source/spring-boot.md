* 可以部署Spring Boot项目到任何兼容Servlet3.0+的容器
* spring-boot-starter-parent 是一个非常好的方法，但并不适用于所有情况。有时你需要继承其他的POM，或者你不喜欢默认的设置
* spring-boot-starter-parent 又提供了 dependency-management ，所以我们可以忽略被选中依赖的版本
* spring-boot-starter-web  包含了很多内容，spring-webmvc、spring-web、jackson、validation、tomcat、starter
* 注意，spring-boot-starter-parent POM中包含了 <executions> 的配置信息，绑定了 repackage goal （maven）。如果你不使用parent POM，你需要自己来声明这个配置信息
* 继承 spring-boot-starter-parent ：      spring-boot-starter-parent project       默认是 Java 1.6。
* 如果不想使用Spring Boot中的默认版本，可以在<properties>覆盖相应的版本，如，想使用不同版本的Spring Data :: <java.version>1.8</java.version>
* 不继承 spring-boot-starter-parent,仍然可以使用dependency management，但不能使用plugin management啦:
<dependencyManagement>
    <dependencies>
        <!-- Override Spring Data release train provided by Spring Boot -->
        <dependency>
            <groupId>org.springframework.data</groupId>
            <artifactId>spring-data-releasetrain</artifactId>
            <version>Fowler-SR2</version>
            <scope>import</scope>
            <type>pom</type>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>1.4.0.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
* 注意，scope是 import 。而且，这种情况下，不再允许在<properties>覆盖相应的版本。如果要使用其他版本，需要在上面的前面添加一个完整的dependency
* 可以创建自己的Starter，但名字格式不能是 spring-boot-starter-*，而是 *-spring-boot-starter。类似Maven插件的规则
* 查看自动配置都配置了什么，以及为什么，启动应用的时候加上 --debug即可
* java -Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=8000,suspend=n -jar target/myproject-0.0.1-SNAPSHOT.jar
* 注意，不同的IDE有不同的表现，例如Eclipse中只要改变了文件并保存，那就会导致classpath中的内容改变。而Intellij IDEA则需要 Build #Make Project。
可以通过build plugin启动应用，只要开启了forking支持，因为Devtools需要一个隔离的classloader才能运行正常。Maven下要这样开启
* <build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <fork>true</fork>
            </configuration>
        </plugin>
    </plugins>
</build>
