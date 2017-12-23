# frame4j
1. 日志对象（logger）
2. 设置输出位置（appender）- 控制台或文件
3. 设置输出样式（layout）
4. 　log4j日志等级的概念，log4j日志分为7个等级：ALL、DEBUG、INFO、WARN、ERROR、FATAL、OFF，从左到右等级由低到高
5. slf4j-log4j12这个包依赖了slf4j和log4j，所以使用slf4j+log4j的组合只要配置上面这一个依赖就够了
6. 局部日志：防止把所有地方的日专输出到同一个地方
	log4j.logger.com.demo.test=DEBUG,test
	log4j.appender.test=org.apache.log4j.FileAppender
	log4j.appender.test.File=/log/test.log
	log4j.appender.test.layout=org.apache.log4j.PatternLayout
	log4j.appender.test.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} [%p] %m%n
7. 日志样式：

#layout有4种选择
org.apache.log4j.HTMLLayout（以HTML表格形式布局）
org.apache.log4j.PatternLayout（可以灵活地指定布局模式）
org.apache.log4j.SimpleLayout（包含日志信息的级别和信息字符串）
org.apache.log4j.TTCCLayout（包含日志产生的时间、线程、类别等信息）

#设置格式的参数说明如下
%p：输出日志信息的优先级，即DEBUG，INFO，WARN，ERROR，FATAL
%d：输出日志时间点的日期或时间，默认格式为ISO8601，可以指定格式如：%d{yyyy/MM/dd HH:mm:ss,SSS}
%r：输出自应用程序启动到输出该log信息耗费的毫秒数
%t：输出产生该日志事件的线程名
%l：输出日志事件的发生位置，相当于%c.%M(%F:%L)的组合，包括类全名、方法、文件名以及在代码中的行数
%c：输出日志信息所属的类目，通常就是类全名
%M：输出产生日志信息的方法名
%F：输出日志消息产生时所在的文件名
%L：输出代码中的行号
%m：输出代码中指定的具体日志信息
%n：输出一个回车换行符，Windows平台为"rn"，Unix平台为"n"
%x：输出和当前线程相关联的NDC(嵌套诊断环境)
%%：输出一个"%"字符

log4j.rootLogger=DEBUG,console,dailyFile,rollingFile,logFile
log4j.additivity.org.apache=true

# 控制台(console)
log4j.appender.console=org.apache.log4j.ConsoleAppender
log4j.appender.console.Threshold=DEBUG
log4j.appender.console.ImmediateFlush=true
log4j.appender.console.Target=System.err
log4j.appender.console.layout=org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} [%p] %m%n

# 日志文件(logFile)
log4j.appender.logFile=org.apache.log4j.FileAppender
log4j.appender.logFile.Threshold=DEBUG
log4j.appender.logFile.ImmediateFlush=true
log4j.appender.logFile.Append=true
log4j.appender.logFile.File=D:/logs/log.log4j
log4j.appender.logFile.layout=org.apache.log4j.PatternLayout
log4j.appender.logFile.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} [%p] %m%n

# 滚动文件(rollingFile)
log4j.appender.rollingFile=org.apache.log4j.RollingFileAppender
log4j.appender.rollingFile.Threshold=DEBUG
log4j.appender.rollingFile.ImmediateFlush=true
log4j.appender.rollingFile.Append=true
log4j.appender.rollingFile.File=D:/logs/log.log4j
log4j.appender.rollingFile.MaxFileSize=200KB
log4j.appender.rollingFile.MaxBackupIndex=50
log4j.appender.rollingFile.layout=org.apache.log4j.PatternLayout
log4j.appender.rollingFile.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} [%p] %m%n

# 定期滚动日志文件(dailyFile)
log4j.appender.dailyFile=org.apache.log4j.DailyRollingFileAppender
log4j.appender.dailyFile.Threshold=DEBUG
log4j.appender.dailyFile.ImmediateFlush=true
log4j.appender.dailyFile.Append=true
log4j.appender.dailyFile.File=D:/logs/log.log4j
log4j.appender.dailyFile.DatePattern='.'yyyy-MM-dd
log4j.appender.dailyFile.layout=org.apache.log4j.PatternLayout
log4j.appender.dailyFile.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss} [%p] %m%n