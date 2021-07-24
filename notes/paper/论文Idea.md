# Creative idea

~~1.我可以用WOA算法做警报的层次聚类分析，分两个方面，第一是如Julish等人的方法一样的每次调用算法产生一个聚类，然后把属于该聚类的警报进行聚合，然后继续调用，直到没有剩余的警报为止。可以模仿SA算法的那一片论文的结构，此外SA算法的应用中使用了k=0to3 ，WOA也可以使用？来使算法更加稳定 ps：使用分层聚类的好处是对于任何类型的属性都可以进行聚类而无需预处理~~

~~第二个方面是使用全局优化的方法，初始时确定要聚类的数量和初始解，然后对警报直接进行全局的聚类。 第二种方法可以消除第一种方法的覆盖问题。~~

~~至于为什么要使用两种方法:第一种的缺陷在于不可避免cluster之间的overlap问题，第二种虽然可以避免出现此类问题，但是cluster的数量不好确定。~~

~~2.针对WOA算法的螺旋搜索阶段可以使用交叉变异因子来代替其螺旋方程？的行为~~

~~3.可以阅读有关WOA算法的改进的相关论文，把改进加入到自己的应用中~~

~~4.对距离计算的权重优化 、 距离计算的阈值优化. ~~*针对不同的属性设置不同的距离权重*~~

~~5.可变的聚类数量(针对mehtod2)~~

~~6.新的fitness函数 目前可以暂定为和 可变染色体长度GA相同的fitness函数：~~

~~**Cluster size threshold+cluster dissimilarlarity+overlapping degree+the number of clusters**~~

~~7.GAbased 单聚类的那篇文章 先用GA算出一个second-best solution 然后再算一步局部左右解得到 the best solution~~

~~8.(GAbased全局聚类的那篇文章中)----dissimilarity的定义为一个警报聚类内所有警报与中心的平均距离的平均  ；overlap的定义为两个聚类中心是否有重叠~~

~~9.考虑加上时间因素~~

~~10.新的评估指标，过去的论文中针对警报聚合结果的评价指标过于单一。。。~~

==为了解决对比实验年份较老的问题，可以加上WOA聚类来进行对比==

# paper contents

1. Related work里可以加上数据挖掘的内容凑字数?

2.加上群智能算法在警报聚合上的应用 如粒子群、混沌粒子群 等

还有基于属性相似度的那些算法

3.加上NUSW-NB15数据集的描述 标注自己选择了哪些特征来做聚类

# 实验内容

可以和穷举搜索进行比较 如SA算法的实验部分

和各种GA算法进行比较

比较的内容：![image-20210425185554421](/Users/alan/Library/Application Support/typora-user-images/image-20210425185554421.png)

![image-20210425185815822](/Users/alan/Library/Application Support/typora-user-images/image-20210425185815822.png)

![image-20210425185954167](/Users/alan/Library/Application Support/typora-user-images/image-20210425185954167.png)

![image-20210425212537242](/Users/alan/Library/Application Support/typora-user-images/image-20210425212537242.png)



![image-20210426101945780](/Users/alan/Library/Application Support/typora-user-images/image-20210426101945780.png)

![image-20210426105232154](/Users/alan/Library/Application Support/typora-user-images/image-20210426105232154.png)

PS：为啥针对同一算法实验的结果都不一样。。

![image-20210426105554170](/Users/alan/Library/Application Support/typora-user-images/image-20210426105554170.png)

![image-20210426105654260](/Users/alan/Library/Application Support/typora-user-images/image-20210426105654260.png)





# 代码实现

Method1:

preparement：要想实现WOA对层次聚类的优化，首先需要进行离散和连续的值的处理？

对于port属性 的局部优化 需要使用parent  类似论文中的局部最优求解算法

1.定义各个属性的层次树

2.读取数据文件，对其做预处理，得到需要用的属性(ip,port,time等)

3,调用WOA算法->随机生成一个聚类中心，将数据集中的数据进行聚类，fitness为聚类内的距离+聚类包含的警报数目的综合->迭代优化->得到聚类告警

->判断剩余告警是否小于某个阈值->小于的话就结束->大于的话就删除已经聚类的警报，(这里可以一次性多输出几个比较优秀的聚类)对剩余的警报继续做WOA 直到满足结束条件

4.输出聚类后的超告警的数量和各告警的属性字段

5.自己的实验结果可以很好的反应聚类重合的情况(缺点)



Method2:

1.定义各个属性的层次树

2.读取数据文件，对其做预处理，得到需要用的属性(ip,port,time等)

3.调用WOA算法，生成n个聚类中心，然后将数据集中的数据进行聚类，fitness为聚类内的距离+聚类包含的警报数目+聚类数量的综合

4.输出最优的聚类结果 --agent





