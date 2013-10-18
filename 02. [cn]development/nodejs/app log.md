
#### **记录的Log包括哪些**
1. Nginx Access log ： 使用ltsv格式输出，输出内容如下
 
 - 设定方法参见下面的 **Nginx ltsv log format**
  
 2. Nginx Error log : 使用默认的输出格式
  - Nginx 的错误日志不可以定制
  
 3. Application log（Nodejs）
  - 参见下面的日志输出内容
  
 4. Application log（Java）
  - 对log4j的输出，用tail进行收集
  - format : /^$/

            2013-10-16 09:59:52,093 DEBUG PropertiesConfiguration:588 - FileName set to server.properties
            2013-10-16 09:59:52,096 DEBUG ConfigurationUtils:449 - ConfigurationUtils.locate(): base is null, name is server.properties
            2013-10-16 09:59:52,096 DEBUG DefaultFileSystem:281 - Could not locate file server.properties at null: no protocol: server.properties

 5. DB log
  - format : /^(?<message>.*)$/
  
            Mon Sep 30 23:38:22.032 [signalProcessingThread] now exiting
            Mon Sep 30 23:38:22.032 dbexit:
            Mon Sep 30 23:38:22.032 [signalProcessingThread] shutdown: going to close listening sockets...

 6. LB log
  - 与Nginx使用相同的方法收集

 7. RabbitMQ log
  - 使用tail-multiline，对象log为/var/log/rabbitmq/rabbit@localhost.log
  - https://github.com/tomohisaota/fluent-plugin-tail-multiline
  - format : /=(?<type>.*)====(?<time>\d{2}-\s{3}-\d{4}::\d{1,2}:\d{1,2}:\d{1,2})===(?<message>.*)/

            =INFO REPORT==== 15-Oct-2013::20:50:54 ===
            accepting AMQP connection <0.6610.9> (10.2.3.49:58897 -> 10.2.8.232:5672)
    
 8. Varnish log
  - 为了减少写日志的开销，varnish把日志缓冲到内存中。
  - 可以通过varnishncsa, varnishlog, varnishstat等命令来查看。
  - 对于varnish，我们不搜集日志，而是用zabbix来监视其工作状态（缓冲状态等）。

 9. OS log
  - 对象日志文件为 /var/log/messages
 
 10. Fluent log
  
----
#### **什么样的事件需记录，记录什么内容**

 - 记录情报内容包括 : Who, What, When, Where, Why, How
  1.  安全：登陆，登陆失败，注销，创建用户，无访问权限，改变权限 等和安全相关的操作使用auit输出
  2.  操作：route方法中的request开始和结束，api中的开始和结束，用operation输出
  3.  追踪：数据库的增删改操作，统一用application的debug输出
  4.  追踪：异步（文件操作，MQ发信等）调用时，用debug输出相关信息
  5.  其他：根据需要，在程序当中输出日志

 - format
  1. time: 日志输出时间
  2. user: user id
  3. host: ip
  4. type: 参看下面的说明
  5. level: 参看下面的说明
  6. category: 分类，多个时用逗号分隔（未使用）
  7. code: 信息编号，一般和错误信息相对应（未使用）
  8. message: 信息
  9. file: 输出日志的代码文件
  10. line: 输出日志的行数

 - type
  1. audit : 登陆，登陆失败，注销，创建用户，无访问权限，改变权限 等和安全相关的内容使用该type
  2. operation : route方法中的request开始和结束，api中的开始和结束，来描述用户做的操作
  3. application : 1和2以外。

 - level : Nginx的日志分8种，我们支持其中的debug, info, warn, error
  1. emerg
  2. alert
  3. crit
  4. error : 异常信息
  5. warn : 警告信息
  6. notice
  7. info : 一般情报信息
  8. debug : 调试用详细信息

----
#### **记录在什么地方**
  - 文件：为了保证日志系统异常时，仍能够正常运行，所有的日志默认都输出到文件中。
  - DB：经Fluentd处理，将日志内容收集到数据库中。
   - 考虑 Capped
   - http://semind.github.io/blog/2012/03/16/mongodb-cappedkorekusiyonwoshi-su/

#### 确保log的安全
 - 与安全方面的内容一起考虑

#### 同步多台服务器的时间
 - 使用NTP对服务器之间的时间进行同步，NTP无法保证时间顺序完全一致，
 - 所以AP分散时，输出的log顺序有可能会乱

----
#### 需求，目的
 - 容易监视，包括第三方监视软件，包括错误详细等
 - Dev与Ops的交互手段
  - 当发生事件时能够根据log判断错误的原因
  - 调整中间件的参数，或修改程序
  - 不需要使用tcpdump，GDB，strace等工具，等到错误重新出现
 - 对数据操作的追中监视
 - 发现错误
 - 确认正常运转

----
#### Log的管理
> rotation
  
  - 所有的log，都进行日次的rotation。
  - mongodb log rotate
 
        use admin
        db.runCommand( { logRotate : 1 } )

> zip
  - 由于日志内容都保存到DB中，所以不显示的对过去的日志做压缩处理

> online log, offline log (backup), remove log
  - 文件日志保存期限为1个月
  - DB中的日志，暂定不删除（先观察一段时间再调整）

----
#### Fluentd logging : 解决日志系统中的课题, 及作用

 - 课题
 1. log种类繁多
 1. 生成log到能参照，需要的时间长
 1. log没能被活用

 - 作用
 1. filter
 1. buffer
 1. routing

#### fluentd安装

> 安装

    # curl -L http://toolbelt.treasure-data.com/sh/install-redhat.sh | sh

> 改变待监视文件的权限

    # chmod o+rx /var/log/httpd

#### fluentd设定

> OS log的转发

	<source>
	  type config_expander
	  <config>
	    type tail
	    format syslog
	    pos_file /tmp/syslog.pos
	    path /var/log/messages
	    tag ${hostname}/syslog.messages
	  </config>
	</source>

> Nginx log的转发（需要先将nginx的log格式进行转换）

    ## /etc/nginx/nginx.conf
    log_format  ltsv  'time:$time_iso8601\t'
        'msec:$msec\t'
        'host:$remote_addr\t'
        'forwardedfor:$http_x_forwarded_for\t'
        'req:$request\t'
        'method:$request_method\t'
        'uri:$request_uri\t'
        'status:$status\t'
        'size:$body_bytes_sent\t'
        'referer:$http_referer\t'
        'ua:$http_user_agent\t'
        'reqtime:$request_time\t'
        'upsttime:$upstream_response_time\t'
        'cache:$upstream_http_x_cache\t'
        'runtime:$upstream_http_x_runtime\t'
        'vhost:$host';

    <source>
      tag nginx.access
      type tail
      path /var/log/nginx/access.log
      format ltsv
      pos_file /var/log/td-agent/nginx_access.pos
    </source>
    
    <source>
      tag nginx.error
      type tail
      path /var/log/nginx/error.log
      format /^(?<time>.+) \[(?<level>[^\]]+)\] *(?<message>.*)$/
      time_format %Y/%m/%d %H:%M:%S
      pos_file /var/log/td-agent/nginx_error.pos
    </source>

> 将日志内容保存到Mongodb中

    <match apache.access>
      type mongo
      database httpd
      collection accesslog
      host localhost
      port 27017
      flush_interval 10s
    </match>
    <match apache.error>
      type mongo
      database httpd
      collection accesslog
      host localhost
      port 27017
      flush_interval 10s
    </match>

#### 分析插件

 - GrowthForecast

#### 参考
https://logentries.com/product/features/





