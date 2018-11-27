### maven自定义插件开发
* 一般来说，我们会将自己的插件命名为 -maven-plugin
* Mojo 就是 Maven plain Old Java Object。每一个 Mojo 就是 Maven 中的一个执行目标（executable goal），而插件则是对单个或多个相关的 Mojo 做统一分发。一个 Mojo 包含一个简单的 Java 类。插件中多个类似 Mojo 的通用之处可以使用抽象父类来封装
* 使用 Idea 作为开发工具进行讲解，创建工程选择 Maven，然后在模板中找到 maven-archetype-mojo，点击下一步，输入对应的参数，如：com.qchery/ekjar-maven-plugin/1.0-SNAPSHOT，最后点击完成即可创建一个简单的 Mojo 工程
*
/**
 * @goal hello
 */
ublic class HelloMojo extends AbstractMojo
@Mojo(name = "hello")
public class HelloMojo extends AbstractMojo
mvn com.qchery:ekjar-maven-plugin:1.0-SNAPSHOT:hello
如果你想要执行的是你本地库中最新版本的插件，那么你可以删除掉版本号；如果你的命名满足前面提及的两种命令方式，你可以直接使用插件名及 goal 名来运行对应的插件
mvn ekjar:hello
* plugin-tools 会把使用了 @Mojo 注解或 Javadoc 里包含 @goal 注释的类来当作一个 Mojo 类；使用 @Mojo 注解，我们需要引入一个新包
<dependency>
  <groupId>org.apache.maven.plugin-tools</groupId>
  <artifactId>maven-plugin-annotations</artifactId>
  <version>3.1</version>
</dependency>
* 还可以将插件配置为将特定目标，从而附加到构建生命周期中的某个特定阶段
<plugin>
    <groupId>com.qchery</groupId>
    <artifactId>ekjar-maven-plugin</artifactId>
    <version>1.0-SNAPSHOT</version>
    <executions>
        <execution>
            <goals>
                <goal>hello</goal>
            </goals>
            <phase>package</phase>
        </execution>
    </executions>
</plugin>
* 继承AbstractMojo 的类中，参数可以通过命令赋值
/**
 *
 * @goal echo
 * @phase process-sources
 */
public class MyMojo extends AbstractMojo {

    /**
     * @parameter expression="${echo.message}" default-value="Hello World..."
     */
    private String message;

    public void execute() throws MojoExecutionException, MojoFailureException {
        System.out.println("hello world");

        getLog().info("hello mymojo : "+message);
    }

}
* 注释就是maven插件很重要的元数据
/**
 * @goal CustomMavenMojo：表示该插件的服务目标
 * @phase compile：表示该插件的生效周期阶段
 * @requiresProject false：表示是否依托于一个项目才能运行该插件
 * @parameter expression="${name}"：表示插件参数，使用插件的时候会用得到
 * @required:代表该参数不能省略
 */
 * mvn com.handarui.yanquan:yanquan:1.0-SNAPSHOT:echo -Decho.message="The Eagle has Landed"
 * swagger项目中的codegen自动生成代码
 * 如果一个工程想通过mvn groupId:artifactId:version:goal形式的命令调用my-maven-plugin；；只需将my-maven-plugin发布到远程仓库或装载到本地仓库，那么在该工程中，不需要在pom的plugins属性中引入对my-maven-plugin的依赖，即可直接通过mvn myplugin:my-maven-plugin:1.0:goaltest命令进行调用
 * 如果一个工程想通过mvn goalPrefix:goal别名形式的命令调用my-maven-plugin
 1. 必须通过Maven Plugin Plugin指定my-maven-plugin的别名即goalPrefix(假设指定别名为my)，并且在该工程pom的plugins属性中引入对my-maven-plugin的依赖，即可通过mvn my:goaltest的形式进行调用
 2. plugin的artifactId满足***-maven-plugin或maven-***-plugin命名规范(如果满足命名规范，会自动生成别名***，本文中my-maven-plugin已满足命名规范，将会生成的别名为my)，或者同样通过Maven Plugin Plugin指定my-maven-plugin的别名即goalPrefix，做到以上两点，便可以在不需要依赖my-maven-plugin的情况下，直接在工程中通过mvn my:goaltest命令调用my-maven-plugin

---

# 命令
* mvn clean package -P product
* mvn -DpropA=valueA -DpropB=valueB -DpropC=valueC clean package

# 属性
* ${basedir}表示项目根目录,即包含pom.xml文件的目录
* ${version}表示项目版本
* ${project.basedir}同${basedir}
* ${project.baseUri}表示项目文件地址
* ${maven.build.timestamp}表示项目构件开始时间
* ${maven.build.timestamp.format}表示属性${maven.build.timestamp}的展示格式,默认值为yyyyMMdd-HHmm
<properties>
<maven.build.timestamp.format>yyyy-MM-dd HH:mm:ss</maven.build.timestamp.format>
</properties>
* ${project.build.directory}表示主源码路径，缺省为target
* ${project.build.outputDirectory} 构建过程输出目录，缺省为target/classes
* ${project.build.sourceEncoding}表示主源码的编码格式
* ${project.build.sourceDirectory}表示主源码路径
* ${project.build.finalName}表示输出文件名称，缺省为${project.artifactId}-${project.version}
* ${project.packaging} 打包类型，缺省为jar
* ${project.version}表示项目版本,与${version}相同
* ${settings.localRepository}表示本地仓库的地址
* ${user.home}表示用户目录
* ${env.JAVA_HOME}表示JAVA_HOME环境变量的值
* ${project.build.testSourceDirectory}:项目的测试源码目录，默认为/src/test/java/
* ${project.build.testOutputDirectory}:项目测试代码编译输出目录，默认为target/testclasses/
* ${project.build.sourceDirectory}:项目的主源码目录，默认为src/main/java/
* ${project.groupId}:项目的groupId
* ${project.artifactId}:项目的artifactId

# 资源过滤
* 默认情况下，Maven属性只有在POM中才会被解析。资源过滤就是指让Maven属性在资源文件(src/main/resources、src/test/resources)中也能被解析
资源文件过滤的意思是指我们可以在资源文件里用使用占位符${propertyName}，然后开启对资源文件的过滤，pom.xml里再统一设置所有{propertyName}对应的值
<build>  
    <resources>  
        <resource>  
            <directory>${project.basedir}/src/main/resources</directory>  
            <filtering>true</filtering>  
        </resource>  
    </resources>  
    <testResources>  
        <testResource>  
            <directory>${project.basedir}/src/test/resources</directory>  
            <filtering>true</filtering>  
        </testResource>  
    </testResources>  
</build>
* Maven除了可以对主资源目录、测试资源目录过滤外，还能对Web项目的资源目录(如css、js目录)进行过滤
<plugin>  
    <groupId>org.apache.maven.plugins</groupId>  
    <artifactId>maven-war-plugin</artifactId>  
    <version>2.1-beta-1</version>  
    <configuration>  
        <webResources>  
            <resource>  
                <filtering>true</filtering>  
                <directory>src/main/webapp</directory>  
                <includes>  
                    <include>**/*.css</include>  
                    <include>**/*.js</include>  
                </includes>  
            </resource>  
        </webResources>  
    </configuration>  
</plugin>

# profile
每个Profile可以看作是POM的一部分配置，我们可以根据不同的环境应用不同的Profile，从而达到不同环境使用不同的POM配置的目的
pom.xml：很显然，这里声明的profile只对当前项目有效
用户settings.xml：.m2/settings.xml中的profile对该用户的Maven项目有效
全局settings.xml：conf/settings.xml，对本机上所有Maven项目有效
* 激活Profile
mvn clean install  -Pdevx,devy

# jetty
<plugin>
    <groupId>org.eclipse.jetty</groupId>
    <artifactId>jetty-maven-plugin</artifactId>
    <version>9.4.5.v20170502</version>
    <configuration>
        <scanIntervalSeconds>10</scanIntervalSeconds>
        <httpConnector>
            <port>8080</port>
        </httpConnector>
        <webApp>
            <contextPath>/${project.build.finalName}</contextPath>
            <extraClasspath>
                ../ccms-common/target/classes;
                ../ccms-dao/target/classes;
                ../ccms-model/target/classes;
                ../ccms-service/ccms-inspection/target/classes;
                ../ccms-service/ccms-permission/target/classes;
                ../ccms-service/ccms-schedule/target/classes;
            </extraClasspath>
        </webApp>
    </configuration>
</plugin>
# compiler
<plugin>  
    <groupId>org.apache.maven.plugins</groupId>  
    <artifactId>maven-compiler-plugin</artifactId>  
    <configuration>  
        <source>1.8</source>  
        <target>1.8</target>  
        <encoding>UTF-8</encoding>  
    </configuration>  
</plugin>
# properties
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>properties-maven-plugin</artifactId>
    <version>1.0-alpha-2</version>
    <executions>
        <execution>
            <phase>initialize</phase>
            <goals>
                <goal>read-project-properties</goal>
            </goals>
            <configuration>
                <files>
                    <file>../../property/jdbc.properties</file>
                </files>
            </configuration>
        </execution>
    </executions>
</plugin>

# maven-resources-plugin
<plugin>  
    <groupId>org.apache.maven.plugins</groupId>  
    <artifactId>maven-resources-plugin</artifactId>  
    <version>2.4.3</version>  
    <executions>  
        <execution>  
            <phase>compile</phase>  
        </execution>  
    </executions>  
    <configuration>  
        <encoding>${project.build.sourceEncoding}</encoding>  
    </configuration>  
</plugin>
<plugin>  
    <groupId>org.apache.maven.plugins</groupId>  
    <artifactId>maven-resources-plugin</artifactId>  
    <version>2.5</version>  
    <executions>  
        <execution>  
            <id>deploy-website</id>  
            <phase>package</phase>  
            <goals>  
                <goal>copy-resources</goal>  
            </goals>  
            <configuration>  
                <outputDirectory>${server_home}/webapps/${project.build.finalName}</outputDirectory>  
                <resources>  
                    <resource>  
                        <directory>${project.build.directory}/${project.build.finalName}</directory>  
                    </resource>  
                </resources>  
            </configuration>  
        </execution>  
    </executions>  
</plugin> 

# maven-dependency-plugin
maven-dependency-plugin最大的用途是帮助分析项目依赖
dependency:list能够列出项目最终解析到的依赖列表
dependency:tree能进一步的描绘项目依赖树
dependency:analyze可以告诉你项目依赖潜在的问题
dependency:copy-dependencies能将项目依赖从本地Maven仓库复制到某个特定的文件夹下面
<plugin>  
    <groupId>org.apache.maven.plugins</groupId>  
    <artifactId>maven-dependency-plugin</artifactId>  
    <version>2.6</version>  
    <executions>  
        <execution>  
            <id>copy-dependencies</id>  
            <phase>compile</phase>  
            <goals>  
                <goal>copy-dependencies</goal>  
            </goals>  
            <configuration>  
                <!-- ${project.build.directory}为Maven内置变量，缺省为target -->  
                <outputDirectory>${project.build.directory}/lib</outputDirectory>  
                <!-- 表示是否不包含间接依赖的包 -->  
                <excludeTransitive>false</excludeTransitive>  
                <!-- 表示复制的jar文件去掉版本信息 -->  
                <stripVersion>true</stripVersion>  
            </configuration>  
        </execution>  
    </executions>  
</plugin>

# maven-source-plugin(生成源代码jar)
<plugin>  
    <artifactId>maven-source-plugin</artifactId>  
    <version>2.1</version>  
    <configuration>  
        <!-- <finalName>${project.build.name}</finalName> -->  
        <attach>true</attach>  
        <encoding>${project.build.sourceEncoding}</encoding>  
    </configuration>  
    <executions>  
        <execution>  
            <phase>compile</phase>  
            <goals>  
                <goal>jar</goal>  
            </goals>  
        </execution>  
    </executions>  
</plugin>

# maven-jar-plugin
<plugin>  
    <groupId>org.apache.maven.plugins</groupId>  
    <artifactId>maven-jar-plugin</artifactId>  
    <version>2.4</version>  
    <configuration>  
        <archive>  
            <manifest>  
                <!-- 告知 maven-jar-plugin添加一个 Class-Path元素到 MANIFEST.MF文件，以及在Class-Path元素中包括所有依赖项 -->  
                <addClasspath>true</addClasspath>  
                <!-- 所有的依赖项应该位于 lib文件夹 -->  
                <classpathPrefix>lib/</classpathPrefix>  
                <!-- 当用户使用 lib命令执行JAR文件时，使用该元素定义将要执行的类名 -->  
                <mainClass>com.zhengtian.tools.service.phone.MobilePhoneTool</mainClass>  
            </manifest>  
        </archive>  
    </configuration>  
</plugin>

# tomcat
<plugin>  
    <groupId>org.codehaus.mojo</groupId>  
    <artifactId>tomcat-maven-plugin</artifactId>  
    <configuration>  
        <server>tomcat6-manager</server>
        <path>/${project.build.name}</path>  
        <url>http://localhost:8080/manager</url>  
        <username>admin</username>  
        <password>admin</password>  
    </configuration>  
    <executions>  
        <execution>  
            <phase>deploy</phase>  
            <goals>  
                <goal>deploy</goal>  
            </goals>  
        </execution>  
    </executions>  
</plugin>

# cargo-maven2-plugin
<plugin>  
    <groupId>org.codehaus.cargo</groupId>  
    <artifactId>cargo-maven2-plugin</artifactId>  
    <version>1.2.0</version>  
    <configuration>  
        <container>  
            <containerId>${server_name}</containerId>  
            <home>${server_home}</home>  
        </container>  
        <configuration>  
            <type>existing</type>  
            <home>${server_home}</home>  
            <properties>  
                <cargo.servlet.port>8088</cargo.servlet.port>  
            </properties>  
        </configuration>  
    </configuration>  
</plugin>
<plugin>  
    <!-- 指定插件名称及版本号 -->  
    <groupId>org.codehaus.cargo</groupId>  
    <artifactId>cargo-maven2-plugin</artifactId>  
    <version>1.2.3</version>  
    <!-- 插件的Tomcat6.x配置 -->  
    <configuration>  
        <!-- 容器的配置 -->  
        <container>  
            <!-- 指定服务器版本 -->  
            <containerId>tomcat6x</containerId>  
            <!-- 指定服务器的安装目录 -->  
            <home>E:\Program Files\tomcat-6.0.32</home>  
        </container>  
        <!-- 具体的配置 -->  
        <configuration>  
            <!-- 部署模式：existing、standalone等 -->  
            <type>existing</type>  
            <!-- Tomcat的位置，即catalina.home -->  
            <home>E:\Program Files\tomcat-6.0.32</home>  
            <!-- 配置属性 -->  
            <properties>  
                <!-- 管理地址 -->  
                <cargo.tomcat.manager.url>http://localhost:8080/manager</cargo.tomcat.manager.url>  
                <!-- Tomcat用户名 -->  
                <cargo.remote.username>admin</cargo.remote.username>  
                <!-- Tomcat密码 -->  
                <cargo.remote.password>admin</cargo.remote.password>  
                <!-- <cargo.jvmargs> -Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=8787 </cargo.jvmargs> -->  
            </properties>  
        </configuration>  
    </configuration>  
</plugin>

# exec-maven-plugin
<plugin>  
  <groupId>org.codehaus.mojo</groupId>  
  <artifactId>exec-maven-plugin</artifactId>  
  <version>1.2.1</version>  
  <executions>  
    <execution>  
      <goals>  
        <goal>java</goal>  
      </goals>  
    </execution>  
  </executions>  
  <configuration>  
    <mainClass>com.yunzero.App</mainClass>  
  </configuration>  
</plugin>

# maven-assembly-plugin(支持定制化打包方式)
pom.xml文件里配置maven-assembly-plugin，指定描述文件
描述文件配置具体参数
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-assembly-plugin</artifactId>
    <configuration>
        <appendAssemblyId>false</appendAssemblyId>
        <descriptors>
            <descriptor>target/classes/package.xml</descriptor>
        </descriptors>
    </configuration>
    <executions>
        <execution>
            <id>make-assembly</id>
            <phase>package</phase>
            <goals>
                <goal>single</goal>
            </goals>
        </execution>
    </executions>
</plugin>

<assembly>
  <id>bin</id>
  <formats>
    <format>zip</format>
  </formats>
  <dependencySets>
    <dependencySet>
      <useProjectArtifact>true</useProjectArtifact>
      <outputDirectory>lib</outputDirectory>
    </dependencySet>
  </dependencySets>
  <fileSets>
    <fileSet>
      <outputDirectory>/</outputDirectory>
      <includes>
        <include>README.txt</include>
      </includes>
    </fileSet>
    <fileSet>
      <directory>src/main/scripts</directory>
      <outputDirectory>/bin</outputDirectory>
      <includes>
        <include>run.sh</include>
        <include>run.bat</include>
      </includes>
    </fileSet>
  </fileSets>
</assembly>

# versions-maven-plugin
当项目模块化后，我们会遇到一个问题，就是项目版本升级的时候，需要同时变更父模块和所有子模块中的版本号
mvn versions:set -DnewVersion=1.2-SNAPSHOT

# maven-shade-plugin(用来打可执行包)

# maven-enforcer-plugin
maven-enforcer-plugin能够帮助你避免之类问题，它允许你创建一系列规则强制大家遵守，包括设定Java版本、设定Maven版本、禁止某些依赖、禁止SNAPSHOT依赖
只要在一个父POM配置规则，然后让大家继承，当规则遭到破坏的时候，Maven就会报错

# maven-help-plugin
maven-help-plugin是一个小巧的辅助工具。
最简单的help:system可以打印所有可用的环境变量和Java系统属性
help:effective-pom和help:effective-settings最为有用，它们分别打印项目的有效POM和有效settings

# maven-release-plugin
lease-plugin的用途是帮助自动化项目版本发布
release:prepare用来准备版本发布，具体的工作包括检查是否有未提交代码、检查是否有SNAPSHOT依赖、升级项目的SNAPSHOT版本至RELEASE版本、为项目打标签

# maven-surefire-plugin
只要你的测试类遵循通用的命令约定（以Test结尾、以TestCase结尾、或者以Test开头），就几乎不用知晓该插件的存在。
mvn test -Dtest=FooTest 这样一条命令的效果是仅运行FooTest测试类
mvn package -Dmaven.test.skip=true
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-plugin</artifactId>
    <version>2.16</version>
    <configuration>
        <skip>true</skip>
        <forkMode>once</forkMode>
        <argLine>-Dfile.encoding=UTF-8</argLine>
</plugin>

最简单的help:system可以打印所有可用的环境变量和Java系统属性

# maven-javadoc-plugin
<plugin>          
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-javadoc-plugin</artifactId>
    <version>2.7</version>
    <executions>
      <execution>
        <id>attach-javadocs</id>
          <goals>
            <goal>jar</goal>
          </goals>
      </execution>
    </executions>
  </plugin>

# maven-clean-plugin
<plugin>  
    <artifactId>maven-clean-plugin</artifactId>  
    <configuration>  
        <verbose>true</verbose>  
        <filesets>  
            <fileset>  
                <directory>c:/a/b/c/</directory>  
            </fileset>  
      </filesets>  
    </configuration>  
</plugin>
