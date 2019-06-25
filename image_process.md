# 图像处理和计算机视觉
$E = mc^2$


## 数学基础

**定理(Weierstrass第一定理)** 设$f(x)\in C[a,b]$,那么对于任意给定的$\epsilon >0$,都存在多项式$P(x)$，使得：
$$\max \limits_{a\leq x\leq b}|P(x)-f(x)|< \epsilon$$

**定理(Weierstrass第一定理)** 

### 插值方法

牛顿插值：
n+1个节点$x_0,x_1,\dots,x_n$上的n次拉格朗日插值多项式也可以唯一的写成如下的形式：
$$p_n(x)=a_0+a_1(x-x_0)+\dots+a_n(x-x_0)(x-x_1)\dots(x-x_{n-1})$$
完备的线性赋范空间称为Banach空间。    
($L^p(\Omega)$空间)
用$H'$表示$H$上所有有界线性泛函全体，称之为$H$的对偶空间或者共轭空间。

#### 方向导数

定义1 设三元函数$f$在点$P_0(x_0,y_0,z_0)$的某邻域$U(P_0)\in R^3$有定义

**定理** 插值型求积公式$\int_a^b \rho(x)f(x)\mathrm{d}x\approx\sum_{j=1}^n A_j f(x_j) $具有2n-1次代数精度，必须且只需插值结点$x_1,x_2,\dots,x_n$是$[a,b]$上以$\rho(x)$为权的n次正交多项式的零点。

### 直角坐标系下二重积分的计算

定理  设$f(x,y)$在矩形区域$D=[a,b]\times[c,d]$上可积，且对每个$x\in [a,b]$,积分$\int_c^d f(x,y)\mathrm{d}y$存在，则累次积分
$$\int_a^b\mathrm{d}x\int_c^d f(x,y)\mathrm{d}y$$
也存在，且
$$\iint_d f(x,y)\mathrm{d}\sigma=\int_a^b\mathrm{d}x\int_c^d f(x,y) \mathrm{d}y$$

### 第一型曲面积分的计算

第一型曲面积分可以化为二重积分来计算
定理  设有光滑曲面
$$ S:z=z(x,y),\quad (x,y)\in D,$$
$f(x,y,z)$为$S$上的连续函数，则
$$\iint_Sf(x,y,z)\mathrm{d}S=\iint_Df(x,y,z(x,y)\sqrt{1+z_x^2+z_y^2})$$

### 从泛函到变分法

#### 最速下降曲线

（弧长公式）弧微分公式：$\mathrm{d}s=\sqrt{1+(\frac{dy}{dx})^2}\mathrm{d}x$

#### 泛函的无约束极值

在古典变分法中，如果泛函取极值的变量只受容许函数空间和满足边界条件的限制，仍称为无约束极值问题。
**变分学基本引理** 若$x(t)$在$[t_1,t_2]$上连续，并且对于每一个$h\in C^1[t_1,t_2]$以及$h(t_1)=h(t_2)=0$,都有$\int_{t_1}^{t_2} xh \mathrm{d}t=0$,那么$x(t)=0,t\in [t_1,t_2]$。

#### 函数极值必要条件

设$\Omega \in R^N$是一个开集，函数$f\in C^1(\Omega)$在$x_0\in \Omega$达到极小值，即在$x_0$的一个开领域$U$内：
$$f(x_0)\leq f(x)$$
于是$\forall h \in R^n(h\neq 0),\exists \epsilon(h)>0$,当$0<|\epsilon|<\epsilon(h)$时，$x_0+\epsilon h \in U$有
$$f(x_0+\epsilon h)\geq f(x_0) $$
即
$$\frac{1}{\epsilon}[f(x_0+\epsilon h)-f(x_0)]\geq 0$$
令$\epsilon \rightarrow 0$
$$(\triangledown f(x_0),h)_{R^n}=0$$
而$h\in R^n(h\neq 0)$是任意的的，所以由变分学基本引理：
$$\triangledown f(x_0)=0$$
这就是$x_0$成为$f$的极小值点的必要条件。
**对偶剖分**：

#### 欧拉-拉格朗日方程

#### 广义函数与傅里叶变换

**广义函数就是定义在某些特定函数空间上的线性连续泛函**
广义函数的定义域是特殊的函数空间，值域是$R^1$。

### 高斯积分公式

### 样条函数及其基本性质

### PCA的本质

## 图像平滑

## 阈值分割

### 熵算法

信息熵的概念来源于信息论，假设信源符号$u$有$N$种取值，记为：
$$u_1,u_2,\dots,u_N$$
且每一种信源符号出现的概率，记为：
$$p_1,p_2,\dots,p_3$$
那么该信源符号的信息熵，记为：
$$ entropy(u)=-\sum_{i=1}^N p_i \log~p_i$$

### Otsu阈值处理

$\phi$


