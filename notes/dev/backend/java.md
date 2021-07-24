# java笔记

[TOC]

## **线程池的使用**

### 1.创建线程池

```java
ExecutorService executorService = Executors.newFixedThreadPool(2);//参数为设置线程池内线程的数量
```

### 2.创建自己的Runnable类

```java
//main
MyRunnable myRunnable = new MyRunnable();
//MyRunnable
public class MyRunnable implements Runnable {
    @Override
    public void run() {//具体实现任务
        System.out.println("我要一个教练");
        try{
            Thread.sleep(2000);
        }catch (InterruptedException e){
            e.printStackTrace();
        }
        System.out.println("教练来了"+Thread.currentThread().getName());
        System.out.println("教练教完之后，回到了游泳池");

    }
}
```

### 3.使用线程池执行Runnable

```java
executorService.submit(myRunnable);
executorService.submit(myRunnable);
executorService.submit(myRunnable);
```

------

## **File类**

### 1.绝对路径和相对路径

#### 绝对路径：从根目录出发

#### 相对路径：从当前文件的根目录出发

------

### 2.Mac环境下的分隔符

```java
String pathSeparator = File.pathSeparator;
System.out.println(pathSeparator);//路径分隔符 ：
String Separator = File.separator;
System.out.println(Separator);//文件名称分隔符 /
```

------

### 3.三种常用的构造方法

```java
File f1 = new File("usr");//pathname
System.out.println(f1);
File f2 = new File("usr","bin");//parent child
System.out.println(f2);
File f3 = new File(f1,"bin");//File child
```

### 4.常用方法

#### 常用get方法

```java
getAbsolutePath();//获取绝对路径
getPath();//获取路径，是哪个就是哪个
getName();//获取当前文件夹或文件名
length();//获取文件的大小

File f4 = new File("a.txt");
System.out.println(f4.getAbsolutePath());
///Users/alan/javacode_folder/a.txt
File f5 = new File("/Users/alan/javacode_folder/a.txt");
System.out.println(f5.getAbsolutePath());
///Users/alan/javacode_folder/a.txt
System.out.println(f4.getPath());
///Users/alan/javacode_folder/a.txt
System.out.println(f5.getPath());
//a.txt
System.out.println(f4.getName()); //a.txt
File f6 = new File("/Users/alan/javacode_folder/");
System.out.println(f6.getName()); //javacode_folder
File f6 = new File("a.txt");
System.out.println(f6.length());//0 不存在 文件夹大小也为0
File f7 = new File("/Users/alan/助学贷款申请表.doc");
System.out.println(f7.length());//112516
```

#### 常用判断方法

```java
exists();//是否存在
isFile();//是否为文件
isDirectory();//是否为文件夹

File f7 = new File("a.txt");
System.out.println(f7.exists());//false
File f8 = new File("/Users/alan/javacode_folder");
System.out.println(f8.exists());//true
System.out.println(f8.isFile());//false
System.out.println(f8.isDirectory());//true
```

#### 常用创建方法(文件)

```java
createNewFile();//boolean

File f9 = new File("a.txt");
System.out.println(f9.createNewFile());//false 因为已经存在
File f10 = new File("b.txt");
System.out.println(f10.createNewFile());//true 因为还未被创建
```

#### 常用创建方法(文件夹)

```java
mkdir();//创建单级文件夹
mkdirs();//创建多级文件夹
File b1 = new File("abc");
System.out.println(b1.mkdir());//创建单级文件夹
File b2 = new File("aaa/bbb/ccc/ddd");
System.out.println(b2.mkdirs());//创建多级文件夹
System.out.println(b1.delete());//true
System.out.println(b2.delete());//true
```

#### 常用遍历方法

```java
list();//返回String数组
listFiles();//返回File对象数组

File b3 = new File("/Users/alan/javacode_folder/src/demo01_3");
String [ ]arr = b3.list();
for(String fileName:arr){
    System.out.println(fileName);
}//demoForforeach.java
File []files = b3.listFiles();
for(File file:files){
    System.out.println(file);
}///Users/alan/javacode_folder/src/demo01_3/demoForforeach.java

```

------



## **I/O流**

![](/Users/alan/Documents/I:O流.png)





### 分类

1.以内存为中心，分为输入流和输出流

2.以数据单位为中心，分为字节流和字符流

------

### 字节输出流

顶级父类OutputStream类->FileOutputStream类

#### 构造方法

```java
//构造方法
//public FileOutputStream(File file)
//public FileOutputStream(String name)
public static void main(String[] args)throws IOException {
    File file = new File("a.txt");
    FileOutputStream fos = new FileOutputStream(file);
    FileOutputStream fos2 = new FileOutputStream("b.txt");
}
//结果：在javacode_folder文件夹下创建了a.txt b.txt两个文件

//追加写入
		FileOutputStream fos1 = new FileOutputStream("fos1.txt",true);
    fos1.write(97);
		fos1.close();

```

#### 写出字节数据

```java
public static void main(String[] args) throws IOException {
        // 使用文件名称创建流对象
        FileOutputStream fos = new FileOutputStream("fos1.txt");     
      	// write()一次写出单个字节
      	fos1.write(97); // 写出第1个字节
      	fos1.write(98); // 写出第2个字节
      	fos1.write(99); // 写出第3个字节
        fos1.close();
        //写出结果：abc
  			--------------------------------------------------------
  			 FileOutputStream fos2 = new FileOutputStream("fos2.txt");     
      	// 字符串转换为字节数组
      	byte[] b = "黑马程序员".getBytes();
      	// 写出字节数组数据
      	fos2.write(b);
  			//另一种简便写法： fos2.write("黑马程序员".getBytes());
      	// 关闭资源
        fos2.close();
  			//写出结果：黑马程序员
  			--------------------------------------------------------
        FileOutputStream fos3 = new FileOutputStream("fos3.txt");     
      	// 字符串转换为字节数组
      	byte[] b = "abcde".getBytes();
		    // 写出从索引2开始，2个字节。索引2是c，两个字节，也就是cd。
        fos3.write(b,2,2);
      	// 关闭资源
        fos3.close();
  			//写出结果：cd
  			---------------------------------------------------------
        //写出换行 fos.write("\r".getBytes());
    }
```

### 字节输入流

顶级父类InputStream类->FileInputStream类

#### 构造方法

```java
File file = new File("a.txt");
FileInputStream fis = new FileInputStream(file);// File file
FileInputStream fis = new FileInputStream("a.txt");//String filename
//注意： 和OutputStream类不同的是，若文件路径中不含该名称的文件，则会抛出FileNotFoundException
```

#### 读入字节数据

```java
//a.txt:abcdef
//单个读入
int b;
while((b=fis.read())!=-1){
    System.out.println((char)b);
}
fis.close();
//多个读入
int len;
byte []b = new byte[2];
while ((len = fis.read(b)) != -1) {
    System.out.println(new String(b,0,len));//读取有效数据
}
    fis.close();
//ab cd ef 
```

#### 字节输入输出流综合使用：复制图片

```java
public static void main(String[] args) throws IOException {
    // 1.创建流对象
    // 1.1 指定数据源
    FileInputStream fis = new FileInputStream("test.bmp");
    // 1.2 指定目的地
    FileOutputStream fos = new FileOutputStream("test_copy.bmp");
    // 2.读写数据
    // 2.1 定义数组
    byte[] b = new byte[1024];//一次传输1kb
    // 2.2 定义长度
    int len;
    // 2.3 循环读取
    while ((len = fis.read(b))!=-1) {
        // 2.4 写出数据
        fos.write(b, 0 , len);
    }
    // 3.关闭资源
    fos.close();
    fis.close();
```

### 字符输入流

顶级父类：Reader类->FileReader类

#### 构造方法

```java
File file=new File("a.txt");
FileReader fr=new FileReader(file);

FileReader fr2 = new FileReader("b.txt");
```

#### 读取字符数据

```java
File file=new File("a.txt");
int len;
char[]ch = new char[2];
FileReader fr=new FileReader(file);
while((len=fr.read(ch))!=-1){
    System.out.println(new String(ch,0,len));//获取有效的字符
}
//黑马 程序 员
```

------

### 字符输出流

顶级父类Writer类->FileWriter类

#### 构造方法

```java
File file = new File("a.txt");
FileWriter fw = new FileWriter(file);
FileWriter fw2 = new FileWriter("b.txt");
//若文件路径下不存在该名称的文件名，则创建
```

#### 写出数据

```java
FileWriter fw = new FileWriter("fw.txt");
fw.write(97);//a
fw.write('b');//ab
fw.write("cde");//abcde
fw.flush();
char[] ch = "hijk".toCharArray();
fw.write(ch,0,3);//abcdehij
fw.flush();
String str = "klmn";//abcdehijkl
fw.write(str,0,2);
fw.close();
//调用了close()方法后即关闭了输出流，不能再使用write继续写，会抛出异常
//因此为既想写出数据，又想继续使用流，需要使用flush()方法
```

**tips：字符流，只能操作文本文件，不能操作图片，视频等非文本文件。**

**当我们单纯读或者写文本文件时  使用字符流 其他情况使用字节流**

------

## **IO异常处理**

### JDK7之前的处理方式

在实际开发中，常使用try...catch...finally的代码块进行IO的处理，如下

```java
FileWriter fw = null;
try{
    fw = new FileWriter("fw.txt");
    fw.write("IOtest");
}catch (IOException e){
    e.printStackTrace();
}
finally {
    try{
        if(fw!=null){
            fw.close();
        }
    }catch (IOException e){
        e.printStackTrace();
    }
}
```

### 待补充



------

## **属性集**

### 常用方法汇总

```java
Properties properties = new Properties();
properties.setProperty("filename","a.txt");
properties.setProperty("length","20000000");
properties.setProperty("location","/Users/alan/javacode_folder");
System.out.println(properties);
//{filename=a.txt, length=20000000,location=/Users/alan/javacode_folder}
System.out.println(properties.getProperty("filename"));
System.out.println(properties.getProperty("length"));
System.out.println(properties.getProperty("location"));
//a.txt  20000000  /Users/alan/javacode_folder
Set<String> strings = properties.stringPropertyNames();
for(String key:strings){
    System.out.println(key+"---"+properties.getProperty(key));
}
/*filename---a.txt
length---20000000
location---/Users/alan/javacode_folder */

```

### 与流相关的方法

```java
//读取字节输入流中的键值对
/*
filename=a.txt
length=209385038
location=D:\a.txt  可用空格冒号等号进行分隔
*/
Properties pro = new Properties();
pro.load(new FileInputStream("fw.txt"));
Set<String>strings = pro.stringPropertyNames();
for(String key:strings){
    System.out.println(key+"----"+pro.getProperty(key));
}
```

------

## **更强大的流**

### 缓冲流

#### 字节缓冲流

**BufferedInputStream**&**BufferedOutputStream**

##### 构造方法

```java
BufferedInputStream bis = new BufferedInputStream(new FileInputStream("a.txt"));//字节输入缓冲流
BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("bos.txt"));//字节输出缓冲流
```

##### 效率测试

```java
long start = System.currentTimeMillis();
try(//这里注意
    BufferedInputStream bis = new BufferedInputStream(new FileInputStream("fate.epub"));
    BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("copy.epub"));
){
    int len;
    byte[]bytes = new byte[8*1024];//采用一次读取一个数组的方法，效率更快
    while((len=bis.read(bytes))!=-1){
        bos.write(bytes,0,len);
    }
}catch (IOException e){
    e.printStackTrace();
}
long end = System.currentTimeMillis();
System.out.println("共用时"+(end-start)+"毫秒");//70ms左右，远快于仅仅使用IOstream流
```

#### 字符缓冲流

**BufferedReader**&**BufferedWriter**

与字节缓冲流类似但其特有方法有 readLine()和newLine()

```java
BufferedReader br = new BufferedReader(new FileReader("a.txt"));
String line = null;
while((line=br.readLine())!=null){
    System.out.println(line);
}
br.close();
/*一次读取一行
aaaaaaaaaaa
Bbbbbbbb
Cccccccccccccc
dddddddddddddddddd
*/
```

```java
BufferedWriter bw = new BufferedWriter(new FileWriter("out.txt"));
bw.write("黑马");
bw.newLine();//实现换行
bw.write("程序");
bw.newLine();
bw.write("员");
bw.close();
```

#####  综合使用

```java
//对已存在txt文件进行内容排序
HashMap<String,String> hm = new HashMap<>();
BufferedReader br = new BufferedReader(new FileReader("b.txt"));
BufferedWriter bw = new BufferedWriter(new FileWriter("newb.txt"));
String line = null;
while((line=br.readLine())!=null){
    String []split = line.split("\\.");
    hm.put(split[0],split[1]);
}
br.close();
for(int i=1;i<hm.size();i++){
    String key= String.valueOf(i);
    String value = hm.get(key);
    bw.write(key+"."+value);
    bw.newLine();
}
bw.close();
```

------



### 转换流

#### InputStreamReader

==Mac系统中默认的文件编码是UTF-8编码，与idea的环境一致，所以在读取汉字类型的文件信息时不需要转化，这一点与教程中windows不同==

```java
String filename = "a.txt";
    InputStreamReader isr = new InputStreamReader(new FileInputStream(filename),"GBK");
    InputStreamReader isr2 = new InputStreamReader(new FileInputStream(filename),"UTF-8");//默认也为UTF-8
    int read;
    while((read=isr.read())!=-1){
        System.out.println((char)read);
    }//���
    isr.close();
    System.out.println("//////////////");
    while((read=isr2.read())!=-1){
        System.out.println((char)read);
    }//大家好
    isr2.close();
}
```

#### OutputStreamWriter

==UTF-8编码的汉字一个汉字占3个字节，GBK编码的汉字一个汉字占2个字节==

```java
OutputStreamWriter osw1 = new OutputStreamWriter(new FileOutputStream("out1.txt"), "UTF-8");
    OutputStreamWriter osw2 = new OutputStreamWriter(new FileOutputStream("out2.txt"), "GBK");
    osw1.write("你们好");//文件大小显示为9字节
    osw2.write("你们好");//文件大小显示为6字节
    osw1.close();
    osw2.close();
}
```

![image-20190817203320398](/Users/alan/Library/Application Support/typora-user-images/image-20190817203320398.png)	

#### 综合练习

**将GBK格式编码的文件转换为UTF-8格式编码的文件**

1.使用InputStreamReader读取

2.使用OutputStreamWriter写出

3.释放

```java
		String filename1 = "out2.txt";
    String filename2 = "newout2.txt";
    InputStreamReader isr = new InputStreamReader(new FileInputStream(filename1),"GBK");
    OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream(filename2),"UTF-8");
    char[]cbuf = new char[1024];
    int len;
    while((len=isr.read(cbuf))!=-1){
       osw.write(cbuf,0,len);
    }
    osw.close();
    isr.close();
}
```

### 序列化

#### ObjectOutputStream

```java
public class Employee implements Serializable {
    public String name;
    public String address;
    public transient int age;
    public void addressCheck() {
        System.out.println("Address  check : " + name + " -- " + address);
    }
}
```

```java
    Employee employee = new Employee();
    employee.name = "张大汗";
    employee.address="济南";
    employee.age = 20;
    try{
        ObjectOutputStream ops = new ObjectOutputStream(new FileOutputStream("employee.txt"));
        ops.writeObject(employee);
        ops.close();
        System.out.println("Serialized data is saved");
    }catch (IOException e){
        e.printStackTrace();
    }
}
```

#### ObjectInputStream

```java
public class DeserializeDemo {
   public static void main(String [] args)   {
        Employee e = null;
        try {		
             // 创建反序列化流
             FileInputStream fileIn = new FileInputStream("employee.txt");
             ObjectInputStream in = new ObjectInputStream(fileIn);
             // 读取一个对象
             e = (Employee) in.readObject();
             // 释放资源
             in.close();
             fileIn.close();
        }catch(IOException i) {
             // 捕获其他异常
             i.printStackTrace();
             return;
        }catch(ClassNotFoundException c)  {
        	// 捕获类找不到异常
             System.out.println("Employee class not found");
             c.printStackTrace();
             return;
        }
        // 无异常,直接打印输出
        System.out.println("Name: " + e.name);	// zhangsan
        System.out.println("Address: " + e.address); // beiqinglu
        System.out.println("age: " + e.age); // 0
    }
}
```



==待补充==

------

### 打印流

**使用PrintStream改变打印流向**

```java
System.out.println(97);
PrintStream ps = new PrintStream("ps.txt");
System.setOut(ps);
System.out.println(97);
//在ps.txt文件中打印输出了 97
```

------

## **TCP通信**

![image-20190822163942197](/Users/alan/Library/Application Support/typora-user-images/image-20190822163942197.png)

1. 服务端】启动,创建ServerSocket对象，等待连接。
2. 【客户端】启动,创建Socket对象，请求连接。
3. 【服务端】接收连接,调用accept方法，并返回一个Socket对象。
4. 【客户端】Socket对象，获取OutputStream，向服务端写出数据。
5. 【服务端】Scoket对象，获取InputStream，读取客户端发送的数据。

> 客户端向服务端发送数据成功

6.【服务端】Socket对象，获取OutputStream，向客户端回写数据。

7.【客户端】Scoket对象，获取InputStream，解析回写数据。

8.【客户端】释放资源，断开连接。

> 服务端向客户端回写数据

```java
//TCPServer
public static void main(String[] args) throws IOException {
    ServerSocket ss = new ServerSocket(1500);
    Socket socket = ss.accept();
    InputStream inputStream = socket.getInputStream();
    byte[] bytes = new byte[1024];
    int len = inputStream.read(bytes);
    String msg = new String(bytes,0,len);
    System.out.println(msg);
    System.out.println("--------回写数据");
    OutputStream outputStream = socket.getOutputStream();
    outputStream.write("我很好，谢谢你".getBytes());
    outputStream.close();
    inputStream.close();
    socket.close();
    ss.close();
}
//TCPClient
public static void main(String[] args) throws IOException {
        Socket socket = new Socket("127.0.0.1",1500);
        OutputStream os = socket.getOutputStream();
        os.write("你好！".getBytes());
        InputStream inputStream = socket.getInputStream();
        byte []b = new byte[1024];
        int len = inputStream.read(b);
        String msg = new String(b,0,len);
        System.out.println(msg);
        inputStream.close();
        os.close();
        socket.close();
    }
```

**实例：文件上传**

```java
//FileUPload_Client
public static void main(String[] args) throws IOException {
    BufferedInputStream bis = new BufferedInputStream(new FileInputStream("test.png"));
    Socket socket = new Socket("localhost",4000);
    BufferedOutputStream bos = new BufferedOutputStream(socket.getOutputStream());
    byte[]b = new byte[1024*8];
    int len;
    while((len=bis.read(b))!=-1){
        bos.write(b,0,len);
        bos.flush();
    }
    System.out.println("文件发送完成");
    bos.close();
    bis.close();
    socket.close();
    System.out.println("文件上传完毕");
}
```

```java
//FileUpload_Server
public static void main(String[] args) throws IOException {
    System.out.println("服务器  启动.......");
    ServerSocket ss = new ServerSocket(4000);
    Socket socket = ss.accept();
    BufferedInputStream bis = new BufferedInputStream(socket.getInputStream());
    BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("copy.png"));
    byte[]b = new byte[1024*8];
    int len;
    while((len=bis.read(b))!=-1){
        bos.write(b,0,len);
    }
    bos.close();
    bis.close();
    socket.close();
    System.out.println("文件已保存");
}


//优化实现
public static void main(String[] args) throws IOException {
        System.out.println("服务器 启动.....  ");
        // 1. 创建服务端ServerSocket
        ServerSocket serverSocket = new ServerSocket(6666);
      	// 2. 循环接收,建立连接
        while (true) {
            Socket accept = serverSocket.accept();
          	/* 
          	3. socket对象交给子线程处理,进行读写操作
               Runnable接口中,只有一个run方法,使用lambda表达式简化格式
            */
            new Thread(() -> {
                try (
                    //3.1 获取输入流对象
                    BufferedInputStream bis = new BufferedInputStream(accept.getInputStream());
                    //3.2 创建输出流对象, 保存到本地 .
                    FileOutputStream fis = new FileOutputStream(System.currentTimeMillis() + ".jpg");
                    BufferedOutputStream bos = new BufferedOutputStream(fis);) {
                    // 3.3 读写数据
                    byte[] b = new byte[1024 * 8];
                    int len;
                    while ((len = bis.read(b)) != -1) {
                      bos.write(b, 0, len);
                    }
                    //4. 关闭 资源
                    bos.close();
                    bis.close();
                    accept.close();
                    System.out.println("文件上传已保存");
                } catch (IOException e) {
                  	e.printStackTrace();
                }
            }).start();
        }
    }
```

## **基础加强**

```
1. Junit单元测试
2. 反射
3. 注解
```

### Junit单元测试：

```
* 测试分类：
	1. 黑盒测试：不需要写代码，给输入值，看程序是否能够输出期望的值。
	2. 白盒测试：需要写代码的。关注程序具体的执行流程。

* Junit使用：白盒测试
	* 步骤：
		1. 定义一个测试类(测试用例)
			* 建议：
				* 测试类名：被测试的类名Test		CalculatorTest
				* 包名：xxx.xxx.xx.test		cn.itcast.test

		2. 定义测试方法：可以独立运行
			* 建议：
				* 方法名：test测试的方法名		testAdd()  
				* 返回值：void
				* 参数列表：空参

		3. 给方法加@Test
		4. 导入junit依赖环境

	* 判定结果：
		* 红色：失败
		* 绿色：成功
		* 一般我们会使用断言操作来处理结果
			* Assert.assertEquals(期望的结果,运算的结果);

	* 补充：
		* @Before:
			* 修饰的方法会在测试方法之前被自动执行
		* @After:
			* 修饰的方法会在测试方法执行之后自动被执行
```

### 反射：框架设计的灵魂

```
* 框架：半成品软件。可以在框架的基础上进行软件开发，简化编码
* 反射：将类的各个组成部分封装为其他对象，这就是反射机制
	* 好处：
		1. 可以在程序运行过程中，操作这些对象。
		2. 可以解耦，提高程序的可扩展性。
```

```
* 获取Class对象的方式：
	1. Class.forName("全类名")：将字节码文件加载进内存，返回Class对象
		* 多用于配置文件，将类名定义在配置文件中。读取文件，加载类
	2. 类名.class：通过类名的属性class获取
		* 多用于参数的传递
	3. 对象.getClass()：getClass()方法在Object类中定义着。
		* 多用于对象的获取字节码的方式

	* 结论：
		同一个字节码文件(*.class)在一次程序运行过程中，只会被加载一次，不论通过哪一种方式获取的Class对象都是同一个。
```

```
* Class对象功能：
	* 获取功能：
		1. 获取成员变量们
			* Field[] getFields() ：获取所有public修饰的成员变量
			* Field getField(String name)   获取指定名称的 public修饰的成员变量

			* Field[] getDeclaredFields()  获取所有的成员变量，不考虑修饰符
			* Field getDeclaredField(String name)  
		2. 获取构造方法们
			* Constructor<?>[] getConstructors()  
			* Constructor<T> getConstructor(类<?>... parameterTypes)  

			* Constructor<T> getDeclaredConstructor(类<?>... parameterTypes)  
			* Constructor<?>[] getDeclaredConstructors()  
		3. 获取成员方法们：
			* Method[] getMethods()  
			* Method getMethod(String name, 类<?>... parameterTypes)  

			* Method[] getDeclaredMethods()  
			* Method getDeclaredMethod(String name, 类<?>... parameterTypes)  

		4. 获取全类名	
			* String getName()  
```

```
* Field：成员变量
	* 操作：
		1. 设置值
			* void set(Object obj, Object value)  
		2. 获取值
			* get(Object obj) 

		3. 忽略访问权限修饰符的安全检查
			* setAccessible(true):暴力反射
```



```
* Constructor:构造方法
	* 创建对象：
		* T newInstance(Object... initargs)  

		* 如果使用空参数构造方法创建对象，操作可以简化：Class对象的newInstance方法
```

```
* Method：方法对象
	* 执行方法：
		* Object invoke(Object obj, Object... args)  

	* 获取方法名称：
		* String getName:获取方法名
```

```
* 案例：
	* 需求：写一个"框架"，不能改变该类的任何代码的前提下，可以帮我们创建任意类的对象，并且执行其中任意方法
		* 实现：
			1. 配置文件
			2. 反射
		* 步骤：
			1. 将需要创建的对象的全类名和需要执行的方法定义在配置文件中
			2. 在程序中加载读取配置文件
			3. 使用反射技术来加载类文件进内存
			4. 创建对象
			5. 执行方法
```

### 注解：

```
* 概念：说明程序的。给计算机看的
* 注释：用文字描述程序的。给程序员看的

* 定义：注解（Annotation），也叫元数据。一种代码级别的说明。它是JDK1.5及以后版本引入的一个特性，与类、接口、枚举是在同一个层次。它可以声明在包、类、字段、方法、局部变量、方法参数等的前面，用来对这些元素进行说明，注释。
* 概念描述：
	* JDK1.5之后的新特性
	* 说明程序的
	* 使用注解：@注解名称
```

​	

```
* 作用分类：
	①编写文档：通过代码里标识的注解生成文档【生成文档doc文档】
	②代码分析：通过代码里标识的注解对代码进行分析【使用反射】
	③编译检查：通过代码里标识的注解让编译器能够实现基本的编译检查【Override】
```

```
* JDK中预定义的一些注解
	* @Override	：检测被该注解标注的方法是否是继承自父类(接口)的
	* @Deprecated：该注解标注的内容，表示已过时
	* @SuppressWarnings：压制警告
		* 一般传递参数all  @SuppressWarnings("all")

* 自定义注解
	* 格式：
		元注解
		public @interface 注解名称{
			属性列表;
		}

	* 本质：注解本质上就是一个接口，该接口默认继承Annotation接口
		* public interface MyAnno extends java.lang.annotation.Annotation {}

	* 属性：接口中的抽象方法
		* 要求：
			1. 属性的返回值类型有下列取值
				* 基本数据类型
				* String
				* 枚举
				* 注解
				* 以上类型的数组

			2. 定义了属性，在使用时需要给属性赋值
				1. 如果定义属性时，使用default关键字给属性默认初始化值，则使用注解时，可以不进行属性的赋值。
				2. 如果只有一个属性需要赋值，并且属性的名称是value，则value可以省略，直接定义值即可。
				3. 数组赋值时，值使用{}包裹。如果数组中只有一个值，则{}可以省略
	
	* 元注解：用于描述注解的注解
		* @Target：描述注解能够作用的位置
			* ElementType取值：
				* TYPE：可以作用于类上
				* METHOD：可以作用于方法上
				* FIELD：可以作用于成员变量上
		* @Retention：描述注解被保留的阶段
			* @Retention(RetentionPolicy.RUNTIME)：当前被描述的注解，会保留到class字节码文件中，并被JVM读取到
		* @Documented：描述注解是否被抽取到api文档中
		* @Inherited：描述注解是否被子类继承
```

```
* 在程序使用(解析)注解：获取注解中定义的属性值
	1. 获取注解定义的位置的对象  （Class，Method,Field）
	2. 获取指定的注解
		* getAnnotation(Class)
		//其实就是在内存中生成了一个该注解接口的子类实现对象

	            public class ProImpl implements Pro{
	                public String className(){
	                    return "cn.itcast.annotation.Demo1";
	                }
	                public String methodName(){
	                    return "show";
	                }
	            }
	3. 调用注解中的抽象方法获取配置的属性值

```

```
* 案例：简单的测试框架
* 小结：
	1. 以后大多数时候，我们会使用注解，而不是自定义注解
	2. 注解给谁用？
		1. 编译器
		2. 给解析程序用
	3. 注解不是程序的一部分，可以理解为注解就是一个标签
```