# MPC

安全多方计算（Secure Multi-party Computation, MPC）是隐私计算技术中的一种，它可以让一组用户以他们的隐私数据为输入，共同计算一个函数，并且所有用户只能得到这个函数的输出，无法得到其他的任何信息。

大部分的MPC协议，都是用来计算逻辑电路，或者是算数电路的。也就是说，在MPC中，我们要将计算的函数表示为逻辑电路或算数电路的形式。在逻辑电路中，用到的操作只有非门和异或门；在算数电路中，用到的操作只有加法和乘法。 今天我们介绍的协议，是计算算数电路的，也就是说，需要实现安全的加法和乘法。 这里所说的加法和乘法，都是定义在有限环上的，比如说环$F_p$上，$p$是一个非常大的素数。所以每个MPC参与方的输入，以及最后协议的输出，都是在$F_p$中的元素。MASCOT是基于秘密分享的方法。

# MASCOT

MASCOT（Faster Malicious Arithmetic Secure Computation with Oblivious Transfer）安全多方计算协议，即使用不经意传输实现的快速抗恶意算数安全计算。

**威胁模型**

大多数静态恶意参与方。

- 大多数，指的是在总共n个参与方中，可以有至多n−1个参与方是不诚实的；
- 静态指的是在协议开始执行之前，这些不诚实的参与方就已经确定了；
- 恶意指的是这些不诚实的参与方，不仅会尝试从协议中窥探其他人的数据，而且会主动破坏协议的执行，让协议输出不正确的结果。

MASCOT协议整体上分为离线和在线两部分，其中离线部分用来进行预处理，在线部分用来计算所需要的函数。离线部分与在线部分是独立的，与参与方的输入、所需计算的函数无关。

## 离线部分

在离线部分中，主要是用来生成两部分内容：

- 每个参与方$P_i$生成一个随机值$r$的一系列秘密分享的份额$[r]$，$r$只有$P_i$知道。
- 







> 参考资料：
>
> 1. 主要转载于：https://zhuanlan.zhihu.com/p/380037249
> 2. Keller M, Orsini E, Scholl P. MASCOT: faster malicious arithmetic secure computation with oblivious transfer[C]//Proceedings of the 2016 ACM SIGSAC Conference on Computer and Communications Security. 2016: 830-842.
> 3. Beaver D. Efficient multiparty protocols using circuit randomization[C]//Annual International Cryptology Conference. Springer, Berlin, Heidelberg, 1991: 420-432.