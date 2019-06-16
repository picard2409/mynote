#  数值代数基础
### 对于特征值，奇异值的理解
若$A^T=A$,则$A$是对称矩阵，若$A^T=-A$,则$A$是反对称矩阵。

如果矩阵$A$可逆，那么$A^{-1}=\frac{A^*}{|A|}$,$A^*$为$A$的伴随矩阵。
#### 矩阵条件数
矩阵$A$的条件数等于$A$的范数与$A$的逆的范数的乘积，即$cond(A)=\Vert A\Vert\cdot\Vert A^{-1}\Vert$,相应的可以定义三种条件数，即$cond(A,1),cond(A,2),cond(A,inf)$.
## 1.7 向量和矩阵范数
### 2.6.2 如何优化矩阵乘法
## 3 线性最小二乘问题
### 3.1 正规方程
为了导出正规方程，我们导出使得$\Vert Ax-b\Vert_2^2=(Ax-b)^T(Ax-b)$为零的$x$.

### 3.2.2 QR分解
定理3.1 QR分解。设A是$m\times n$阶矩阵，$m\geq n$. 假如A为列满秩的，则存在一个唯一的正交阵$Q(Q^TQ=I_n)$和唯一的具有正对角元$r_{ii}>0$的$n\times n$阶上三角阵$R$使得$A=QR$.
对于$A=[a_1,a_2,\dots,a_n]$的列$a_i$从左到右应用格拉姆-施密特正交化过程，得到张成同一空间的一系列正交向量$q_1$到$q_n$:这些正交向量是$Q$的列。系数$r_{ji}=q_j^Ta_i$,把每列的$a_i$表达为$q_1$到$q_i的一个线性组合：
$a_i=\sum_{j=1}^ir_{ji}q_j$.$r_{ji}$正好是$R$的元素。

> CGS（经典格拉姆-施密特算法）和MGS（修正的格拉姆-施密特算法）
>for i=1 to n   //计算Q和R的第i列
>

当$A$的列几乎线性相关时，CGS按浮点运算数值是不稳定的。MGS是较为稳定的。
### 3.2.3奇异值分解
**定理3.2** SVD.设$A$是一个任意的$m\times n$阶矩阵，$m \geq n$.则可记$A=U\Sigma V^T$,其中$U$是$m\times n$阶矩阵且满足$U^TU=I$,$\Sigma=diag(\sigma_1,...,\sigma_n)$,其中$\sigma_1\geq \sigma_2 \geq...\geq 0$,$U$的列$u_1,...,u_n$称为左奇异向量。$V$的列$v_1,...,v_n$称为右奇异向量。$\sigma_i$称为奇异值。

重新表述：给定任意$m\times n$阶矩阵$A$,将它看作向量$x\in \mathbb{R}^n$到向量$y=Ax\in \mathbb{R}^m$的映射。然后可以选择$\mathbb{R}^n$的一个正交坐标系（其中单位轴是$V$的列）和另一个$\mathbb{R}^n$的正交坐标系（其中单位轴是$U$的列）使得$A$是对角阵($ \Sigma $).

$x=\sum_{i=1}^n \beta_i v_i,y=Ax=\sum_{i=1}^n \sigma_i \beta_i u_i$于是有：</br>

$$Ax=A\sum_{i=1}^n \beta_i v_i=U\Sigma V^T 
[v_1,v_2,...,v_n]  \begin{bmatrix}\beta_1\\ \vdots \\ \beta_n\end{bmatrix}=U\Sigma V^TV\begin{bmatrix}\beta_1\\ \vdots \\ \beta_n\end{bmatrix}=\sum_{i=1}^n \sigma_i \beta_i u_i$$




### 3.4 正交矩阵
####3.4.1  Householder变换
Householder变换（或者反射）是一个形如$P=I-2uu^T$的矩阵，其中$\Vert u\Vert_2=1$,$P=P^T$,$PP^T=I$,$P$是一个对称正交矩阵。因为$Px$是$x$经过$O$点垂直于$u$平面中的反射，所以$P$被称为反射。

给定一个向量$x$，容易找到一个HouseHolder反射$P=I-2uu^T$使得$x$除第一个元素外其余元素都是零：</br>
$Px=[c,0,\dots,0]^T=c \cdot e_1$.

>利用HouseHolder变换作QR分解的一般算法：
>
```cpp
//CGS(格拉姆-施密特)算法求解矩阵的QR分解
#include<iostream>
#include<math.h>
#include"stdafx.h"
#define N1 9
#define N2 9

int QR(double& A, double& Q, double& R);
int main()
{
	//定义矩阵A
	double A[N1][N2];
	double Q[N1][N2];
	double R[N1][N2];

	for (int i = 0; i < N1; i++)
	{
		for (int j = 0; j < N2; j++)
		{
			A[i][j] = i*j / 5;
		}
	}
}
int QR(double& A, double& Q, double& R)
{
	double qi[N1];
	double ai[N1];
	for (int i = 0; i < N2; ++i)  //计算Q和R的第i列
	{

	}
}
```

## 4.2非对称特征值问题
**定义4.1**多项式$p(\lambda)=det(A-\lambda I)$称为$A$的特征多项式. $p(\lambda)=0$的根是$A$的特征值.

大多数算法将涉及到矩阵$A$变换到较简单的形式或者典范型, 根据这些形式容易计算$A$的特征值和特征向量. 这些变换称为相似变换.两个最普通的典范型称为若尔当型和舒尔型。

**定理4.1** 若尔当标准型. 给定$A$，存在一个非奇异阵$S$使得$S^{-1}AS=J$，其中$J$是若尔当标准型. 这意味着$J$是块对角矩阵, $J=diag(J_{n_1}(\lambda_1),J_{n_2}(\lambda_2),\dots,J_{n_k}(\lambda_k))$,而

$$J_{n_i}(\lambda_i)=\begin{equation}
\begin{bmatrix}
\lambda_i &1
\end{bmatrix}_{n_i\times n_i}
\end{equation}$$

**定理4.2**舒尔标准型. 给定$A$，存在一个酉阵$Q$和一个
### 6.5 基本迭代法
定义6.3 $A$的分裂是一个分解$A=M-K$,其中$M$非奇异。</br>
一个分裂得到一个迭代法如下：$Ax=Mx-Kx=b$推出$Mx=Kx+b$或者$x=M^{-1}Kx+M^{-1}b\equiv Rx+c$,故可取$x_{m+1}=Rx_m+c$作为迭代法。

引理6.4 设$\Vert \cdot \Vert$是任意的算子范数（$\Vert R\Vert=\max_{x\neq 0}\frac{\Vert Rx\Vert}{\Vert x\Vert}$）.若$\Vert R\Vert<1$,则$x_{m+1}=Rx_{m}+c$对任意$x_0$收敛。

>矩阵或者有界线性算子$A$的谱半径是指其特征值绝对值集合的上确界，记作$\rho(A)$.
>若$A=(a_{ij})$是复数域上的n阶方阵，又$\lambda_1,\lambda_2,\dots,\lambda_n$是$A$的全部特征值，则
>$$ \rho(A)=\max \limits_{1\leq i\leq n}|\lambda_i|$$

#### 6.5.1 雅可比迭代

#### 6.5.2 高斯-赛德尔法
这个方法的促动因素是在雅可比法循环的第$j$步，已经具有解的前$j-1$个分量的改进值，因而要在式子中利用这些值。


# 矩阵分析
### 1.3 相似性
定义1.3 设给定$A,B\in M_n$. 我们说$B$相似于$A$，如果存在一个非奇异的矩阵$S\in M_n$，使得
$$ B=S^{-1}AS$$
### 2.1酉矩阵
定义2.1.1 向量$x_1,\dots,x_n$构成一个正交组，是指对于所有向量有$x_i*x_j=0$,$x_i*x_i=1$
定义2.1.3 若向量$U\in M_n$,$U*U=I$,那么就称$U$为酉矩阵，若还有$U\in M_n(R)$,就称$U$为实正交矩阵。
定理2.1.4 若$U\in M_n$,下列命题等价：
(1)$U$是酉矩阵;
(2)U*U=I;
### 5 向量范数和矩阵范数
定理5.6.18 设$\Vert \cdot \Vert_{\alpha}$和$\Vert \cdot\Vert_{\beta}$是$C^N$上两个给定的向量范数，且设$\lVert\lvert \cdot \rvert\Vert_{\alpha}$和$\Vert \cdot\Vert_{\beta}$表示$M_n$上的相应诱导范数矩阵。即

$$\rvert\rvert \rvert A\lvert\lvert\lvert_{\alpha}\equiv \max\limits_{x\neq 0}\frac{\Vert Ax\Vert_{\alpha}}{\Vert x\Vert_{\alpha}}$$
和

$$\rvert\rvert \rvert A\lvert\lvert\lvert_{\beta}\equiv \max\limits_{x\neq 0}\frac{\Vert Ax\Vert_{\beta}}{\Vert x\Vert_{\beta} }$$

设向量$\{x_i\},i=1,2,\dots,n$,如有实数$\lambda_i>0$,且$\sum_{i=1}^n \lambda_i=1$,那么$\sum_{i=1}^n \lambda_i x_i$就称为向量$\{x_i\}$的一个凸组合。

1.如果$x_i\in D，i=1,2,\dots,n$的任意凸组合任在$D$中，那么$D$一定为凸集。
2.
# 非线性分析
### 压缩条件下的迭代法
### 