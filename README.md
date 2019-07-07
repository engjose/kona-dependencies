# 简要说明
1. kona-dependencies是最顶层的依赖父项目, 目的帮助我们统一管理jar包

2. 做几点说明:
* kona-dependencies 项目的坐标具体如下, 其中packaging: pom, 表明是一个pom工程
```
    <groupId>com.kona</groupId>
    <artifactId>kona-dependencies</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>pom</packaging>
```
* 我们在<dependencyManagement>中引入引入了springboot 和springcloud的pom, scop类型是import, 因为pom parent是只能指定一个, 我们这里指定为import时会引入其版本管理
```
<dependencyManagement>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>${spring.boot.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${springcloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
...
</dependencyManagement>
```
* 因为我们这里需要将工程push到自己的私服, 所以配置了<distributionManagement>, 具体实际应用中可以配置自己公司的私服
```
    <!-- 分发管理: 自己私服配置 -->
    <distributionManagement>
        <repository>
            <id>${distribution.releases.id}</id>
            <url>${distribution.releases.url}</url>
        </repository>
        <snapshotRepository>
            <id>${distribution.snapshots.id}</id>
            <url>${distribution.snapshots.url}</url>
        </snapshotRepository>
    </distributionManagement>
```
    
# 如何使用
我们只需要将此项目clone 下来上传到自己的私服或者修改适合自己项目的版本依赖, 其中私服地址修改如下配置:
```xml
    <!-- 分发管理: 自己私服配置 -->
    <distributionManagement>
        <repository>
            <id>${distribution.releases.id}</id>
            <url>${distribution.releases.url}</url>
        </repository>
        <snapshotRepository>
            <id>${distribution.snapshots.id}</id>
            <url>${distribution.snapshots.url}</url>
        </snapshotRepository>
    </distributionManagement>
```

