[TOC]



## 《**Research on IDS Alert Aggregation Based on Improved Quantum- behaved Particle Swarm Optimization**》

1.基于属性相似度的方法进行警报聚合

2.模糊隶属函数完成初始警报聚合

3.使用粒子群优化算法对参数进行优化-----各个属性字段的权重、聚合的阈值

![image-20210204135233226](/Users/alan/Library/Application Support/typora-user-images/image-20210204135233226.png)

![image-20210204135256606](/Users/alan/Library/Application Support/typora-user-images/image-20210204135256606.png)

![image-20210204135328449](/Users/alan/Library/Application Support/typora-user-images/image-20210204135328449.png)

![image-20210204135341699](/Users/alan/Library/Application Support/typora-user-images/image-20210204135341699.png)

## **《一种基于信息熵的IDS告警预处理方法》**

![image-20210204141300778](/Users/alan/Library/Application Support/typora-user-images/image-20210204141300778.png)

1.本文的告警预处理包含两个方面：误告警去除（新知识和新技术，可以深究）和告警聚合。

2.误告警去除阶段：

​	 1.总体思想是计算每一条告警和误告警(应该是事先定义好的或已知的)的互雷尼信息熵，是否超过阈值来判定该告警是误告警还是真实告警。

​	2.因此关键点就是在于求告警的特征信息熵，本文中特征信息熵由四部分组成，分别是告警密度、告警周期、同一源ip对应的目的ip数、攻击源威胁度，每一部分是由其熵组成的。最后对这一个四维向量求归一化来限定值的范围。对四个特征的计算方法暂时不深究。

3.告警聚合阶段：

1. 首先根据一个源ip对应单个目的ip还是多个目的ip将去除误告警后的告警分为两类，然后进行特征提取阶段，包含了四个特征：告警类型对应的告警数、告警协议对应的告警数、源和目的ip对应的告警数（两种）、告警优先级对应的告警数，并且分别求出它们各自的熵。
2. 告警聚合的原理在于：相同或相似的告警具有相同或相似的特征信息熵，因此使用了DBSCAN聚类算法进行聚类，其基于密度空间，不需要预先定义聚类的数量，输入参数为扫描半径和最小包含的点数。
3. 使用DBSCAN聚类后，两类告警分别被聚为19和7个类，然后使用论文[10]中的动态时间窗口的方法将19和7个类分别划分为了72和18个时间窗口，也就是说，最终得到了72+18条超高警。
4. 超告警数90/原始告警数6601即得到了告警的聚合率为98.63% 。







