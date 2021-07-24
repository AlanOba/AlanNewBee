==Scipy==

![image-20200504133430478](/Users/alan/Library/Application Support/typora-user-images/image-20200504133430478.png)

# **优化算法--scipy.optimize**

scipy中的optimize子包中提供了常用的最优化算法函数实现，我们可以直接调用这些函数完成我们的优化问题。

scipy.optimize包提供了几种常用的优化算法。 该模块包含以下几个方面 

- 使用各种算法(例如BFGS，Nelder-Mead单纯形，牛顿共轭梯度，COBYLA或SLSQP)的无约束和约束最小化多元标量函数(minimize())
- 全局(蛮力)优化程序(例如，anneal()，basinhopping())
- 最小二乘最小化(leastsq())和曲线拟合(curve_fit())算法
- 标量单变量函数最小化(minim_scalar())和根查找(newton())
- 使用多种算法(例如，Powell，Levenberg-Marquardt混合或Newton-Krylov等大规模方法)的多元方程系统求解

在用python实现逻辑回归和线性回归时，使用梯度下降法最小化cost function，用到了fmin_tnc()和minimize()。



## fmin_tnc()

```python
有约束的多元函数问题，提供梯度信息，使用截断牛顿法。

调用：

scipy.optimize.fmin_tnc(func, x0, fprime=None, args=(), approx_grad=0, bounds=None, epsilon=1e-08, scale=None, offset=None, messages=15, maxCGit=-1, maxfun=None, eta=-1, stepmx=0, accuracy=0, fmin=0, ftol=-1, xtol=-1, pgtol=-1, rescale=-1, disp=None, callback=None)

最常使用的参数：

func：优化的目标函数

x0：初值

fprime：提供优化函数func的梯度函数，不然优化函数func必须返回函数值和梯度，或者设置approx_grad=True

approx_grad :如果设置为True，会给出近似梯度

args：元组，是传递给优化函数的参数

返回：

x ： 数组，返回的优化问题目标值

nfeval ： 整数，function evaluations的数目

在进行优化的时候，每当目标优化函数被调用一次，就算一个function evaluation。在一次迭代过程中会有多次function evaluation。这个参数不等同于迭代次数，而往往大于迭代次数。

rc ： int,Return code, see below 

result = opt.fmin_tnc(func=costf_reg,x0=theta,args=(X,y,1),fprime=gredient_reg)

(array([ 1.27271026,  1.18111686,  0.62529965, -1.43166928, -0.91743189,
       -2.01987399, -0.17516292, -0.35725404, -0.36553118,  0.12393227,
       -1.19271299, -0.27469165, -0.61558556, -0.05098418, -1.45817009,
       -0.45645981, -0.29539513, -0.27778949, -0.04466178, -0.206033  ,
       -0.2421784 , -0.92467487, -0.1438915 , -0.32742405,  0.0155576 ,
       -0.29244868,  0.02779373, -1.04319154]), 32, 1)
```

## minimize()

```python
调用：

scipy.optimize.minimize(fun, x0, args=(), method=None, jac=None, hess=None, hessp=None, bounds=None, constraints=(), tol=None, callback=None, options=None)

参数：

fun ：优化的目标函数

x0 ：初值，一维数组，shape (n,)

args ： 元组，可选，额外传递给优化函数的参数

method：求解的算法，选择TNC则和fmin_tnc()类似

jac：返回梯度向量的函数

返回：

返回优化结果对象，x：优化问题的目标数组。success: True表示成功与否，不成功会给出失败信息。

例子：
result = opt.minimize(fun=costf_reg, x0=theta, args=(X,y,2), method='TNC')
print(result)


     fun: 0.5740215331747713
     jac: array([-1.11983756e-03, -3.17176285e-03,  1.66888725e-04, -3.80251386e-04,
        5.17319521e-04,  5.48006085e-05, -1.71642700e-03, -9.40103551e-04,
        2.54840593e-04,  1.63347114e-04, -4.23616697e-04,  9.04154529e-04,
       -7.58726415e-05,  3.3874014……])
 message: 'Converged (|f_n-f_(n-1)| ~= 0)'
    nfev: 192
     nit: 20
  status: 1
 success: True
       x: array([ 0.89832911,  0.72816704,  0.32672603, -0.8722403 , -0.49704549,
       -1.37221312, -0.16553916, -0.29805388, -0.18577737,  0.02011522,
       -0.78541694, -0.0979966 ,…… ])
```

