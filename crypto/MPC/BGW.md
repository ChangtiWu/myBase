# BGW协议

Ben-Or-Goldwassert -Wigdemon （BGW）

> - 支持的参与方数量：多方
> - 协议的执行轮数：电路深度
> - 支持的电路类型：布尔电路/算术电路

强依赖于Shamir秘密分享方案，利用Shamir秘密分享方案的同态性。每个参与方持有所有参与方的输入的秘密份额，将其输入电路，输出最终计算结果的秘密份额。

## 以算术电路为例

假设$n$个参与方$P_1,...,P_n$想要安全计算函数$y=f(a,b)$（两个输入）。

假设各参与方$P_i$各自持有所有输入的一个Shamir秘密份额$\langle a\rangle_i,\langle b\rangle_i$。

### 加法门

根据Shamir秘密分享的加法同态性，各参与方本地计算$\langle y\rangle _i= \langle a\rangle_i + \langle b\rangle_i$，得到最终计算结果的Shamir秘密份额$\langle y\rangle_i$。

### 乘法门

由于$\langle a\rangle_i$在$t$阶多项式$f_a(x)=a+r^a_1x+...+r^a_tx^t$上，$\langle b\rangle_i$在$t$阶多项式$f_b(x)=b+r^b_1x+...+r^b_tx^t$上，则$\langle a\rangle_i\cdot \langle b\rangle_i$在$2t$阶多项式$h=f_a\cdot f_b=ab+...$上，但是该多项式至少需要$2t+1$个秘密份额才能恢复出来，超过了秘密份额的阈值，造成了阈值溢出。为了使阈值保持不变，仍然至少$t+1$个参与方才能恢复出$y$，需要采取以下办法。

首先，依然回到$h=f_a\cdot f_b$，假设$h(x)=f_a(x)\cdot f_b(x)=ab+r_1x+r_2x^2+...+r_{2t}x^{2t}$。已知该多项式曲线上的$2t+1$个点$\{(x_1,h(x_1)),...,(x_{2t+1},h(x_{2t+1}))\},h(x_i)=f_a(x_i)\cdot f_b(x_i)=\langle a\rangle_i\cdot \langle b\rangle_i$，必能恢复出该多项式曲线：
$$
AX=\left[\begin{array}{cccc}
1 & x_1 & \ldots & x_1^{2 t} \\
1 & x_2 & \ldots & x_2^{2 t} \\
\ldots & \ldots & \ldots & \ldots \\
1 & x_{2 t+1} & \ldots & x_{(2 t+1)}^{2 t}
\end{array}\right]\left[\begin{array}{c}
ab \\
r_1 \\
\ldots \\
r_{2 t}
\end{array}\right]
=\left[\begin{array}{c}
h\left(x_1\right) \\
h\left(x_2\right) \\
\ldots \\
h(x_{2t+1})
\end{array}\right]
$$
其中，$A$是一个范德蒙矩阵，其可逆。设
$$
A^{-1}=\left[\begin{array}{cccc}
\lambda_1 & \lambda_2 & \ldots & \lambda_{2 t+1} \\
\ldots & \ldots & \ldots & \ldots \\
\ldots & \ldots & \ldots & \ldots \\
\ldots & \ldots & \ldots & \ldots
\end{array}\right]
$$
进一步可得：
$$
X=\left[\begin{array}{c}
a b \\
r_1 \\
\cdots \\
r_{2 t}
\end{array}\right]
=A^{-1} \left[\begin{array}{c}
h\left(x_1\right) \\
h\left(x_2\right) \\
\ldots \\
h(x_{2t+1})
\end{array}\right]
=\left[\begin{array}{cccc}
\lambda_1 & \lambda_2 & \ldots & \lambda_{2 t+1} \\
\ldots & \ldots & \ldots & \ldots \\
\ldots & \ldots & \ldots & \ldots \\
\ldots & \ldots & \ldots & \ldots
\end{array}\right]
\left[\begin{array}{c}
h\left(x_1\right) \\
h\left(x_2\right) \\
\ldots \\
h(x_{2t+1})
\end{array}\right]
$$
则：
$$
ab=\lambda_1 \cdot h\left(x_1\right)+\lambda_2 \cdot h\left(x_2\right)+\ldots \lambda_{2 t+1} \cdot h\left(x_{2 t+1}\right)
$$
其中$\lambda_1,...,\lambda_{2t+1}$称为拉格朗日系数，是公开参数。而$h(x_i)=\langle a\rangle_i\cdot \langle b\rangle_i$只有参与方$P_i$拥有。

此时，$P_i$对$h(x_i)=\langle a\rangle_i\cdot \langle b\rangle_i$做一次(t,n)-Shamir秘密分享：$\{\langle h(x_i)\rangle_1,...,\langle h(x_i)\rangle_n \}$。之后，$P_i$收到$\{\langle h(x_1)\rangle_i,...,\langle h(x_n)\rangle_i \}$。

$P_i$本地计算$y$的秘密份额：
$$
\langle ab\rangle_i =\sum_j^{2t+1}\lambda_j \langle h(x_j)\rangle_i
$$
