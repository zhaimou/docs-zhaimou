### IO
Java IO流是Java中处理输入和输出的一个重要机制。它提供了一系列的类和接口来处理数据的读写，包括文件、网络等。Java IO可以分为两大类：字节流和字符流。
#### file类的作用
File类对象可封装要操作的文件，可通过File类的对象对文件进行操作，如查看文件的大小、判断文件是否隐藏、判断文件是否可读等<br/>
局限：File类的相关操作，并不涉及文件内容相关的操作，这是单独依靠File类对象无法实现的操作，此时需要借助I/O流完成

#### I/O的作用
![[Pasted image 20240924081116.png]]
#### 功能划分
方式1：按照方向划分输入流、输出流。<br/>
方式2：按照处理单元划分字节流、字符流。<br/>
方式3：按照功能划分。节点流、处理流。
![[Pasted image 20240924084241.png]]
想关代码操作
==文件对程序进行输入操作==
```java
//文件对程序进行输入操作
import java.io.File;  
import java.io.FileReader;  
import java.io.IOException;  
  
public class iotest {  
    public static void main(String[] args) throws IOException {  
        //对文件进行操作，必须将文件封装为File对象  
        File f = new File("d:\\test.txt");  
        //“管子”=流=输入字符流 将管子怼到文件上-管子和文件结合  
        FileReader fr = new FileReader(f);  
        //开始动作吸 一口 利用循环吸完  
        int n = fr.read();  
        while(n != 1){  
             n = fr.read();  
            System.out.println(n);  
        }  
        //关闭操作  
        fr.close();  
    }  
}
```
==程序对文件进行输出操作==
```java
public class iotest02 {  
    public static void main(String[] args) throws IOException {  
        String str = "abc";  
        File f= new File("d:\\demo.txt");  
        FileWriter fw = new FileWriter(f);  
        fw.write(str);  
  
        fw.close();  
    }  
  
}
```
#### 将上篇文章综合项目使用IO流升级
图书管理有个缺点就是  数据不能永久保存 
##### 所需知识点
 1. 对象流：
FilelnputStream、 FileOutputStream
ObjectinputStreamObjectoutputStream
 2. 序列化：
implements Serializable
实现了Serializable接口，才会具备将对象输出到文件的能力
```java
// Book.java
//public class Book  implements Serializable 
J//test01.java
public class test01 {  
    public static void main(String[] args) throws IOException, ClassNotFoundException {  
        // 开始程序主循环，提供用户交互界面  
        while(true) {  
            // 打印主菜单  
            System.out.println("----图书管理----");  
            System.out.println("1.展示书籍");  
            System.out.println("2.添加书籍");  
            System.out.println("3.删除书籍");  
            System.out.println("4.退出应用");  
  
            // 创建 Scanner 对象以获取用户输入  
            Scanner sc = new Scanner(System.in);  
            System.out.println("请输入功能号码");  
            int choice = sc.nextInt(); // 读取用户选择的功能  
  
            // 根据用户选择的功能执行相应操作  
            if (choice == 1) { // 展示书籍  
                System.out.println("--图书展示区域--");  
                File f = new File("demo.txt"); // 创建文件对象，指向 demo.txt                FileInputStream fis = new FileInputStream(f); // 创建文件输入流  
                ObjectInputStream ois = new ObjectInputStream(fis); // 创建对象输入流  
                ArrayList list = (ArrayList)(ois.readObject()); // 读取对象并转换为 ArrayList  
                // 遍历书籍列表并打印每本书的编号和名称  
                for (int i = 0; i < list.size(); i++) {  
                    Book b = (Book)(list.get(i));  
                    System.out.println(b.getbNo() + "---" +b.getBName());  
                }  
                ois.close(); // 关闭流以释放资源  
  
            } else if (choice == 2) { // 添加书籍  
                // 提示用户输入书籍信息  
                System.out.println("请输入书籍编号");  
                int bNo =sc.nextInt(); // 读取书籍编号  
                System.out.println("请输入书籍名字");  
                String bName = sc.next(); // 读取书籍名称  
  
                // 创建新的书籍对象  
                Book b = new Book();  
                b.setbNo(bNo); // 设置书籍编号  
                b.setBName(bName); // 设置书籍名称  
  
                // 获取文件对象  
                File f = new File("demo.txt");  
                if(f.exists()) { // 如果文件存在  
                    // 防止覆盖已有内容，先读取现有书籍  
                    FileInputStream fis  = new FileInputStream(f);  
                    ObjectInputStream ois = new ObjectInputStream(fis);  
                    ArrayList list = (ArrayList)(ois.readObject()); // 读取现有书籍列表  
  
                    // 将新书籍添加到列表中  
                    list.add(b);  
  
                    // 将更新后的列表写回文件  
                    FileOutputStream fos = new FileOutputStream(f);  
                    ObjectOutputStream oos = new ObjectOutputStream(fos);  
                    oos.writeObject(list); // 写入更新后的列表  
                    oos.close(); // 关闭流  
  
                } else { // 如果文件不存在  
                    ArrayList list = new ArrayList(); // 创建新的书籍列表  
                    list.add(b); // 添加新书籍  
                    FileOutputStream fos = new FileOutputStream(f);  
                    ObjectOutputStream oos = new ObjectOutputStream(fos);  
                    oos.writeObject(list); // 写入新书籍列表  
                    oos.close(); // 关闭流  
                }  
  
            } else if (choice == 3) { // 删除书籍  
                System.out.println("请输入删除书籍编号");  
                File f = new File("demo.txt"); // 获取文件对象  
                FileInputStream fis = new FileInputStream(f);  
                ObjectInputStream ois = new ObjectInputStream(fis);  
                ArrayList list = (ArrayList)(ois.readObject()); // 读取现有书籍列表  
  
                int delbNo = sc.nextInt(); // 读取要删除的书籍编号  
  
                // 遍历书籍列表查找要删除的书籍  
                for (int i = 0; i <list.size() ; i++) {  
                    Book b =  (Book)(list.get(i));  
                    if(b.getbNo() == delbNo) { // 如果找到匹配的书籍编号  
                        list.remove(b); // 从列表中删除书籍  
                        System.out.println("删除成功"); // 提示用户删除成功  
                        break; // 退出循环  
                    }  
                }  
  
                // 将更新后的列表写回文件  
                FileOutputStream fos = new FileOutputStream(f);  
                ObjectOutputStream oos = new ObjectOutputStream(fos);  
                oos.writeObject(list); // 写入更新后的列表  
                oos.close(); // 关闭流  
  
            } else { // 如果用户选择退出  
                break; // 结束循环，退出程序  
            }  
        }  
    }  
}
```
### 进程 线程
==程序==:是为完成特定任务、用某种语言编写的一组指令的集合，是一段静态的代码。   
(程序是静态的)<br/>
==进程==:是程序的一次执行过程。正在运行的一个程序，进程作为资源分配的单位，在内存中会为每个进程分配不同的内存区域。<br/>
==线程==:进程可进一步细化为线程，是一个进程内部的一条执行路径。若一个进程同一时间并行执行多个线程，就是支持多线程的<br/>
**进程是操作系统进行资源分配的基本单位**<br/>
**线程是操作系统调度执行的基本单位**<br/>
#### 创建线程的三种方式
1. 方式1：继承Thread类
```java
class MyThread extends Thread {  
    @Override  
    public void run() {  
        System.out.println("Thread running: " + Thread.currentThread().getName());  
    }  
}  
  
public class ThreadExample {  
    public static void main(String[] args) {  
        MyThread thread1 = new MyThread();  
        thread1.start(); // 启动线程  
    }  
}
```
2. 方式2： 实现Runnable接口
```java
class MyRunnable implements Runnable {  
    @Override  
    public void run() {  
        System.out.println("Runnable running: " + Thread.currentThread().getName());  
    }  
}  
  
public class RunnableExample {  
    public static void main(String[] args) {  
        Thread thread2 = new Thread(new MyRunnable());  
        thread2.start(); // 启动线程  
    }  
}
```
4. 方式3：实现Callable接口
```java
import java.util.concurrent.Callable;  
import java.util.concurrent.FutureTask;  
  
class MyCallable implements Callable<String> {  
    @Override  
    public String call() throws Exception {  
        return "Callable running: " + Thread.currentThread().getName();  
    }  
}  
  
public class CallableExample {  
    public static void main(String[] args) throws Exception {  
        FutureTask<String> futureTask = new FutureTask<>(new MyCallable());  
        Thread thread3 = new Thread(futureTask);  
        thread3.start(); // 启动线程  
  
        // 获取线程执行结果  
        String result = futureTask.get();  
        System.out.println(result);  
    }  
}
```

### 网络编程

#### 网络编程介绍
分布在不同地理区域的计算机与专门的外部设备用通信线路互连成一个规模大、功能强的网络系统，从而使众多的计算机可以方便地互相传递信息、共享硬性、软件、数据信息等资源。设备之间在网络中进行数据的传输，发送/接收数据。
#### IP地址
用来标志网络中的一个通信实体的地址。通信实体可以是计算机，路由器等
#### 端口号
IP地址用来标志一台计算机，但是一台计算机上可能提供多种应用程序，使用端口来区分这些应用程序。
#### 网络通信协议
计算机网络中实现通信必须有一些约定即通信协议，对速率、传输代码、代码结构、传输控制步骤、出错控制等制定标准<br/>
由于结点间联系复杂，制定协议时，把复杂成份分解成一些简单的成份，再将它们复合起来。最常用的复合方式是层次方式，即同层间可以通信、上一层可以调用下一层，而与再下一层不发生关系
#### 网络通信协议的分层
名义上标准：ISO/OSI参考模型<br/>
事实上标准：TCP/IP协议栈（Internet使用的协议）

![[Pasted image 20240924101333.png]]
我们开发的网络应用程序位于应用层，TCP和UDP属于传输层协议，在应用层如何使用传输层的服务呢？在应用层和传输层之间，则是使用套接字来进行分离。<br/>
套接字就像传输层为应用层开的一个小口，应用程序通过这个小口向远程发送数据，或接收远程发来数据而这个小口以内，也就是数据进入这个口之后，或者数据从这个口出来之前，是不知道也不需要知道的，也不会关心它如何传输，这属于网络其它层次的工作。<br/>
**Socket实际是传输层供给应用层的编程接口**。传输层则在网络层的基础上提供进程到进程问的逻辑通道，应用层的进程则利用传输层向另一台主机的某一进程通信。**Socket就是应用层与传输层之间的桥梁**
#### 演示代码
简单的 TCP 服务器
```java
    import java.io.*; // 导入输入输出流相关类  
        import java.net.*; // 导入网络相关类  
  
public class SimpleTCPServer {  
    public static void main(String[] args) {  
        try (ServerSocket serverSocket = new ServerSocket(12345)) { // 创建服务器端Socket，监听端口12345  
            System.out.println("服务器启动，等待连接...");  
            Socket clientSocket = serverSocket.accept(); // 等待并接受客户端连接  
            System.out.println("客户端连接：" + clientSocket.getInetAddress()); // 打印客户端IP地址  
  
            // 创建输入流以接收数据  
            BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));  
            // 创建输出流以发送数据  
            PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);  
  
            String inputLine;  
            // 持续接收客户端发送的数据  
            while ((inputLine = in.readLine()) != null) {  
                System.out.println("收到消息: " + inputLine); // 打印收到的消息  
                out.println("回声: " + inputLine); // 将收到的消息回显给客户端  
            }  
  
            // 关闭流和Socket连接  
            in.close();  
            out.close();  
            clientSocket.close();  
        } catch (IOException e) {  
            e.printStackTrace(); // 捕获异常并打印错误信息  
        }  
    }  
}
```
简单的 TCP 客户端
```java
import java.io.*; // 导入输入输出流相关类  
        import java.net.*; // 导入网络相关类  
  
public class SimpleTCPClient {  
    public static void main(String[] args) {  
        try (Socket socket = new Socket("localhost", 12345)) { // 连接到本地服务器，端口12345  
            // 创建输出流以发送数据  
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);  
            // 创建输入流以接收数据  
            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));  
            // 创建标准输入流以读取用户输入  
            BufferedReader stdIn = new BufferedReader(new InputStreamReader(System.in));  
  
            String userInput;  
            // 持续读取用户输入并发送给服务器  
            while ((userInput = stdIn.readLine()) != null) {  
                out.println(userInput); // 发送用户输入到服务器  
                System.out.println("服务器回复: " + in.readLine()); // 接收并打印服务器的回复  
            }  
  
            // 关闭流和Socket连接  
            in.close();  
            out.close();  
            stdIn.close();  
        } catch (IOException e) {  
            e.printStackTrace(); // 捕获异常并打印错误信息  
        }  
    }  
}
```

### XML

XML指可扩展标记语(EXtensibleMarkupLanguage)

#### XML的作用是什么？
XML是不作为的，XML不会做任何事情。XML被设计用来结构化、存储以及传输信息。它仅仅是纯文本而已。它仅仅将信息包装在XML标签中。我们需要编写软件或者程序，才能传送、接收和显示出这个文档。
#### xml特点
1. 必须有声明语句。
XML声明是XML文档的第一句，其格式如下
<7xml version=1.0 encoding=utf-8？>
2. XML文档有且只有一个根元素
良好格式的XML文档必须有一个根元素，就是紧接着声明后面建立的第一个元素，其他元素都是这个根元素的子元素，根元素完全包括文档中其他所有的元素
3. 注意大小写
在XML文档中，大小写是有区别的。 “A”和“a”是不同的标记。
4. 所有的标记必须有相应的结束标记
所有标记必须成对出现，有一个开始标记，就必须有一个结束标记，否则将被视为错误。
5. 属性值使用引号
所有属性值必须加引号（可以是单引号，也可以是双引号，建议使用双引号），否则将被视为错误
6. XML中可以加入注释
注释格式：<!-\-  -->

### 注解
### 什么是注解？
注解其实就是代码里的特殊标记， 这些标记可以在编译、类加载、运行时被读取，并执行相应的处理通过使用注解，程序员可以在不改变原有逻辑的情况下，在源文件中嵌入一些补充信息。代码分析工、开发工具和部署工可以通过这些补充信息进行验证或者进行部署
#### 注解的使用
使用注解时要在其前面增加@符号，并把该注解当成一个修饰符使用。用于修饰它支持的程序元素（包、类、构造器、方法、成员变量、参数、局部变量的声明）
#### 注解的重要性
在JavaSE中，注解的使用目的比较简单，例如标记过时的功能，忽略警告等。在JavaEE/Arldroid中注解占据了更重要的角色，例如用来配置应用程序的任何切面，代替JavaEE日版中所遗留的繁代码和XML配置等。未来的开发模式都是基于注解的。 一定程度上可以说：框架=注解+反射+设计模式
#### 注解的使用实例
1. 标识类的作者@author
2. 指定类的版本@version
3. 说明方法的参数@param
4. 说明方法的返回值类型@return
5. 限定重写的方法@Override
### MySQL
**安装Mysql和MysqlWorkbench**
`https://dev.mysql.com/downloads/workbench/`
`https://dev.mysql.com/downloads/mysql/`
**MySQL数据库**最初是由瑞典MySQLAB公司开发，2008年1月16号被Sun公司收购2009年，SUN又被Oracle收购。<br/>
由于MySQL数据库体积小、速度快、成本低、跨平台、开放源码等优点，现已被广泛应用于互联网上的中小型网站中，并且大型网站也开始使用MySQL数据库，如网易、新浪等。<br/>
 SQL（StructuredQueryLanguage）是一种操作数据库的语言。<br/>
  在数据库管理系统中，使用SQL语言来实现数据的存取、查询、更新等功能。SQL是一种非过程化语言，只需提出“做什么”，而不需要指明“怎么做”
  速成阶段目标：学习创建表SQL、对表中数据进行增删改查的SQL
**MySQL Workbench** 是一个综合性的数据库设计和管理工具，专为 MySQL 数据库开发。它提供了图形用户界面，使用户能够更轻松地与 MySQL 数据库进行交互。
#### 代码实现
```sql
创建一个新的数据库：
CREATE DATABASE my_database;
选择要使用的数据库：
USE my_database;
创建一个名为 `users` 的表
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    age INT
);
向 `users` 表中插入数据：
INSERT INTO users (name, email, age) VALUES ('Alice', 'alice@example.com', 30); INSERT INTO users (name, email, age) VALUES ('Bob', 'bob@example.com', 25);
从 `users` 表中查询所有数据：
SELECT * FROM users;
更新指定用户的年龄
UPDATE users SET age = 31 WHERE name = 'Alice';
删除指定用户的数据：
DELETE FROM users WHERE name = 'Bob';


`ALTER TABLE` 是 SQL 中用于修改现有表结构的命令。通过 `ALTER TABLE` 语句，你可以对表进行多种操作，比如添加、删除或修改列，修改表的约束等

ALTER TABLE table_name ADD column_name datatype;

ALTER TABLE table_name DROP COLUMN column_name;
```

![[Pasted image 20240924170711.png]]

### JDBC
==JDBC(Java DataBase Connectivity) 称为Java数据库连接，它是一种用于数据库访问的应用程序API，由一组用Java语言编写的类和接口组成==，有了JDBC就可以用同一的语法对多种关系数据库进行访问，而不用担心其数据库操作语言的差异。 有了JDBC，就不必为访问Mysql数据库专门写一个程序，为访问Oracle又专门写一个程序等等。
#### JDBC访问数据库编码步骤
1. 加载Driver驱动
2. 获取数据库连接(Connection)
3. 创建会话-SQL命令发送器(Statement)
4. 通过Statement发送SQL命令并得到结果
5. 处理结果
6. 关闭数据库资源（ResultSet、Statement、Connection）
#### 准备资源
1. 准备数据库
2. 官网下载数据库连接驱动jar包。`https://downloads.mysql.com/archives/c-j/`
3. 创建Java项目，在项目下创建Iib文件夹，将下的驱动jar包复制到文件夹里
4. 选中lib文件夹右键->Add as Library，与项目集成。
```java
Class.forName("com.mysql.cj.jdbc.Driver");  

String url = "jdbc:mysql://127.0.0.1:3306/book?useSSL=false";  
String username = "yourname";  
String password = "yourpassword";  
Connection conn = DriverManager.getConnection(url,username,password);  
//创建会话  
Statement sta = conn.createStatement();  
  
ResultSet rs = sta.executeQuery("select * from book where id");

while (rs.next()) { System.out.println('1'); }
  
sta.close(); conn.close();
```
### 图书管理数据库版
```java
import java.sql.*;  
import java.util.ArrayList;  
import java.util.Scanner;  
  
public class bookadmin {  
        public static void main(String[] args) throws SQLException, ClassNotFoundException {  
  
            while(true) {  
                System.out.println("----图书管理----");  
                System.out.println("1.根据id展示书籍");  
                System.out.println("2.展示全部书籍");  
                System.out.println("3.根据id删除书籍");  
                System.out.println("4.退出应用");  
                Scanner sc = new Scanner(System.in);  
                System.out.println("请输入功能号码");  
                int choice = sc.nextInt();  
                if (choice == 1) {  
                            int bno = sc.nextInt();  
                            Book b = findBookByBno(bno);  
  
                    System.out.println(b.getId() +"----" +b.getTitle());  
                } else if (choice == 2) {  
                    ArrayList books = findBook();  
  
                    for(int i = 0 ; i< books.size(); i++){  
                        Book b =(Book)books.get(i);  
                        System.out.println(b.getId()+"-----"+b.getTitle());  
                    }  
                }else if (choice == 3) {  
                    System.out.println("请录入你想要删除的书籍编号");  
                    int bno = sc.nextInt();  
                    int n = delBookById(bno);  
  
                    System.out.println("删除成功");  
                } else {  
                    break;  
                }  
  
            }  
        }  
        public static Book findBookByBno(int id) throws ClassNotFoundException, SQLException {  
            Class.forName("com.mysql.cj.jdbc.Driver");  
            Book b = null;  
            String url = "jdbc:mysql://127.0.0.1:3306/book?useSSL=false";  
            String username = "yourusername";  
            String password = "yourpassword";  
            Connection conn = DriverManager.getConnection(url,username,password);  
            //创建会话  
            Statement sta = conn.createStatement();  
  
            ResultSet rs = sta.executeQuery("select * from book where id =" + id);  
  
            if(rs.next()){  
                b = new Book();  
              //  System.out.println(rs.getInt("id") + rs.getString("title"));  
                int Bookid = rs.getInt("id");  
                String title = rs.getString("title");  
                b.setId(Bookid);  
                b.setTitle(title);  
            }  
            sta.close();  
            conn.close();  
            return b;  
  
        }  
  
        public static ArrayList findBook() throws ClassNotFoundException, SQLException {  
            ArrayList list = new ArrayList();  
            Class.forName("com.mysql.cj.jdbc.Driver");  
  
            String url = "jdbc:mysql://127.0.0.1:3306/book?useSSL=false";  
            String username = "root";  
            String password = "zhai2665323601";  
            Connection conn = DriverManager.getConnection(url,username,password);  
            //创建会话  
            Statement sta = conn.createStatement();  
  
            ResultSet rs = sta.executeQuery("select * from book");  
  
            while(rs.next()){  
               Book b = new Book();  
                //  System.out.println(rs.getInt("id") + rs.getString("title"));  
                int Bookid = rs.getInt("id");  
                String title = rs.getString("title");  
                b.setId(Bookid);  
                b.setTitle(title);  
                list.add(b);  
            }  
            sta.close();  
            conn.close();  
            return list;  
        }  
        public static int delBookById(int id) throws ClassNotFoundException, SQLException {  
            Class.forName("com.mysql.cj.jdbc.Driver");  
  
            String url = "jdbc:mysql://127.0.0.1:3306/book?useSSL=false";  
            String username = "root";  
            String password = "zhai2665323601";  
            Connection conn = DriverManager.getConnection(url,username,password);  
            //创建会话  
            Statement sta = conn.createStatement();  
  
            int n = sta.executeUpdate("delete from book where id =" + id);  
  
            sta.close();  
            conn.close();  
            return n ;  
        }  
  
    }
```
![[Pasted image 20240926223144.png]]