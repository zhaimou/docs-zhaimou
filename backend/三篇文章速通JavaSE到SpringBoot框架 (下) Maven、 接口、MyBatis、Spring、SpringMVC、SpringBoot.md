### 前言
本文只是速通一下这些重要概念并简单实现下简单的demo 后续会更新精进SpringBoot的相关文章
### Maven
#### 非Maven项目的缺点
问题一：
项目中的jar包资源需要我们自己从网上下载后，手动导入到项目中使用，不好管理。<br/>
问题二：
jar包版本控制麻烦

Maven是使用Java语编写的基于项目对象模型(POM)项目管理工具软件，开发者可通过小段描述信息来管理项目构建、报告和文档。使用`Maven`可以更好的帮助我们完成项目的管理。
#### Maven仓库
**中央仓库**（**CentralRepository**）:Maven官方服务器。里面存放了绝大多数市面上流行的jar。允许用户注册后，上传自己的项目到官方服务器。网址在国外，经常访问不了。https://mvnrepository.com<br/>
**本地仓库**（**LocalRepository**）:本机的文件夹作为本地仓库，本地仓库指本机的一份贝，用来缓存远程下载，包含你尚未发布的临时构件<br/>
**镜像仓库**（**MirrorRepository**）:对于国内来说，访问国外的Maven仓库会特别慢。镜像仓库就是另一台备份/复制了中央仓库的服务器。平时使用时国内开发者多使用阿里云镜像或华为云镜像，这样可以大大提升从中央仓库下载资源的速度。但它的角色仍然是一个远程库。
#### Maven的资源坐标
Groupld:一般是逆向公司域名<br/>
。同一个公司的Groupld都是相同的
Artifactld:一般是项目(jar)名mysql-connector-java<br/>
Version:版本号8.0.28<br/>
#### Maven的下载和安装
`https://maven.apache.org/download.cgi`

如果终端出现问题mvn not found 
```
```
#### Maven常用配置
在解压出的文件中conf文件夹中settings.xml配置信息
```xml
//根据他们所在相对应的标签配置
<localRepository>your path</localRepository>

<mirror>  
  <id>alimaven</id>  
  <name>aliyun maven</name>  
  <url>http://maven.aliyun.com/nexus/content/groups/public/</url>  
  <blocked>central</blocked>  
</mirror>  
 </mirrors>

<profile>  
    <id>jdk-11</id>  
    <activation>    <activeByDefault>true</activeByDefault>  
    <jdk>11</jdk>  
      </activation>   <properties>   <maven.compiler.source>11</maven.compiler.source>  
    <maven.compiler.target>11</maven.compiler.target>  
     <maven.compiler.compilerVersion>11</maven.compiler.compilerVersion>  
   </properties></profile>
```
#### Maven使用
打开idea 选择新建项目选择 Maven就行 
在pom.xml引入包。在相关网站搜索并引入就行`https://mvnrepository.com/`
![[Pasted image 20240927145436.png]]
```xml
//pom.xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">  
  <modelVersion>4.0.0</modelVersion>  
  
  <groupId>org.example</groupId>  
  <artifactId>test01</artifactId>  
  <version>1.0-SNAPSHOT</version>  
  <packaging>jar</packaging>  
  
  <name>test01</name>  
  <url>http://maven.apache.org</url>  
  
  <properties>    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>  
  </properties>  
  <dependencies>    <dependency>      <groupId>junit</groupId>  
      <artifactId>junit</artifactId>  
      <version>3.8.1</version>  
      <scope>test</scope>  
    </dependency>    <dependency>      <groupId>mysql</groupId>  
      <artifactId>mysql-connector-java</artifactId>  
      <version>8.0.28</version>  
    </dependency>    <dependency>      <groupId>org.mybatis</groupId>  
      <artifactId>mybatis</artifactId>  
      <version>3.5.6</version>  
    </dependency>  </dependencies></project>
```
### 接口
1. 类是类，接口是接口。
 2. 接口：定义规则。实现类：实现接口，实现规则
 3. 接口：用interface来表示。
 4. 在JDK1.8之前，接口中的内容：常量、抽象方法
 5. 实现类实现接口，利用implements关键字
 6. 实现类实现接口后，重写接口中定义的抽象方法
 7. 接口不能创建对象，需要用接口指向实现类的形式创建对象。（多态的形式）
```java
public interface Speak{
/*常量：
它的数值不能改变，一旦给定了值以后就不能更改
接口中的常量前面的修饰符：public static final如果在接口中，可以省略public static final约定俗成的规定，一般定义常量的时候，名字全部大写*/

// 约定俗称 定义常量名字大写
public static final int AGT = 18;
//抽象方法
//在接口中，public abstract可以省略
public abstract void say();
}
```
接口不能创建对象 但是可以创建实现类的对象
```java
public class Chinese implements Speak {  
// 重写接口中的抽象方法  
@Override  
public void speak() {  
System.out.println("你好");  
}  
}
Speak s = new Chinese(); // 多态 s.speak(); // 调用实现类中的方法

```
#### 接口和继承的区别
继承：子类对父类的继承，提高代码的复用性。“is-a”的关系。<br/>
实现：实现类对接口的实现，实现规则。“has-a”的关系

### 框架
#### 框架出现的意义
重复/基础代码封装，同时添加额外功能<br/>
释放程序员写代码精力，更关注业务层面<br/>
框架是半成品。
#### 常见框架

常见Java框架分类
 1. 持久层框架。MyBatis、Hibernate、Spring Data、iBatis
 2. MVC框架。Spring MVC、 Struts1、 Struts2d
  3. 项目管理框架。SpringFramework、Spring Boot
  4. 微服务框架。Springcloud。
  5. 权限管理框架。SpringSecurity、Shiro。
### MyBatis
`https://mybatis.net.cn/index.html`官网
**MyBatis** 是一款优秀的持久层框架，它支持自定义 SQL、存储过程以及高级映射。MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。
#### MyBatis是持久层框架<br/>
持久层是分层开发中专门负责访问数据源的一层，Java项目中每一层都有自己的作用，持久层的作用就是访问数据源，把访问数据源的代码和业务逻辑代码分离开，有利于后期维护和团队分工开发。同时也增加了数据访问代码的复用性。
#### MyBatis是ORM框架<br/>
ORM(Object/RelationMapping)中文名称:对象/关系映射。是一种解决数据库发展和面向对象编程语言发展不匹配问题而出现的技术。
#### 搭建第一个MyBatis框架
1. 创建数据库表
2. 创建Maven项目
3. 添加依赖
```java
//pom.xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">  
  <modelVersion>4.0.0</modelVersion>  
  
  <groupId>org.example</groupId>  
  <artifactId>test01</artifactId>  
  <version>1.0-SNAPSHOT</version>  
  <packaging>jar</packaging>  
  
  <name>test01</name>  
  <url>http://maven.apache.org</url>  
  
  <properties>    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>  
  </properties>  
  <dependencies>    <dependency>      <groupId>junit</groupId>  
      <artifactId>junit</artifactId>  
      <version>3.8.1</version>  
      <scope>test</scope>  
    </dependency>    <dependency>      <groupId>mysql</groupId>  
      <artifactId>mysql-connector-java</artifactId>  
      <version>8.0.28</version>  
    </dependency>    <dependency>      <groupId>org.mybatis</groupId>  
      <artifactId>mybatis</artifactId>  
      <version>3.5.6</version>  
    </dependency>  </dependencies></project>
```

4. 创建MyBatis全局配置文件
```java
<?xml version="1.0" encoding="UTF-8" ?>  
<!DOCTYPE configuration  
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"  
        "http://mybatis.org/dtd/mybatis-3-config.dtd">  
<configuration>  
    <environments default="mysql">  
        <environment id="mysql">  
            <transactionManager type="JDBC"/>  
            <dataSource type="POOLED">  
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>  
                <property name="url" value="jdbc:mysql://127.0.0.1:3306/book?useSSL=false"/>  
                <property name="username" value="yourusername"/>  
                <property name="password" value="yourpassword"/>  
            </dataSource>        </environment>    </environments>    <mappers>        <mapper resource="mapper/BookMapper.xml"></mapper> 
    </mappers></configuration>
```
5. 创建实体类
```java
//zhai.test.book
package zhai.test.book;  
  
public class Book {  
        private int id;  
        private String title;  
  
    public int getId() {  
        return id;  
    }  
  
    public void setId(int id) {  
        this.id = id;  
    }  
  
    public String getTitle() {  
        return title;  
    }  
  
    public void setTitle(String title) {  
        this.title = title;  
    }  
  
    public Book() {  
    }  
  
    public Book(int id, String title) {  
        this.id = id;  
        this.title = title;  
    }  
}
```
6. 创建映射文件
```java
//BookMapper.xml
<?xml version="1.0" encoding="UTF-8" ?>  
<!DOCTYPE mapper  
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"  
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">  
<mapper namespace="a.b">  
    <select id="selectAllBooks" resultType="zhai.test.book.Book">  
         select * from book  
    </select>  
</mapper>

```

7. 编写测试类，启动项目
```java
package com.zhai.test;  
  
import org.apache.ibatis.io.Resources;  
import org.apache.ibatis.session.SqlSession;  
import org.apache.ibatis.session.SqlSessionFactory;  
import org.apache.ibatis.session.SqlSessionFactoryBuilder;  
import zhai.test.book.Book;  
  
import java.io.IOException;  
import java.io.InputStream;  
import java.util.List;  
  
public class test {  
    public static void main(String[] args) throws IOException {  
        //制定myBatis核心配置文件路径  
        String resource = "mybatis.xml";  
        //获取加载配置文件的输入流  
        InputStream inputStream = Resources.getResourceAsStream(resource);  
  
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);  
  
        SqlSession sqlSession = sqlSessionFactory.openSession();  
  
        List list = sqlSession.selectList("a.b.selectAllBooks");  
  
        for(int i= 0; i< list.size(); i++){  
          Book b =(Book)list.get(i);  
            System.out.println(b.getTitle()+ "---" + b.getId());  
        }  
        sqlSession.close();  
    }  
}
```
#### 别名设置
MyBatis提供了别名机制可以对某个类起别名或给某个包下所有类起别名，简化resultType取值的写法。
在核心配置文件中，通过\<typeAlias>标签明确设置类型的别名。<br/>
type：类型全限定路径<br/>
alias:别名名称<br/>
当类数较多时，明确指定别名工作量较可以通过\<package>标签指定包下全部类的别名。指定后所有类的别名就是类名.(也不区分大小写）
```xml
//mybatis.xml
<typeAliases>  
    <package name="zhai.test.book"></package>  
</typeAliases>
//BookMapper.xml
<mapper namespace="a.b">  
    <select id="selectAllBooks" resultType="Book">  
         select * from book  
    </select>  
</mapper>
```
![[Pasted image 20240927104012.png]]

#### 属性文件配置

```java
//db.properties
driver = com.mysql.cj.jdbc.Driver  
url = jdbc:mysql://127.0.0.1:3306/book?useSSL=false  
name = root  
password = zhai2665323601
```

```xml
//mybatis.xml
<?xml version="1.0" encoding="UTF-8" ?>  
<!DOCTYPE configuration  
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"  
        "http://mybatis.org/dtd/mybatis-3-config.dtd">  
<configuration>  
    <properties resource="db.properties"></properties>  
    <typeAliases>        <package name="zhai.test.book"></package>  
    </typeAliases>    <environments default="mysql">  
  
        <environment id="mysql">  
  
            <transactionManager type="JDBC"/>  
  
            <dataSource type="POOLED">  
                <property name="driver" value="${driver}"/>  
                <property name="url" value="${url}"/>  
                <property name="username" value="${name}"/>  
                <property name="password" value="${password}"/>  
            </dataSource>        </environment>    </environments>    <mappers>        <mapper resource="mapper/BookMapper.xml"></mapper>  
    </mappers></configuration>
```

#### MyBatis启动日志功能
MyBatis框架内置日志工厂。日志工厂负责自动加载项目中配置的日志。MyBatis支持以下日志：
1. SLF4J
2. Apache Commons Logging
3. Log4j2
4. Log4j（deprecated since3.5.9）
5. JDK logging
这里我们使用Log4j
```xml
//添加依赖
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```
在resources中新建log4j.properties配置文件。名称必须叫这个名字，扩展名必须是.properties
```java
log4j.rootLogger = error,console  
  
log4j.logger.a.b = TRACE  
### console ###  
log4j.appender.console=org.apache.log4j.ConsoleAppender  
log4j.appender.console.target = System.out  
log4j.appender.console.layout=org.apache.log4j.PatternLayout  
log4j.appender.console.layout.ConversionPattern=%d{ISO8601} [%t] %-5p %c %x - %m%n
```

![[Pasted image 20240927201828.png]]
#### MyBatis参数传递问题
使用符号：#{}进行获取中名字使用规则
arg、arg1、argM(M为从0开始的数字，和方法参数顺序对应)<br/>
param1、param2、paramN(N为从1开始的数字，和方法参数顺序对应)
##### 如果多个参数且参数有对象，获取参数
使用符号：进行获取
argM.属性名<br/>
paramN.属性名
PS：argM.或者paramN.不可以省略不写
```xml
<mapper namespace="com.example.UserMapper">  
<insert id="insertUser">  
    INSERT INTO users (username, age)  
    VALUES (#{arg0.username}, #{arg0.age})  
</insert>  
  
<insert id="insertUserWithParam">  
    INSERT INTO users (username, age)  
    VALUES (#{param1.username}, #{param1.age})  
</insert>  
</mapper>
```
### Spring
#### SpringIoCDI介绍
loc（inversionofControl）中文名称：控制反转，也被称为DIgependencyinjection）：依赖注入。注意：属于同一件事情的两个名称<br/>
创建对象的权利或者是控制的位置，由JAVA代码转移到spring容器，由spring的容器控制对象的创建，就是控制反转<br/>
由于控制反转概念比较含糊，所以在2004年大师级人物MartinFowler又给出了一个新的名字：“依赖注入”，相对loC而言，“依赖注入”明确描述了“被注入对象依赖IoC容器来配置依赖对象”，DI英文全称为DependencyInjection，中文译名为依赖注入）是loc的别名。<br/>
#### Spring
1. 对比以往项目，Spring优势有哪些：方便解耦，简化开发；AOP切面编程；声明式事务；整合各种优秀的框架
2. 不重复造轮子
3. 使用Spring所需jar包
4. spring官网：去spring官网找：https://spring.io/
#### 相关图例

![[Pasted image 20240927222911.png]]

![[Pasted image 20240927224331.png]]
#### 第一个spring项目 完成IoC/DI代码实现

创建maven项目 添加依赖
Spring项目想要运行起来必须包含
spring-context jar它依赖了下面的四个jar。
spring-core jar-它依赖了spring-jcl jar<br/>
spring-aop jar<br/>
spring-expression jar<br/>
spring-beans jar<br/>
spring-jcl jar<br/>
所以在Maven中想要使用Spring框架只需要在项目中导入spring-context就可以了，其他的jar包根据Maven依赖传递性都可以导入进来
```xml
  <dependency>  
    <groupId>org.springframework</groupId>  
    <artifactId>spring-context</artifactId>  
    <version>5.3.23</version>  
  </dependency></dependencies>
```
 实现一个实体类Book之后代码实现 
```java
// resources/applicationContext.xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xsi:schemaLocation="http://www.springframework.org/schema/beans  
        https://www.springframework.org/schema/beans/spring-beans.xsd">  
    <bean id="b" class="org.example.Book">  </bean>
    </beans>  
//test.java
package org.example;  
  
import org.springframework.context.ApplicationContext;  
import org.springframework.context.support.ClassPathXmlApplicationContext;  
  
public class test {  
    public static void main(String[] args) {  
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");  
        Book b = (Book)context.getBean("b");  
        Book b1 = (Book)context.getBean("b1");  
        System.out.println(b.getId()+"---"+b.getTitle());  
        System.out.println(b1.getId()+"---"+b1.getTitle());  
  
    }  
}

```
#### 属性注入方式
##### 设值注入 
相关代码实现
```xml

// resources/applicationContext.xml
<bean id="b" class="org.example.Book">  
    <!-- collaborators and configuration for this bean go here -->  
    <property name="id" value="1"></property>  
    <property name="title" value="三国"></property>  
</bean>
```
##### 构造注入
相关代码实现
```xml
//resources/applicationContext.xml
<bean id="b1" class="org.example.Book">  
    <constructor-arg name="id" value="2"></constructor-arg>  
    <constructor-arg name="title" value="水浒"></constructor-arg>  
</bean>
```
##### 属性为复杂引用类型
```java
<bean id="b" class="org.example.Boy">  
    <property name="age" value="18"></property>  
    <property name="name" value="芜湖"></property>  
</bean>  
<bean id="g" class="org.example.Girl">  
    <property name="age" value="18"></property>  
    <property name="name" value="小红"></property>  
    <property name="boyfriend" ref="b"></property>  
</bean>
```
设置属性的值：
方式1：value：简单数据类型（基本数据类型+String）直接设置<br/>
方式2：ref:需要引I用另一个bean的id。也就是说这个参数是一个类类型，且这个类的对象也被Spring容器管理。
#### IoC/DI相关注解

![[Pasted image 20240928093846.png]]
@Component的使用
在要创建对象的类中加入@Component注解，对象名字默认为：类名首字母变小写
注解在哪个包下？要想找到这些注解，需要将注解所在的包进行扫描：设置需要扫描的包。并且需要在applicationContext.xml中添加context命名空间<br/>
前五个注解作用一样，只所以搞出这么多，就是在语义上给你区别，放入不同层用不同的注解，但是作用都是创建对象
```xml
//
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xmlns:context="http://www.springframework.org/schema/context"  
       xsi:schemaLocation="http://www.springframework.org/schema/beans  
        https://www.springframework.org/schema/beans/spring-beans.xsd        http://www.springframework.org/schema/context        https://www.springframework.org/schema/context/spring-context.xsd        ">  
    <context:component-scan base-package="org.example"></context:component-scan>  
</beans>
```
使用
```java
//book.java
package org.example;  
  
import org.springframework.beans.factory.annotation.Value;  
import org.springframework.stereotype.Component;  
  
@Component  
public class Book {  
    @Value("1")  
    private int id;  
    @Value("三国")  
    private String title;  
  
    public Book() {  
        System.out.println("空构造器");  
    }  
  
    public Book(int id, String title) {  
        System.out.println("有掺构造器");  
        this.id = id;  
        this.title = title;  
    }  
  
    public int getId() {  
        return id;  
    }  
  
    public void setId(int id) {  
        System.out.println("setid");  
        this.id = id;  
    }  
  
    public String getTitle() {  
        return title;  
    }  
  
    public void setTitle(String title) {  
        System.out.println("settitile");  
        this.title = title;  
    }  
}
//test.java
package org.example;  
  
import org.springframework.context.ApplicationContext;  
import org.springframework.context.support.ClassPathXmlApplicationContext;  
  
public class test {  
    public static void main(String[] args) {  
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");  
        Book b = (Book)context.getBean("book");  
        System.out.println(b.getId()+"---"+b.getTitle());  
  
    }  
}
```
##### @Value的使用 
给普通数据类型赋值的注解， 普通数据类型包括：八种基本数据类型+String<br/>
@Autowired的使用
添加@Autowired注解后会把容器中的对象自动注入进来，并且不需要依赖set方法。
```java
@Autowired  
private Boy boyfriend;
```
### web项目构建
#### java项目和web项目的区别
Java项目是由main方法来开始的，直接依赖JVM就能被编译执行。Java项目不需要服务器。<br/>
Web项目中的Java文件是tomcat服务器来触发的，脱离了web服务器就无法启动。Web项目需要服务器。Web项目部署到服务器上，任何用户都可以通过浏览器来访问。将本地资源共享给外部访问。<br/>
#### 使用服务器
Tomcat服务器对Servlet，Jsp，JNDI，JavaMail有很好的的支持，并且这个Web容器是开源免费的。(Apache开源免费)
#### 创建maven webapp项目
在idea中使用tomcat 插件
```xml
//pom.xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">  
  <modelVersion>4.0.0</modelVersion>  
  <groupId>org.example</groupId>  
  <artifactId>javaweb01</artifactId>  
  <packaging>war</packaging>  
  <version>1.0-SNAPSHOT</version>  
  <build>    <plugins>      <plugin>        <groupId>org.apache.tomcat.maven</groupId>  
        <artifactId>tomcat7-maven-plugin</artifactId>  
        <version>2.2</version>  
        <configuration>          <path>/javaweb01</path>  
          <port>8080</port>  
        </configuration>      </plugin>    </plugins>  </build></project>
```
### SpringMVC
Spring MVC 是一种基于 Java 的 Web 框架，是 Spring Framework 的一部分，用于构建现代化的企业级应用程序。它采用了模型-视图-控制器 (MVC) 设计模式，帮助开发者将应用程序的不同关注点分离，使得代码更加模块化和可维护。
**处理 HTTP 请求**：接收和处理来自客户端的 HTTP 请求，分发请求到相应的控制器 也就是获取前端传过来的数据 响应内容到前端<br/>
**分离关注点**：通过模型-视图-控制器 (MVC) 设计模式，将应用程序的业务逻辑、用户界面和输入处理分开，提高代码的可维护性和可测试性。
#### 相关实现
1. 创建maven-web项目
2. 补全目录
![[Pasted image 20240928154421.png]]
3. 添加依赖
4. 加入tomcat插件
```xml
pom.xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">  
  <modelVersion>4.0.0</modelVersion>  
  <groupId>org.example</groupId>  
  <artifactId>javaweb01</artifactId>  
  <packaging>war</packaging>  
  <version>1.0-SNAPSHOT</version>  
  <dependencies>    <dependency>      <groupId>org.springframework</groupId>  
      <artifactId>spring-webmvc</artifactId>  
      <version>5.3.16</version>  
    </dependency>  </dependencies>  <build>    <plugins>      <plugin>        <groupId>org.apache.tomcat.maven</groupId>  
        <artifactId>tomcat7-maven-plugin</artifactId>  
        <version>2.2</version>  
        <configuration>          <path>/javaweb01</path>  
          <port>8080</port>  
        </configuration>      </plugin>    </plugins>  </build></project>
```
5. 编写web.xml内容
这段配置文件用于设置 Spring MVC 的 DispatcherServlet，使其能够接收和处理来自客户端的 HTTP 请求，并通过指定的 Spring 配置文件进行初始化。这是实现基于 Spring 的 MVC 架构的基础配置。
```xml
//web.xml
<?xml version="1.0" encoding="UTF-8" ?>  
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"  
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"  
         version="4.0">  
<!-- 这里可以添加 servlet、filter 等其他配置 -->  
    <servlet>  
        <servlet-name>springmvc</servlet-name>  
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>  
        <init-param>            <param-name>contextConfigLocation</param-name>  
            <param-value>classpath:springmvc.xml</param-value>  
        </init-param>        <load-on-startup>1</load-on-startup>  
    </servlet>    <servlet-mapping>        <servlet-name>springmvc</servlet-name>  
        <url-pattern>/</url-pattern>  
    </servlet-mapping></web-app>
```

6. 搭配注解环境
这段配置文件的主要作用是设定一个 Spring MVC 应用的基础环境，包括定义组件扫描的路径和启用注解驱动的 MVC 功能。它使得开发者可以通过注解来简化控制器和服务的配置，提高开发效率
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xmlns:context="http://www.springframework.org/schema/context"  
       xmlns:mvc="http://www.springframework.org/schema/mvc"  
       xsi:schemaLocation="http://www.springframework.org/schema/beans  
        https://www.springframework.org/schema/beans/spring-beans.xsd        http://www.springframework.org/schema/context        https://www.springframework.org/schema/context/spring-context.xsd        http://www.springframework.org/schema/mvc        https://www.springframework.org/schema/mvc/spring-mvc.xsd        ">  
    <context:component-scan base-package="com.zhai.controller"></context:component-scan>  
    <mvc:annotation-driven></mvc:annotation-driven>  
</beans>
```
7. 运行tomcat
```java
package com.zhai.controller;  
  
import org.springframework.stereotype.Controller;  
import org.springframework.web.bind.annotation.RequestMapping;  
  
@Controller  
public class testController {  
    @RequestMapping("/test1")  
    public String test(){  
        return "index.jsp";  
    }  
}
```
#### 获取普通参数
```java
@RequestMapping("/testParam")  
public String testParam(String name, int age){  
    System.out.println(name +"----" + age);  
    return "index.jsp";  
}
```
#### 使用类对象作为控制单元参数
JavaBean：一个包含私有属性，getter/setter方法和无参构造方法的Java类。，是不是感觉和实体类特别像。其实写法上和实体类相同。唯一区别是实体类是数据库层面的概念，类型中属性要和数据库字段对应。而JavaBean的属性是灵活的，不是必须和哪里对应的。
JavaBean是一个专业概念，可以简单点理解：使用类对象做为控制单元参数，接收请求参数。如果不是特别较真，狭义上可以认为JavaBean就是项目中的实体类
在控制单元中放置一个类型对象，对象名称没有要求，只需要保证请求参数名和类的属性名相同就可以了。
```java
   @RequestMapping("/testParam2")  
    public String testParam2(person p){  
        System.out.println(p.getname() +"----" + p.getage());  
        return "index.jsp";  
    }  
}
```

### SSM介绍
SSM:**Spring + Spring MVC + MyBatis**：一种在Java开发中常用的框架组合。

### SpringBoot
#### springboot概念简介
SpringBoot是Spring公司的一个顶级项目，和SpringFramework是一个级别的。<br/>
SpringBoot实际上是利用SpringFramework4自动配置特性完成。编写项目时不需要编写xml文件。发展到现在，SpringBoot已经县有很很大的生态圈，各种主流技术已经都提供了SpringBoot的启动器。
#### springBoot优点
`约定大于配置`
#### 例子:整合SpringMVC
1. 创建maven工程
2.  选择springboot的版本添加到pom.xml
```xml
<dependencyManagement>  
  <dependencies>    <dependency>      <groupId>org.springframework.boot</groupId>  
      <artifactId>spring-boot-dependencies</artifactId>  
      <version>2.4.5</version>  
      <type>pom</type>  
      <scope>import</scope>  
    </dependency>  </dependencies></dependencyManagement>
```
3. 整合springmvc用到的包,添加启动器
什么是启动器<br/>
Spring框架在项目中作用是Spring整合各种其他技术，让其他技术使用更加方便。SpringBoot的启动器实际上就是一个依赖。这个依赖中包含了整个这个技术的相关jar包，还包含了这个技术的自动配置，以前绝大多数XML配置都不需要配置了。以后每次使用SpringBoot整合其他技术时首先需要考虑导入启动器。<br/>
什么是启动类<br/>
SpringBoot的启动类的作用是启动SpringBoot项目，是基于Main方法来运行的<br/>
==启动类与启动器区别==
启动类表示项目的启动入口<br/>
启动器表示jar包的坐标
```xml
<dependencies>  
  <dependency>    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-web</artifactId>  
  </dependency></dependencies>
```
4. 开发一个Controller控制层
```java
package com.zhai.controller;  
  
import org.springframework.stereotype.Controller;  
import org.springframework.web.bind.annotation.RequestMapping;  
import org.springframework.web.bind.annotation.ResponseBody;  
  
@Controller  
public class MyController {  
    @RequestMapping("/test01")  
    @ResponseBody  
    public String test01(){  
        return "hi,springboot...";  
    }  
}
```
5. 启动类编写
```java
package com.zhai.controller;  
  
import org.springframework.boot.SpringApplication;  
import org.springframework.boot.autoconfigure.SpringBootApplication;  
  
@SpringBootApplication  
public class testSpringBootApplication {  
    public static void main(String[] args) {  
        SpringApplication.run(testSpringBootApplication.class,args);  
    }  
}
```
6. 运行，游览器访问测试 
![[Pasted image 20240928185546.png]]
#### springBoot配置文件
在resources中创建文件application.properties编写内容
```java
server.port = 8080  
server.servlet.context-path=/springboot01
```
官方推荐的配置文件
springboot官方推荐的配置文件是yml文件，yml是用层级来表示关系的一种配置文件。yml中没有标签，而是通过两个空格的缩进来表示层级结构<br/>
例如：
properties中：
server.port=8080
yml中：
Server:
port:8080
层级结构怎么找（SpringBoot常见配置，查看官网文档）
https://docs.spring.io/spring-boot/docs/2.7.6/reference/html/application-properties.html#appendix.application-properties
注意：文件名字为：**application**.yml，文件名字application开头，不能随意动<br/>
==注意冒号后空格==
```yml
server:  
  port: 9999  
  servlet:  
    context-path: /test02
```
#### SpringBoot整合SSM
1. 导入依赖
```xml
//pom.xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">  
  <modelVersion>4.0.0</modelVersion>  
  <groupId>org.example</groupId>  
  <artifactId>onessm</artifactId>  
  <packaging>war</packaging>  
  <version>1.0-SNAPSHOT</version>  
  <dependencyManagement>    <dependencies>      <dependency>        <groupId>org.springframework.boot</groupId>  
        <artifactId>spring-boot-dependencies</artifactId>  
        <version>2.4.5</version>  
        <type>pom</type>  
        <scope>import</scope>  
      </dependency>    </dependencies>  </dependencyManagement>  <dependencies>    <dependency>      <groupId>org.springframework.boot</groupId>  
      <artifactId>spring-boot-starter-web</artifactId>  
    </dependency>    <dependency>      <groupId>org.mybatis.spring.boot</groupId>  
      <artifactId>mybatis-spring-boot-starter</artifactId>  
      <version>2.1.3</version> <!-- 替换为你需要的版本 -->  
    </dependency>  
    <dependency>      <groupId>mysql</groupId>  
      <artifactId>mysql-connector-java</artifactId>  
    </dependency>  </dependencies>  
</project>
```
 2. 编写配置文件
```java
server:  
  port: 9999  
  servlet:  
    context-path: /test02  
spring:  
  datasource:  
    url: jdbc:mysql://127.0.0.1:3306/book?useSSL=false  
    driver-class-name: com.mysql.cj.jdbc.Driver  
    username: root  
    password: yourpassword
```
3. 编写实体类，配置文件中加入别名
![[Pasted image 20240928195008.png]]
4. 定义mapper接口和定义mapper.xml映射文件
```java
	package com.zhai.mapper;  
  
import java.util.List;  
  
public interface BookMapper {  
    List selectAllBooks();  
}
// BookMapper.xml
<?xml version="1.0" encoding="UTF-8" ?>  
<!DOCTYPE mapper  
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"  
        "https://mybatis.org/dtd/mybatis-3-mapper.dtd">  
<mapper namespace="com.zhai.mapper.BookMapper">  
    <select id="selectAllBooks" resultType="book">  
        select * from book  
    </select>  
</mapper>
```
7. 定义启动类在启动类加入mapper的包扫描
```java
package com.zhai;  
  
import org.mybatis.spring.annotation.MapperScan;  
import org.springframework.boot.SpringApplication;  
import org.springframework.boot.autoconfigure.SpringBootApplication;  
  
@SpringBootApplication  
@MapperScan("com.zhai.mapper")  
public class testSpringBootApplication {  
    public static void main(String[] args) {  
        SpringApplication.run(testSpringBootApplication.class,args);  
    }  
}
```
### 最终效果实现
![[Pasted image 20240928231954.png]]

> 如果对你有用的话 就点个关注吧 会持续更新技术文章

