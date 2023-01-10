
# zookeeper和kafka的安全认证机制SASL
	https://developer.aliyun.com/article/708449

	七、zookeeper和kafka的安全认证机制SASL

	zookeeper在生产环境中，如果不是只在内网开放的话，就需要设置安全认证，可以选择SASL的安全认证。以下是和kafka的联合配置，如果不需要kafka可以去掉kafka相关的权限即可，以下基于zk3.5.5和kafka2.12进行操作。
	下面就是详细的部署步骤：

## 7.1 zookeeper的安全认证配置

	zookeeper所有节点都是对等的，只是各个节点角色可能不相同。以下步骤所有的节点配置相同。

	1、导入kafka的相关jar
	从kafka/lib目录下复制以下几个jar包到zookeeper的lib目录下：

	kafka-clients-2.3.0.jar
	lz4-java-1.6.0.jar
	slf4j-api-1.7.25.jar
	slf4j-log4j12-1.7.25.jar
	snappy-java-1.1.7.3.jar

	2、zoo.cfg文件配置
	添加如下配置：


	authProvider.1=org.apache.zookeeper.server.auth.SASLAuthenticationProvider
	requireClientAuthScheme=sasl
	jaasLoginRenew=3600000

	3、编写JAAS文件，zk_server_jaas.conf，放置在conf目录下
	这个文件定义需要链接到Zookeeper服务器的用户名和密码。JAAS配置节默认为Server：

	Server {
	org.apache.kafka.common.security.plain.PlainLoginModule required 
		username="admin" 
		password="admin-2019" 
		user_kafka="kafka-2019" 
		user_producer="prod-2019";
	};

	这个文件中定义了两个用户，一个是kafka，一个是producer，这些用user_配置出来的用户都可以提供给生产者程序和消费者程序认证使用。还有两个属性，username和password，其中username是配置Zookeeper节点之间内部认证的用户名，password是对应的密码。

	4、修改zkEnv.sh
	在zkEnv.sh添加以下内容，路径按你直接的实际路径来填写：

	export SERVER_JVMFLAGS=" -Djava.security.auth.login.config=/mnt/tools/zookeeper/apache-zookeeper-3.5.5/conf/zk_server_jaas.conf "

	5、在各个节点分别执行bin/zkServer.sh start启动zk。如果启动异常查看日志排查问题。

## 7.2 kafka的安全认证配置

	zookeeper启动之后，就配置kafka,下面步骤的配置在所有节点上都相同。

	1、在kafka的config目录下，新建kafka_server_jaas.conf文件，内容如下：

	KafkaServer {
		org.apache.kafka.common.security.plain.PlainLoginModule required
		username="admin"
		password="admin-2019"
		user_admin="admin-2019"
		user_producer="prod-2019"
		user_consumer="cons-2019";
	};

	Client {
	org.apache.kafka.common.security.plain.PlainLoginModule required
		username="kafka"
		password="kafka-2019";
	};

	KafkaServer配置的是kafka的账号和密码，Client配置节主要配置了broker到Zookeeper的链接用户名密码，这里要和前面zookeeper配置中的zk_server_jaas.conf中user_kafka的账号和密码相同。

	2、配置server.properties，同样的在config目录下

	listeners=SASL_PLAINTEXT://0.0.0.0:9092
	advertised.listeners=SASL_PLAINTEXT://node1:9092
	security.inter.broker.protocol=SASL_PLAINTEXT  
	sasl.enabled.mechanisms=PLAIN  
	sasl.mechanism.inter.broker.protocol=PLAIN  
	authorizer.class.name=kafka.security.auth.SimpleAclAuthorizer
	allow.everyone.if.no.acl.found=true

	这里注意listeners配置项，将主机名部分（本例主机名是node1）替换成当前节点的主机名。其他在各个节点的配置一致。注意，allow.everyone.if.no.acl.found这个配置项默认是false，若不配置成true，后续生产者、消费者无法正常使用Kafka。

	3、在server启动脚本JVM参数,在bin目录下的kafka-server-start.sh中，将

	export KAFKA_HEAP_OPTS="-Xmx1G -Xms1G"

	这一行修改为

	export KAFKA_HEAP_OPTS="-Xmx1G -Xms1G -Djava.security.auth.login.config=/mnt/tools/kafka/kafka_2.12/config/kafka_server_jaas.conf"

	4、配置其他节点
	配置剩余的kafka broker节点，注意server.properties的listeners配置项

	5.启动各个节点的kafka服务端，在bin目录下执行

	./kafka-server-start.sh ../config/server.properties


# 配置filebeat
	http://rk700.github.io/2016/12/16/filebeat-kafka-logstash-authentication-authorization/
	
## 配置filebeat

	filebeat支持output到kafka，而且可以设置使用SASL/PLAIN进行认证，只需要在文件filebeat.yml中填入以下内容即可：

	output.kafka:
	hosts: ["127.0.0.1:9092"]
	topic: '%{[type]}'
	username: "producer"
	password: "producer"

	上述各项的具体含义很明确，如果有疑问可以参考文档。
