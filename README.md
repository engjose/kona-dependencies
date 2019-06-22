### 万物之源
在企业级开发中我们我们做一个项目首先需要去搭建项目结构, 有了良好的项目结构我们才能更快速, 更舒畅的搞开发,所以对于kona 的第一篇我们来研究微服务架构下的项目结构. 当然我们的服务是基于springboot2.x搭建的, 后续会使用springcloud生态

### 1.基础依赖---kona-dependencies
1. 现在企业级项目大多数java项目都是基于maven管理的. 利用maven帮助我们管理jar包依赖, 构建项目. 说到jar包依赖, 我们首先做的第一件事情就是需要将企业中一个项目组乃至整个部门使用的jar包集中管理, 这里我们创建一个kona-dependencies项目, 这个项目的作用是管理我们的jar包依赖, 是所有项目的父项目. 这样的话我们之后创建的每一个服务继承这个顶层父项目就可以了

2. [kona-dependencies](https://github.com/engjose/kona-dependencies.git)

3. kona-dependencies 项目很简单,它仅仅是一个pom工程, 这里有几点需要注意一下:
* kona-dependencies 项目的坐标: packaging: pom, 表明是一个pom工程
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
至此我们顶层项目依赖已经搭建完毕, 具体的项目大家可以克隆2 中对应的项目

