logback
---

<?xml version="1.0" encoding="UTF-8"?>
<configuration scan="true">
    <property resource="log/logback.properties"/>
    <!-- 控制台日志配置 -->
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <layout class="ch.qos.logback.classic.PatternLayout">
            <pattern>%d{yyyy-MM-dd HH:mm:ss} [%p] [%t] %c{50}:%L - %m%n</pattern>
        </layout>
    </appender>
    <!-- info级别日志控制 -->
    <appender name="FILE_INFO" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>${logback.path}/info.log</file>
        <append>true</append>
        <rollingPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">
            <fileNamePattern>${logback.zip.path}/%d{yyyy-MM-dd}/info/info-%i.zip</fileNamePattern>
            <maxFileSize>${logback.maxFileSize}</maxFileSize>
            <maxHistory>${logback.maxHistory}</maxHistory>
            <totalSizeCap>${logback.totalSizeCap}</totalSizeCap>
        </rollingPolicy>
        <layout class="ch.qos.logback.classic.PatternLayout">
            <pattern>%d{yyyy-MM-dd HH:mm:ss} [%p] [%t] %c{50}:%L - %m%n</pattern>
        </layout>
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>INFO</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>
    <!-- warn级别日志控制 -->
    <appender name="WARN_INFO" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>${logback.path}/warn.log</file>
        <append>true</append>
        <rollingPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">
            <fileNamePattern>${logback.zip.path}/%d{yyyy-MM-dd}/warn/warn-%i.zip</fileNamePattern>
            <maxFileSize>${logback.maxFileSize}</maxFileSize>
            <maxHistory>${logback.maxHistory}</maxHistory>
            <totalSizeCap>${logback.totalSizeCap}</totalSizeCap>
        </rollingPolicy>
        <layout class="ch.qos.logback.classic.PatternLayout">
            <pattern>%d{yyyy-MM-dd HH:mm:ss} [%p] [%t] %c{50}:%L - %m%n</pattern>
        </layout>
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>WARN</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>
    <!-- ERROR级别日志控制 -->
    <appender name="ERROR_INFO" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>${logback.path}/error.log</file>
        <append>true</append>
        <rollingPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">
            <fileNamePattern>${logback.zip.path}/%d{yyyy-MM-dd}/error/error-%i.zip</fileNamePattern>
            <maxFileSize>${logback.maxFileSize}</maxFileSize>
            <maxHistory>${logback.maxHistory}</maxHistory>
            <totalSizeCap>${logback.totalSizeCap}</totalSizeCap>
        </rollingPolicy>
        <layout class="ch.qos.logback.classic.PatternLayout">
            <pattern>%d{yyyy-MM-dd HH:mm:ss} [%p] [%t] %c{50}:%L - %m%n</pattern>
        </layout>
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>ERROR</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>

    <!-- 开发环境 -->
    <springProfile name="dev">
        <root level="INFO">
            <appender-ref ref="CONSOLE"/>
        </root>
    </springProfile>
    <!-- 测试环境 -->
    <springProfile name="test">
        <root level="INFO">
            <appender-ref ref="CONSOLE"/>
            <appender-ref ref="FILE_INFO"/>
            <appender-ref ref="WARN_INFO"/>
            <appender-ref ref="ERROR_INFO"/>
        </root>
    </springProfile>
    <!-- 生产环境 -->
    <springProfile name="prod">
        <root level="INFO">
            <appender-ref ref="CONSOLE"/>
            <appender-ref ref="FILE_INFO"/>
            <appender-ref ref="WARN_INFO"/>
            <appender-ref ref="ERROR_INFO"/>
        </root>
    </springProfile>

</configuration>
