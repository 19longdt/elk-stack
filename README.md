⚙️Config Elastic stack set passwords auto
<br>
-------------
**1.** open /bin in docker container: **cd /usr/share/elasticsearch/bin/**

**2.** insert query **elasticsearch-setup-passwords auto** -> **save result** to your notepad

**3.** add **username/password** from elastic, logstash, filebeat, kibana to **files config**

🌱 Spring Boot config file **logback-spring.xml**  send logs to Logstash (TCP 5044)
<br>
-------------
Add dependencies:
```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-logging</artifactId>
</dependency>
<dependency>
	<groupId>net.logstash.logback</groupId>
	<artifactId>logstash-logback-encoder</artifactId>
</dependency>
```

Beacause you have so many application services, you must config **customFields** with **app_name** label
```xml
<appender name="logstash" class="net.logstash.logback.appender.LogstashTcpSocketAppender">
	<param name="Encoding" value="UTF-8"/>
	<destination>{YOUR_HOST}:5044</destination>
	<encoder class="net.logstash.logback.encoder.LogstashEncoder">
		<customFields>{"app_name":"{YOUR_APP_SERVICE_NAME}"}</customFields>
	</encoder>
</appender>
<root level="INFO">
	<appender-ref ref="logstash" />
</root>
```

💡 **Note**: Options config to Kibana Dev Tool
<br>
-------------
**1.** Config Lifecycle policy to indexes

&nbsp;  PUT mqtt-data**/_settings 
  ```json
  {
    "index": {
      "lifecycle": {
        "name": "Clean-data"
      }
    }
  }
  ```

&nbsp;  **mqtt-data**** : Regular expression to map all your indexes

&nbsp;  **Clean-data** : the name of Lifecycle policy
