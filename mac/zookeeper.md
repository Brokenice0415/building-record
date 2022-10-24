## Package and Run
```shell
# 复制并修改config
# 其中dataDir需要确实存在
# 确保有读写权限（chmod）
> cp conf/zoo_sample.cfg conf/zoo.cfg

# 打包
# 跳过测试（费时间且有个会失败）
> mvn clean package -DskipTests

# 运行zookeeper server
> bash bin/zkServer.sh start

# 如果失败可以通过下面指令查看函数栈
# > bash bin/zkServer.sh start-foreground

# 运行zookeeper client
> bash bin/zkCli.sh
```

### ERROR WHEN PACKAGING

1. java.lang.ClassNotFoundException:org.apache.zookeeper.server.quorum.QuorumPeerMain

    在运行zkServer.sh前需要先通过mvn打包

2. java.lang.NoClassDefFoundError:org/slf4j/LoggerFactory

    依赖缺失
    
    解决：在pom.xml添加如下依赖
    
    ```xml
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.17</version>
      </dependency>
      <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.7.7</version>
      </dependency>
      <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-log4j12</artifactId>
        <version>1.7.7</version>
      </dependency>
    ```