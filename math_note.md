# Chebyshev谱配置法的稳定性与收敛性基础
数值格式被称为是稳定的如果数值解可以被不依赖于$N$(多项式的次数)的数据所控制。</br>
稳定性通过能量方法或者广义变分原理来证明。

考虑问题
$$\frac{\partial u}{\partial t}=\frac{\partial u}{\partial x^2},\quad -1<x<1,t>0$$
边界条件
$$u(-1,t)=u(1,t)=0$$
初始条件
$$u(x,0)=u_0(x)$$
使用配置法求解时，有如下的配置方程
$$\frac{\partial u^N}{\partial t}(x_k,t)=\frac{\partial u}{\partial x^2}(x_k,t),\quad k=1,\dots,N-1$$
使用能量方法，将上式两边都乘以$u^N(x_k,t)$,并求和，得到</br>
$$\sum_{k=0}^{N}\frac{\partial u^N}{\partial t}(x_k,t)u^N(x_k,t)\omega_k=\sum_{k=0}^{N}\frac{\partial u^N}{\partial x^2}(x_k,t)u^N(x_k,t)\omega_k$$
进一步可以写为
$$\frac12\frac{d}{dt}\sum_{k=0}^N [u^N(x_k,t)]^2\omega_k=\sum_{k=0}^{N}\frac{\partial u^N}{\partial x^2}(x_k,t)u^N(x_k,t)\omega_k$$
因为$u^N$是$N$次多项式，$\frac{\partial^2 u}{\partial x^2}u^N$是$2N-2$的多项式。对于高斯型求积公式，有</br>
**定理** 对于插值型求积公式
$$\int_{-1}^1\rho(x)f(x)dx\approx\sum_{i=1}^N A_i f(x_i) $$
具有$2N-1$次代数精度，当且仅当插值节点$x_1,x_2,\dots.x_N$是$[a,b]$上以$\rho(x)$为权的正交多项式的零点。

因此，式()中的右端可以精确的写成
$$\int_{-1}^1 \frac{\partial u^N}{\partial x^2}(x_k,t)u^N(x_k,t)\omega_k dx=\sum_{k=1}^{N}\frac{\partial u^N}{\partial x^2}(x_k,t)u^N(x_k,t)\omega_k$$
结合()式，有
$$\frac12\frac{d}{dt}\sum_{k=0}^N [u^N(x_k,t)]^2\omega_k= \int_{-1}^1 \frac{\partial u^N}{\partial x^2}(x_k,t)u^N(x_k,t)\omega_k dx$$

先上一个结论
$$-\int_{-1}^{1}\frac{\partial^2 u^N}{\partial x^2}(x,t)u^N(x,t)\omega(x)dx\geq \frac14\int_{-1}^{1}[\frac{\partial u^N}{\partial x}(x,t)]^2\omega(x)dx$$
结合()和()
$$\frac12\frac{d}{dt}\sum_{k=0}^N [u^N(x_k,t)]^2\omega_k+\frac14\int_{-1}^{1}[\frac{\partial u^N}{\partial x}(x,t)]^2\omega(x)dx\leq 0$$

在$[0,t]$上对上式两边积分
$$\frac12 \sum_{k=0}^N [u^N(x_k,t)]^2\omega_k+\frac14\int_0^t\int_{-1}^{1}[\frac{\partial u^N}{\partial x}(x,t)]^2\omega(x)dxds-\sum_{k=0}^N[u_0(x_k,t)]^2 \leq 0$$
亦
$$\frac12 \sum_{k=0}^N [u^N(x_k,t)]^2\omega_k+\frac14\int_0^t\int_{-1}^{1}[\frac{\partial u^N}{\partial x}(x,t)]^2\omega(x)dxds \leq \sum_{k=0}^N[u_0(x_k,t)]^2$$

所以

$$\frac12 \sum_{k=0}^N [u^N(x_k,t)]^2\omega_k+\frac14\int_0^t\int_{-1}^{1}[\frac{\partial u^N}{\partial x}(x,t)]^2\omega(x)dxds \leq 2 \max\limits_{-1\leq x\leq 1}|u_0(x_k,t)|^2$$

这就证明了Chebyshev配置法的稳定性。
令$\tilde{u}$为$u$的插值,即$\tilde{u}=I_Nu$，其满足
$$\frac{\partial \tilde{u}}{\partial t}(x_k,t)-\frac{\partial \tilde{u}}{\partial x^2}(x_k,t)=r(x_k,t),\quad t>0,k=1,\dots,N-1$$
$r$是阶段误差

下面考虑其收敛性





















[//]: <> ($$ \frac{\partial u}{\partial t}=\frac{\partial^2 u}{\partial x^2}+f$$)

[//]: <> (this is comment)




# 泛函、变分、代数与测度论（笔记）


### 列紧集

设$(\mathscr{X},\rho)$是一个距离空间，$A$是$\mathscr{X}$的一个子集，$A$称为是有界的，如果$\exists x_0\in\mathscr{X}$以及$r>0$,使得$A\subset B(x_0,r)$， 其中

$B(x_0,r)\triangleq\{x\in\mathscr{X}|\rho(x,x_0)<r\}$

在有穷维欧式空间中，有界无穷集合必含有一个收敛的子列，但这个性质不能推广到任意距离空间。

**定义1.3.1**设$(\mathscr{x},\rho)$是一个距离空间，$A$为其一子集，称$A$是列紧的，如果$A$中任意点列在$\mathscr{X}$中有一个收敛子列。

**定义1.3.10** 在拓扑空间$\mathscr{X}$中，集合$M$称为是紧的，如果$\mathscr{X}$中每个覆盖$M$的开集族中有有穷个开集覆盖集合$M$.

**例1.4.14**Sobolev空间$H^{m,p}(\Omega)$. 设$\Omega$是$R^n$中的一个有界连通开区域，$m$是一个非负整数，$1\leq p< \infty$，对于$C^k(\overline{\Omega})$中任意$u$
$$\Vert u\Vert_{m,p}=\Big(\sum_{|\alpha|\leq m}\int_{\Omega}|\partial^{\alpha}u(x)|^p \mathrm{d}x\Big)^{\frac 1 p}$$


**定义1.6.14**完备的内积空间称为Hilbert空间

**引理1.6.15**（庞加莱不等式）设$C_0^m(\Omega)$表示有界开区域$\Omega\subset R^n$上一切$m$次连续可微，并在边界$\partial \Omega$的某邻域内为0的函数集合。即
$$C_0^m(\Omega)=\{u \in C^m(\overline{\Omega})|u(x)=0,\text{当}x\in \partial \Omega\text{的某邻域}\}$$
那么$\forall u \in C_0^m(\Omega)$有
$$\sum_{|\alpha|<m}\int_{\Omega}|\partial^{\alpha}u(x)|^2 \mathrm{d}x\leq C\sum_{|\alpha|=m}\int_{\Omega}|\partial^{\alpha} u(x)|^2 \mathrm{d}x$$
其中$C$是仅依赖区域$\Omega$与$m$的常数。