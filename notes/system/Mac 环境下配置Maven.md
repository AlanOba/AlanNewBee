# Mac 环境下配置Maven

1.官网下载Maven

http://maven.apache.org/download.cgi

2.配置环境变量

​	1.打开终端输入 vim ~/.bash_profile 

​	==ps：出现错误时：==![image-20200227160510359](/Users/alan/Library/Application Support/typora-user-images/image-20200227160510359.png)

**解决方法**

- 输入 q（退出）
- 然后在终端出入：rm -f ~/.bash_profile.swp
- 最后你在终端输入 source ~/.bash_profile就可以了

2.按i进入insert模式

export MAVEN_HOME=/Users/kun/Desktop/midongtools/apache-maven-3.5.0 

export PATH=$PATH:$MAVEN_HOME/bin

PS:（可以将文件直接拖拽至终端内文件路径便可显示出来）

3.按ese退出后 输入wq保存并退出

4.输入source .bash_profile使保存生效

5.输入mvn -v 测试安装结果