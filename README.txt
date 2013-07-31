如何正确地编译taokeeper：
1.下载这两个项目：
  git clone https://github.com/hengyunabc/common-toolkit.git
  git clone https://github.com/nileader/zkclient.git
  
  先分别执行 mvn -Dmaven.test.skip install
2.下载本项目：
  git clone https://github.com/hengyunabc/taokeeper.git
  
  执行  mvn -Dmaven.test.skip clean package
  到taokeeper-monitor/target/目录就可以看到生成的War包了。
  
3.部署：
  原项目的部署说明有问题。
  要有mysql数据库，导入taokeeper-build/etc/taokeeper.sql 文件；
  配置tomcat启动参数，增加JVM启动参数：
  JAVA_OPTS=-DconfigFilePath="~/taokeeper/taokeeper-monitor-config.properties"
  并在上面的配置中配置好参数，例如：
	systemInfo.envName=TEST
	#DBCP
	dbcp.driverClassName=com.mysql.jdbc.Driver
	dbcp.dbJDBCUrl=jdbc:mysql://localhost:3306/taokeeper
	dbcp.characterEncoding=GBK
	dbcp.username=root
	dbcp.password=root
	dbcp.maxActive=30
	dbcp.maxIdle=10
	dbcp.maxWait=10000
	#SystemConstant
	SystemConstent.dataStoreBasePath=~/taokeeper/
	#SSH account of zk server
	SystemConstant.userNameOfSSH=hello
	SystemConstant.passwordOfSSH=hello

  其中SSH用户密码要配置对，zookeeper部署的机器要开放SSH服务。
  把生成的War包改为ROOT.war，放到tomcat的webapps目录下，启动tomcat。
  如果报log4j错误，则还要配置webapps/ROOT/WEB-INF/classes/log4j.properties 文件。
  也可以在编绎前先修改好。
  
  打开 http://localhost:8080/ ，就可以看到taokeeper的界面了。
 
4.注意
  在chrome浏览器下，“机器监控”这个功能有时会把信息显示下浏览器的下面，要拉到最后才能看到，并不是这个功能不能工作。
  

================下面的配置已过时，可以参考========================
	

Notice:The file is encoded by UTF-8

HomePage: http://jm.taobao.org/2012/01/12/zookeeper%E7%9B%91%E6%8E%A7/
CopyRight by Taobao.com
Any question to: nileader@qq.com
   
   
1. Use To manage projects dependence using maven
2. Database Initialization: taokeeper-build/sql/taokeeper.sql
3. Implements com.taobao.taokeeper.reporter.alarm.MessageSender to send message.
4. Exec taokeeper-build/build.cmd to generate taokeeper-monitor.war


How to deploy(See more,please to http://jm.taobao.org/2012/01/12/zookeeper%E7%9B%91%E6%8E%A7/ )

1. Download taokeeper.sql( http://pan.baidu.com/share/link?shareid=515952&uk=2064399439 ),init mysql.

2. Download taokeeper-monitor.tar.gz ( http://pan.baidu.com/share/link?shareid=515943&uk=2064399439 ), 
    tar -zxvf taokeeper-monitor.tar.gz  to webapps of tomcat, 
    make sure the path is %TOMCAT_HOME%\webapps\taokeeper-monitor\WEB-INF

3. Download taokeeper-monitor-config.properties http://pan.baidu.com/share/link?shareid=515942&uk=2064399439 ), 
    store it such as /home/admin/taokeeper-monitor/config/taokeeper-monitor-config.properties

----------------------------------------------------------------
systemInfo.envName=TEST
#DBCP
dbcp.driverClassName=com.mysql.jdbc.Driver
dbcp.dbJDBCUrl=jdbc:mysql://1.1.1.1:3306/taokeeper
dbcp.characterEncoding=GBK
dbcp.username=xiaoming
dbcp.password=123456
dbcp.maxActive=30
dbcp.maxIdle=10
dbcp.maxWait=10000
#SystemConstant
SystemConstent.dataStoreBasePath=/home/xiaoming/taokeeper-monitor/ZookeeperStore
#SSH account of zk server
SystemConstant.userNameOfSSH=xiaoming
SystemConstant.passwordOfSSH=123456
------------------------------------------------------------------

4. Add JAVA_OPTS to tomcat catalina.bat or catalina.sh:
windows：set JAVA_OPTS=-DconfigFilePath="D:\server\tomcat-6.0.33\webapps\taokeeper-monitor-config.properties"
linux：JAVA_OPTS=-DconfigFilePath="/home/admin/taokeeper-monitor/config/taokeeper-monitor-config.properties"

5. Startup tomcat

6. Visit the page: http://127.0.0.1:8080/taokeeper-monitor
         
         
         
         
         
Alibaba OpenSource Maven Repository  
	<profiles>
		<profile>
			<id>opensource</id>
			<repositories>
				<repository>
					<id>taocodeReleases</id>
					<name>taocode nexus</name>
					<url>http://mvnrepo.code.taobao.org/nexus/content/repositories/releases/</url>
				</repository>
				<repository>
					<id>taocodeSnapshots</id>
					<name>taocode nexus</name>
					<url>http://mvnrepo.code.taobao.org/nexus/content/repositories/snapshots/</url>
				</repository>
			</repositories>
		</profile>
	</profiles>

        
