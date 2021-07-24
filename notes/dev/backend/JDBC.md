[TOC]

## **增删改**

```java
public class jdbcTest {
    public static void main(String[] args) {
        Connection c = null;
        Statement s  = null;
        try{
            Class.forName("com.mysql.jdbc.Driver");
            System.out.println("数据驱动加载成功！");
             c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
            System.out.println("连接成功，获取的连接对象为  "+c);
            s  = c.createStatement();
            System.out.println("获取Statement对象  "+ s);
            String sql = "insert into job values(7,"+"'鼓励员',"+"'振奋程序员')"  ;
          //  String sql2 =  "insert into job values(6,'鼓励员','振奋程序员')" ;
            s.execute(sql);
            System.out.println("执行插入语句成功");
        }catch(ClassNotFoundException e){
            e.printStackTrace();
        }
        catch (SQLException e){
            e.printStackTrace();
        }finally{
            if(s!=null){
                try{
                    s.close();
                }
                catch (SQLException e){
                    e.printStackTrace();
                }
            }
            if(c!=null){
                try{
                    c.close();
                }catch (SQLException e){
                    e.printStackTrace();
                }
            }
        }
    }
}
```

## **使用try-with-resource的方式自动关闭连接**

```java
public class jdbcTest {
    public static void main(String[] args) {
        try{
            Class.forName("com.mysql.jdbc.Driver");
        }catch (ClassNotFoundException e){
            e.printStackTrace();
        }
        try(
            Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
            Statement s = c.createStatement();
        ){
            String sql = "insert into job values(8,'高级技工','维修设备')";
            s.execute(sql);
            System.out.println("数据插入成功");
        }catch (SQLException e){
            e.printStackTrace();
        }
    }
}
```

**查**

```java
public class test_for_select {
    public static void main(String[] args) {
        try{
            Class.forName("com.mysql.jdbc.Driver");
        }catch(ClassNotFoundException e){
            e.printStackTrace();
        }
        try(
                Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
                Statement s = c.createStatement();)
        {
            String sql =  "select * from job";
            ResultSet rs = s.executeQuery(sql);
            while (rs.next()) {
                int id =  rs.getInt(1);
                String name = rs.getString(2);
                String description = rs.getString(3);
               // System.out.println(id+"   "+ name+"    "+ description); 这样写格式不工整
                System.out.printf("%d\t%s\t%s%n",id,name,description);
            }
        }catch (SQLException e){
            e.printStackTrace();
        }
    }
}
```

## **利用查询判断用户输入账户密码是否正确**

```java
public class test_for_select {
    public static void main(String[] args) {
        try{
            Class.forName("com.mysql.jdbc.Driver");
        }catch(ClassNotFoundException e){
            e.printStackTrace();
        }
        try(
                Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
                Statement s = c.createStatement();)
        {
            String name = "dashen";
            String password = "thisispassword";
            String sql =  "select * from user u where u.name = '"+name +"'"+" and u.password = '"+ password+"'";
            System.out.println(sql);
            ResultSet rs = s.executeQuery(sql);
            if(rs.next()){
                System.out.println("账号密码正确");
            }
            else
            {
                System.out.println("账号密码错误");
            }
        }catch (SQLException e){
            e.printStackTrace();
        }
    }
}
```

## **分页查询**

```java
public static void main(String[] args) {
    list(0,5);
    System.out.println("-------------------");
    list(5,5);
    System.out.println("-------------------");
    list(10,5);
}
public static void list(int start,int count){
    try{
        Class.forName("com.mysql.jdbc.Driver");
    }catch(ClassNotFoundException e){
        e.printStackTrace();
    }
    try(
            Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
            Statement s = c.createStatement();)
    {
        String sql = "select * from soldier limit " +  start+","+count+";" ;
        System.out.println(sql);
        ResultSet rs = s.executeQuery(sql);
        int id;
        String name;
        while(rs.next()){
           id = rs.getInt(1);
           name = rs.getString(2);
            System.out.printf("%d\t%s%n",id,name);
        }

    }catch (SQLException e){
        e.printStackTrace();
    }
}
}
```

## **使用preparedStatement---优化Statement**

```java
public class test_for_preparedStatement {
    public static void main(String[] args) {
        try{
            Class.forName("com.mysql.jdbc.Driver");
        }catch (ClassNotFoundException e){
            e.printStackTrace();
        }
        String sql = "insert into job values(?,?,?)";
        try(
                Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
                PreparedStatement ps = c.prepareStatement(sql);
                ){
                ps.setInt(1,8);
                ps.setString(2,"司机");
                ps.setString(3,"送大boss上下班");
                ps.execute();
        }catch (SQLException e){
            e.printStackTrace();
        }
    }
}
```

## **获取自增长的数据-id**

```java
String sql = "insert into hero values(null,?,?,?)";
try(
        Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
        PreparedStatement ps = c.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS);//后面的参数可以不加
        ){
        ps.setString(1,"盖伦");
        ps.setFloat(2,1000);
        ps.setInt(3,200);
        ps.execute();
        ResultSet rs = ps.getGeneratedKeys();
        if(rs.next()){
            int id =  rs.getInt(1);
            System.out.println(id);
        }
}catch (SQLException e){
    e.printStackTrace();
}
```

## **获取服务器表的元数据**

```java
DatabaseMetaData dbmd = c.getMetaData();

// 获取数据库服务器产品名称
System.out.println("数据库产品名称:\t"+dbmd.getDatabaseProductName());
// 获取数据库服务器产品版本号
System.out.println("数据库产品版本:\t"+dbmd.getDatabaseProductVersion());
// 获取数据库服务器用作类别和表名之间的分隔符 如test.user
System.out.println("数据库和表分隔符:\t"+dbmd.getCatalogSeparator());
// 获取驱动版本
System.out.println("驱动版本:\t"+dbmd.getDriverVersion());

System.out.println("可用的数据库列表：");
// 获取数据库名称
ResultSet rs = dbmd.getCatalogs();

while (rs.next()) {
    System.out.println("数据库名称:\t"+rs.getString(1));
}
```

## **事务的使用--删除数据库数据**

```java
public class jdbcTest2 {
    public static void main(String[] args) {
        try{
            Class.forName("com.mysql.jdbc.Driver");
        }catch (ClassNotFoundException e){
            e.printStackTrace();
        }
        String sql = "select * from hero limit 0,10";
        try(
                Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
                PreparedStatement ps = c.prepareStatement(sql);
                Statement s = c.createStatement();
                ){
            Scanner scanner = new Scanner(System.in);
            c.setAutoCommit(false);
            ps.execute();
            ResultSet rs = ps.getResultSet();
            while(rs.next()){
                int id = rs.getInt(1);
                System.out.println("试图删除id=" + id+ " 的数据");
                String sql2 = "delete from hero where id = " + id;
                s.execute(sql2);
            }
            while(true){
                System.out.println("是否要删除数据(Y/N)");
                String reply = scanner.next();
                if(reply.equals("Y")){
                    c.commit();
                    System.out.println("提交删除");
                    break;
                }
                else if(reply.equals("N")){
                    System.out.println("放弃删除");
                    break;
                }
            }
        }catch (SQLException e){
            e.printStackTrace();
        }
    }
}
```

## **ORM(Object Relationship Database Mapping)** 

```java
public static void main(String[] args) {
    hero h = get(14);
    System.out.printf("%d\t%s\t%.0f\t%d\n",h.id,h.name,h.hp,h.damage);
}
public static hero get(int id){
    hero h = null;
    try {
        Class.forName("com.mysql.jdbc.Driver");
    } catch (ClassNotFoundException e) {
        e.printStackTrace();
    }

    try (Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root", "nulixuexi1234");
         Statement statement = c.createStatement();) {
        String sql = "select * from hero where id = " + id;
        statement.execute(sql);
        ResultSet rs = statement.getResultSet();
        if(rs.next()) {
             h = new hero();
            String name = rs.getString(2);
            float hp = rs.getFloat(3);
            int damage = rs.getInt(4);
            h.id = id;
            h.name = name;
            h.hp = hp;
            h.damage = damage;
        }

    } catch (SQLException e) {
        // TODO Auto-generated catch block
        e.printStackTrace();
    }
    return h;
}
```

## **几个常见的ORM方法实现**

```java
public static void main(String[] args) {
        /*hero newhero1 = new hero(3,"火焰猛男",1500,100);
        add(newhero1);*/// 插入
        /*hero newhero2 = new hero(3,"火焰猛男",1500,100);
        delete(newhero2);*///删除
        /*hero newhero3 = new hero(14,"无双剑姬",2000,400);
        update(newhero3);*/ //更新
        List<hero> list = list();
        for(hero h : list){
            System.out.println(h.toString());
        }//遍历
        
}
    public static void add(hero h){
        try{
            Class.forName("com.mysql.jdbc.Driver");
        }catch (ClassNotFoundException e){
            e.printStackTrace();
        }
        String sql = "insert into hero values(?,?,?,?)";
        try(Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
            PreparedStatement ps = c.prepareStatement(sql);
        ){

           int  id = h.id;
           String name = h.name;
           float hp = h.hp;
           int damage = h.damage;
           ps.setInt(1,id);
           ps.setString(2,name);
           ps.setFloat(3,hp);
           ps.setInt(4,damage);
           ps.execute();
           System.out.println("插入成功！");

        }catch (SQLException e ){
            e.printStackTrace();
        }

    }
    public static void delete(hero h){
        try{
            Class.forName("com.mysql.jdbc.Driver");
        }catch (ClassNotFoundException e){
            e.printStackTrace();
        }
        int id = h.id;
        String sql = "delete from hero where id = " + id;
        try(Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
            PreparedStatement ps = c.prepareStatement(sql);
        ){
            ps.execute();
            System.out.println("删除成功！");
        }catch (SQLException e){
            e.printStackTrace();
        }
    }
    public static void update(hero h){
        try{
            Class.forName("com.mysql.jdbc.Driver");
        }catch (ClassNotFoundException e){
            e.printStackTrace();
        }
        int id = h.id;
        String name = h.name;
        float hp = h.hp;
        int damage = h.damage;

        try(Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
            Statement s = c.createStatement();){
            String sql = "update hero set name = '" + name + "' ,hp = " + hp + " ,damage = " + damage + " where id = " + id + ";";
            System.out.println(sql);
            s.execute(sql);
            System.out.println("更新完毕!");
        }catch (SQLException e ){
            e.printStackTrace();
        }
    }
        public static List<hero> list(){
            try{
                Class.forName("com.mysql.jdbc.Driver");
            }catch (ClassNotFoundException e){
                e.printStackTrace();
            }
            List<hero>heros = new ArrayList<>();
            String sql  = "select * from hero;";
            int count = 0;
            try(Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
                Statement s = c.createStatement();){
                s.execute(sql);
                ResultSet rs = s.getResultSet();
                while(rs.next()){
                    int id = rs.getInt(1);
                    String name = rs.getString(2);
                    float hp  = rs.getFloat(3);
                    int damage = rs.getInt(4);
                    hero h = new hero(id,name,hp,damage);
                    heros.add(h);
                    count++;
                    System.out.println("已成功将"+count+"条数据从数据库加入到list!");
                }
            }catch (SQLException e){
                e.printStackTrace();
            }
            return heros;
        }
```

## **DAO(Data Access Object)数据库访问对象**

==数据库相关的操作放在这个类里，其他地方看不到JDBC代码==

```java
public interface DAO {
    public void add(hero h);
    public void update(hero h);
    public void delete(int id);
    public hero get(int id);
    public List<hero> list();
    public List<hero> list(int start,int count);
}
```

```java
public class HeroDAO implements DAO {
    public HeroDAO() {
        try{
            Class.forName("com.mysql.jdbc.Driver");
        }catch (ClassNotFoundException e){
            e.printStackTrace();
        }
    }
    public Connection getConnnection()throws SQLException{
        return DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
    }
    public int getTotal(){
        int total = 0;
        try(Connection c = getConnnection();
            Statement s = c.createStatement();){
            String sql = "select * from hero";
            s.execute(sql);
            ResultSet rs = s.getResultSet();
            while(rs.next()){
                total++;
            }
        }catch (SQLException e){
            e.printStackTrace();
        }
        System.out.println("正在查询总英雄数.........");
        return total;
    }
    @Override
    public void add(hero h) {
        String sql = "insert into hero values(?,?,?,?)";
        try(Connection c = getConnnection();
            PreparedStatement ps = c.prepareStatement(sql);) {
            ps.setInt(1,h.id);
            ps.setString(2,h.name);
            ps.setFloat(3,h.hp);
            ps.setInt(4,h.damage);
            ps.execute();
            System.out.println("添加成功");
        }catch (SQLException e){
            e.printStackTrace();
        }

    }

    @Override
    public void update(hero h) {
        String sql = "update hero set name = ?,hp = ?,damage=? where id = ?";
        try(Connection c = getConnnection();
            PreparedStatement ps = c.prepareStatement(sql);) {
            ps.setString(1,h.name);
            ps.setFloat(2,h.hp);
            ps.setInt(3,h.damage);
            ps.setInt(4,h.id);
            ps.execute();
            System.out.println("更新成功");
        }catch (SQLException e){
            e.printStackTrace();
        }
    }
    @Override
    public void delete(int id) {
        String sql = "delete from hero where id = ?";
        try(Connection c = getConnnection();
            PreparedStatement ps = c.prepareStatement(sql)) {
            ps.setInt(1,id);
            ps.execute();
            System.out.println("删除成功");
        }catch (SQLException e){
            e.printStackTrace();
        }
    }
    @Override
    public hero get(int id) {
        hero h = new hero();
        String sql = "select * from hero where id = ?";
        try(Connection c = getConnnection();
            PreparedStatement ps = c.prepareStatement(sql)) {
            ps.setInt(1,id);
            ps.execute();
            ResultSet rs = ps.getResultSet();
            if(rs.next()){
                h.id = rs.getInt(1);
                h.name = rs.getString(2);
                h.hp = rs.getFloat(3);
                h.damage= rs.getInt(4);
                return h;
            }
        }catch (SQLException e){
            e.printStackTrace();
        }
       return null;
    }
    @Override
    public List<hero> list() {
        String sql = "select * from hero";
        List<hero>heros = new ArrayList<>();
        try(Connection c = getConnnection();
            PreparedStatement ps = c.prepareStatement(sql)) {
            ps.execute();
            ResultSet rs = ps.getResultSet();
            while(rs.next()){
                int id = rs.getInt(1);
                String name = rs.getString(2);
                float hp = rs.getFloat(3);
                int damage = rs.getInt(4);
                hero temp = new hero(id,name,hp,damage);
                heros.add(temp);
            }
        }catch (SQLException e){
            e.printStackTrace();
        }
        return heros;
    }

    @Override
    public List<hero> list(int start, int count) {
        List<hero>heros = new ArrayList<>();
        String sql = "select * from hero limit ?,?";
        try(Connection c = getConnnection();
            PreparedStatement ps = c.prepareStatement(sql)) {
            ps.setInt(1,start);
            ps.setInt(2,count);
            ps.execute();
            ResultSet rs = ps.getResultSet();
            while(rs.next()){
                int id = rs.getInt(1);
                String name = rs.getString(2);
                float hp = rs.getFloat(3);
                int damage = rs.getInt(4);
                hero temp = new hero(id,name,hp,damage);
                heros.add(temp);
            }
        }catch (SQLException e){
            e.printStackTrace();
        }
        return heros;
    }
}
```

```java
public class HeroDAOTest {
    public static void main(String[] args) {
        HeroDAO heroDAO = new HeroDAO();
        System.out.println("当前数据库中的英雄总数为:" + heroDAO.getTotal());
        System.out.println("------------------------");
        hero h = new hero(20, "酒桶", 1000, 200);
        heroDAO.add(h);
        System.out.println("------------------------");
        System.out.println("当前数据库中的英雄总数为:" + heroDAO.getTotal());
        System.out.println("------------------------");
        hero newh = new hero(1, "战争女神", 1000, 200);
        heroDAO.update(newh);
        System.out.println("------------------------");
        heroDAO.delete(3);
        System.out.println("------------------------");
        hero h2 = heroDAO.get(14);
        System.out.println(h2.toString());
        System.out.println("------------------------");
        List<hero>heros = heroDAO.list();
        for(hero hh:heros){
            System.out.println(hh.toString());
        }
        System.out.println("------------------------");
        List<hero>limitheros = heroDAO.list(3,4);
        for(hero hh :limitheros){
            System.out.println(hh.toString());
        }
        System.out.println("------------------------");
        System.out.println("当前数据库中的英雄总数为:" + heroDAO.getTotal());
    }
    }
```

## **数据库连接池ConnectionPool**

```java
public class ConnectionPool {
    List<Connection>cs = new ArrayList<>();
    int size;
    public ConnectionPool(int size){
        this.size = size;
        init();
    }//构造函数 初始化连接池内connection的数量限制
   //init() 对连接池进行初始化操作，创建size数量的connection并依次加入到connection链表中
    public void init(){
        try{
            Class.forName("com.mysql.jdbc.Driver");
            for(int i=0;i<size;i++){
                Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
                cs.add(c);
            }
        }catch (ClassNotFoundException e){
            e.printStackTrace();
        }catch (SQLException e){
            e.printStackTrace();
        }
    }
  //获取
    public synchronized Connection getConnection(){
        while(cs.isEmpty()){
            try{
                this.wait();
            }catch (InterruptedException e){
                e.printStackTrace();
            }
        }
        Connection c = cs.remove(0);
        return c;
    }
   //归还
    public synchronized void returnConnection(Connection c){
        cs.add(c);
        this.notifyAll();
    }
}
```

```java
 public class ConnectionPoolTest {
    public static void main(String[] args) {
        ConnectionPool cp = new ConnectionPool(3);
        for (int i = 0; i < 100; i++) {
            new WorkingThread("Working Thread" + i, cp).start();
        }
    }
        static class WorkingThread extends Thread {
            private ConnectionPool cp;

            public WorkingThread(String name, ConnectionPool cp) {
                super(name);
                this.cp = cp;
            }

            public void run() {
                Connection c = cp.getConnection();
                System.out.println(this.getName() + ":\t 获取了一根连接，并开始了工作");
                try (Statement st = c.createStatement()) {
                    Thread.sleep(1000);
                    st.execute("select * from hero");
                } catch (InterruptedException e) {
                    e.printStackTrace();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
                cp.returnConnection(c);
            }
    }
}
```

## **普通线程连接和使用线程连接池的比较**

```java
//传统线程连接
public class TraditionalWorkingThread extends  Thread {
   public void run(){
       try{
           Class.forName("com.mysql.jdbc.Driver");
       } catch (ClassNotFoundException e1) {
           e1.printStackTrace();
       }
       try (Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8",
               "root", "nulixuexi1234");
            Statement s = c.createStatement();){
           String sql = "insert into hero values(null," + "'提莫'" + "," + 313.0f + "," + 50 + ")";
           s.execute(sql);
       }catch (SQLException e){
           e.printStackTrace();
       }
   }
}
```

```java
//线程连接池连接
public class connectionpoolWorkingThread extends Thread {
    private ConnectionPool cp;
    public connectionpoolWorkingThread(ConnectionPool cp){
        this.cp = cp;
    }
    public void run(){
        Connection c = cp.getConnection();
        try(Statement s = c.createStatement();){
            for(int i=0;i<TestConnectionPool.insertTime;i++){
                String sql = "insert into hero values(null," + "'提莫'" + "," + 313.0f + "," + 50 + ")";
                s.execute(sql);
            }
        }catch (SQLException e){
            e.printStackTrace();
        }
        cp.returnConnection(c);
    }
}
```

```java
//线程连接池定义
public class ConnectionPool {
    List<Connection>cs = new ArrayList<>();
    int size;
    public ConnectionPool(int size){
        this.size = size;
        init();
    }
    public void init(){
        try{
            Class.forName("com.mysql.jdbc.Driver");
            for(int i=0;i<size;i++){
                Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/mydatabase?characterEncoding=UTF-8","root","nulixuexi1234");
                cs.add(c);
            }
        }catch (ClassNotFoundException e){
            e.printStackTrace();
        }catch (SQLException e){
            e.printStackTrace();
        }
    }
    public synchronized Connection getConnection(){
        while(cs.isEmpty()){
            try{
                this.wait();
            }catch (InterruptedException e){
                e.printStackTrace();
            }
        }
        Connection c = cs.remove(0);
        return c;
    }
    public synchronized void returnConnection(Connection c){
        cs.add(c);
        this.notifyAll();
    }
}
```

```java
//测试代码
public class TestConnectionPool {
    public static int insertTime = 1;
    public static int Threadnumber = 100;

    public static void main(String[] args) {
        traditionalWay();
        connectionpoolWay();
    }
    private static void traditionalWay(){
        System.out.println("开始传统方式插入数据测试");
        long start = System.currentTimeMillis();
        List<Thread> ts = new ArrayList<>();
        for(int i=0;i<Threadnumber;i++){
            Thread t = new TraditionalWorkingThread();
            t.start();
            ts.add(t);
        }
        for(Thread t:ts){
            try{
                t.join();
            }catch (InterruptedException e){
                e.printStackTrace();
            }
        }
        long end = System.currentTimeMillis();
        System.out.printf("使用传统方式，启动%d条线程，每个线程插入%d条数据，一共耗时%d 毫秒%n",Threadnumber,insertTime,end-start);
    }
    private static void connectionpoolWay(){
        ConnectionPool cp = new ConnectionPool(10);
        System.out.println("开始使用数据库连接池方式插入数据测试");
        long start  = System.currentTimeMillis();
        List<Thread> ts = new ArrayList<>();
        for(int i=0;i<Threadnumber;i++){
            Thread t = new connectionpoolWorkingThread(cp);
            t.start();
            ts.add(t);
        }
        for(Thread t:ts){
            try{
                t.join();
            }catch (InterruptedException e){
                e.printStackTrace();
            }
        }
        long end = System.currentTimeMillis();

        System.out.printf("使用连接池方式，启动%d条线程，每个线程插入%d条数据，一共耗时%d 毫秒%n",Threadnumber,insertTime,end-start);
    }

}
```

```java
//结果
/*开始传统方式插入数据测试
使用传统方式，启动100条线程，每个线程插入1条数据，一共耗时530 毫秒
开始使用数据库连接池方式插入数据测试
使用连接池方式，启动100条线程，每个线程插入1条数据，一共耗时17 毫秒*/
```

