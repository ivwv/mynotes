# 1.MAVEN 环境变量配置

#### (1).配置 JDK 系统变量

​ JAVA_HOME -> jdk 的根目录![1645614381110](../mdBeforeImg/\1645614381110.png)

#### (2).配置环境变量

​ ![1645614474483](../mdBeforeImg/\1645614474483.png)

#### (3).下载 MAVEN

![1645614582646](../mdBeforeImg/\1645614582646.png)

#### (4).配置 MAVEN 环境

​ 系统变量 ![1645614641090](../mdBeforeImg/\1645614641090.png)

![1645614667765](../mdBeforeImg/\1645614667765.png)

​ 环境变量

​ ![1645614712394](../mdBeforeImg/\1645614712394.png)

#### (5).配置 settings.xml

```bash
apache-maven-3.8.4\conf\settings.xml
```

​ 配置.m2 路径

![1645615015829](../mdBeforeImg/\1645615015829.png)

配置阿里云镜像

![1645615061798](../mdBeforeImg/\1645615061798.png)

```bash
<mirror>
      <id>aliyunmaven</id>
      <mirrorOf>*</mirrorOf>
      <name>阿里云公共仓库</name>
      <url>https://maven.aliyun.com/repository/public</url>
</mirror>
```

# 2.MAVEN 在 idea 开发环境中使用

#### (1).启动 IDEA

#### (2).创建新项目

![1645615395748](../mdBeforeImg/\1645615395748.png)

![1645615717457](../mdBeforeImg/\1645615717457.png)

![1645615867474](../mdBeforeImg/\1645615867474.png)

#### (3).等待项目初始化导入完毕

![1645616066596](../mdBeforeImg/\1645616066596.png)

#### (4).观察 Maven 仓库多了什么东西

![1645616254084](../mdBeforeImg/\1645616254084.png)

#### (5).IDEA 中的 Maven 设置

IDEA 项目创建成功后，看一眼 Maven 的配置

![1645616539226](../mdBeforeImg/\1645616539226.png)

![1645616857279](../mdBeforeImg/\1645616857279.png)

#### (6)到这里，Maven 在 IDEA 中的配置和使用就 OK 了！

#### (7).！！！注意，第一个项目创建不完全,接着创建第二个

![1645617255059](../mdBeforeImg/\1645617255059.png)

![1645617425378](../mdBeforeImg/\1645617425378.png)

#### (8).创建好一个 webapp 后，需要手动添加 java，和 resources 文件夹，在 main 下与 webapp 同一级目录

![1645617861334](../mdBeforeImg/\1645617861334.png)

#### （9）标记文件夹功能

![1645618057137](../mdBeforeImg/\1645618057137.png)

![1645618209649](../mdBeforeImg/\1645618209649.png)

![1645618329471](../mdBeforeImg/\1645618329471.png)

## 3.在 IDEA 配置 tomcat

#### 1.

![1645618506663](../mdBeforeImg/\1645618506663.png)

#### 2.![1645618567696](../mdBeforeImg/\1645618567696.png)

#### 3.

![1645618776123](../mdBeforeImg/\1645618776123.png)

#### 4.

![1645618879369](../mdBeforeImg/\1645618879369.png)

#### 5.

![1645618904813](../mdBeforeImg/\1645618904813.png)

必须要的配置：为什么会有这个问题：我们访问一个网站，需要指定一个文件夹名字

#### 6.

![1645619148386](../mdBeforeImg/\1645619148386.png)

#### 7.

![1645619205355](../mdBeforeImg/\1645619205355.png)

#### 8.

![1645619372840](../mdBeforeImg/\1645619372840.png)

#### 9.

![1645619565672](../mdBeforeImg/\1645619565672.png)

#### 10.pom.xml 文件

pom.xml 文件是 Maven 的核心文件

![1645619610492](../mdBeforeImg/\1645619610492.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.firstweb</groupId>
  <artifactId>javaweb-01-maven</artifactId>
  <version>1.0-SNAPSHOT</version>
<!--
  package:项目打包方式
  jar:java应用
  war:javaweb应用
-->
  <packaging>war</packaging>

  <name>javaweb-01-maven Maven Webapp</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
<!--    项目默认构建编码-->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
<!--    编码版本-->
    <maven.compiler.source>1.7</maven.compiler.source>
    <maven.compiler.target>1.7</maven.compiler.target>
  </properties>

<!--  项目依赖-->
  <dependencies>
<!--    具体依赖的jar包配置文件-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
<!--项目构建的东西-->
  <build>
    <finalName>javaweb-01-maven</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>

```

### 注意 maven 生成的.jsp 文件不会自动创建字符编码，会乱码，要自己加上

```html
<%@ page language="java" contentType="text/html; charset=utf-8"
pageEncoding="utf-8" %> <%--<%@ page language="java" contentType="text/html;
charset-utf-8" pageEncoding="utf-8" %>--%>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Title</title>
  </head>
  <body></body>
</html>
```

## 4.设置 Maven 项目 jsp 页面自动更新

**![1645623023728](../mdBeforeImg/\1645623023728.png)**

![1645623115141](../mdBeforeImg/\1645623115141.png)

![1645623181652](../mdBeforeImg/\1645623181652.png)

现在就可以实时刷新

![1645623210455](../mdBeforeImg/\1645623210455.png)
