```java
//反转输出
while(x!=0){
		int temp = x%10;
    count = count*10 +temp;
    x/=10;
}
```

```java
String str = x+"";//整型转换为字符串
StringBuffer sb = new StringBuffer(str).reverse(); //String to StringBuffer &reverse
String new_str = sb.toString(); //StringBuffer to String
str.equals(new_str);//字符串比较函数
String strs = str.split(" ");//按空格进行分割
str.replace(" ","hh"); 字符串中的替换函数
```

```java
Math.max()//求大
Math.min()//求小
Integer.MAX_VALUE//整型最大值
Integer.MIN_VALUE//整型最小值
```

```java
Character.isLetterOrDigit(c)//判断是否为字母或数字
Character.toLowerCase(c)//大写字母转换为小写字母
int n = Integer.parseInt(ops[i]);//字符串转换为整型变量
Arrays.sort(nums)//对数组进行排序
char []words = word.toCharArray();//String转换为char类型数组
String str = new String(char[],start,end)//由一个char数组创建一个字符串
```

```java
LinkedList<Node> stack = new LinkedList<Node>();//用链表的形式创建一个stack
stack.poolLast()//返回最后一个元素值
Set<Integer> s = new HashSet<>();//定义一个HashSet
```

