# 差分隐私（Differential Privacy）

## 第一节

### 是什么？

差分隐私是用于防范差分攻击的，让攻击者的信息不会随新样本的出现而发生变化。通过加入随机噪声，使得两个数据集查询得到某一个结果的概率很接近，以至于我们分不清这个结果来自于哪一个数据集。（eg:张三单身）

### 定义公式

- 初始版本：（对于任意汉明距离为1的两个数据集）

![](https://pic2.zhimg.com/80/v2-df71f363007b1d302d464d8d56852bd1_1440w.png)

|  符号   | 含义                        |
| :-----: | --------------------------- |
| Pr[...] | 概率                        |
|  M(x)   | 最终查询函数 M(x)=f(x)+r    |
|  x, x'  | 任意汉明距离为1的两个数据集 |
|    S    | 查询函数的任意输出集合      |
|    ε    | 隐私预算                    |

​		只关注差异最大的地方限制住，所以用Max Divergence的定义，

​				<img src="https://pic4.zhimg.com/80/v2-68cc85e20633eebd85e45b7903152fa3_1440w.png" alt="img" style="zoom: 67%;" />

- 松弛版本：

<img src="https://pic3.zhimg.com/80/v2-8232f370700aaa3e20ea09b1ea65c2ba_1440w.png" style="zoom:80%;" />

​		整体实现的目标：可以利用更少的隐私预算，得到相同的噪声尺度；

**符号：**

- ![[公式]](https://www.zhihu.com/equation?tex=f%28x%29) 表示一个查询函数，比如查询count值，最大值，均值，梯度等等。
- ![[公式]](https://www.zhihu.com/equation?tex=R) 表示一个实数的概念，上标如果不写表示一维数据，比如最大值；如果是 ![[公式]](https://www.zhihu.com/equation?tex=R%5En) 表示n维数据，比如梯度。
- ![[公式]](https://www.zhihu.com/equation?tex=r) 表示一个随机噪声，可以服从高斯分布或者指数分布。
- 兄弟数据及 ![[公式]](https://www.zhihu.com/equation?tex=x%2Cx%27) 表示两个数据集只相差了一个样本。
- ![[公式]](https://www.zhihu.com/equation?tex=%5Cmathcal%7BM%7D%28x%29) 表示最终的一个确定的查询结果![[公式]](https://www.zhihu.com/equation?tex=f%28x%29)加上一个不确定的随机噪声![[公式]](https://www.zhihu.com/equation?tex=r)得到的最终结果。
- ![[公式]](https://www.zhihu.com/equation?tex=%5Cvarepsilon+) 表示一个很小的值，用来衡量隐私预算。 ![[公式]](https://www.zhihu.com/equation?tex=%5Cdelta) 是一个松弛项，表示可以接受差分隐私在一定程度上的不满足。
- ![[公式]](https://www.zhihu.com/equation?tex=D_%5Calpha%28%5Ccdot%2C%5Ccdot%29) 表示的是Renyi divergence，当 ![[公式]](https://www.zhihu.com/equation?tex=%5Calpha) 取不同值得时候代表不同的Divergence，比如KL-Divergence，Max-Divergence，是衡量两个分布的一种推广形式的表达，下一篇会讲到。



## 第二节

### 瑞丽熵（Renyi Entropy）

用于衡量系统的不确定性

<img src="https://pic4.zhimg.com/v2-74845e6e763bc2976c94232b88b1b84f_r.jpg" style="zoom:80%;" />

<img src="https://pic1.zhimg.com/80/v2-b47feb86f0e38a78733a394a20ac5168_1440w.png" style="zoom:80%;" />

以下是瑞丽熵的特殊情况；

-----

##### Hartley熵：

当 ![[公式]](https://www.zhihu.com/equation?tex=%5Calpha%3D0) 时， ![[公式]](https://www.zhihu.com/equation?tex=%5Cmathrm+%7BH%7D_%7B0%7D%28X%29) 实际上就是`Hartley熵`

<img src="https://pic3.zhimg.com/v2-37ffabd228ff6fb2fb47b0d9426e441a_r.jpg" style="zoom:80%;" />

-----

##### Shannon熵:

当 ![[公式]](https://www.zhihu.com/equation?tex=%5Calpha+%5Crightarrow+1) 时， ![[公式]](https://www.zhihu.com/equation?tex=%5Cmathrm+%7BH%7D_%7B1%7D%28X%29) 实际上就是`Shannon熵`

<img src="https://pic1.zhimg.com/80/v2-8e08567fd1781ac0b51bc17bcf9f63ac_1440w.png" alt="img" style="zoom:80%;" />

-----

##### Min-entropy:

当 ![[公式]](https://www.zhihu.com/equation?tex=%5Calpha+%5Crightarrow+%5Cinfty) 时， ![[公式]](https://www.zhihu.com/equation?tex=%5Cmathrm+%7BH%7D_%7B%5Cinfty%7D%28X%29) 表示的是最小熵

<img src="https://pic4.zhimg.com/80/v2-a372a59eae29edfae9f154944a11de0f_1440w.png" alt="img" style="zoom:80%;" />

-----

### Renyi Divergence

用于衡量分布之间的差距，但不是距离不满足对称性

<img src="https://pic2.zhimg.com/v2-c3f5679cc1644ceae9563d0e2b6dc399_r.jpg" style="zoom:80%;" />

以下是Renyi Divergence的特殊情况；

-----

##### KL Divergece：

当 ![[公式]](https://www.zhihu.com/equation?tex=%5Calpha%5Crightarrow+1)时，

<img src="https://pic3.zhimg.com/80/v2-52ca598c3478108e9bdef0bd64541f52_1440w.jpg" style="zoom:80%;" />

-----

##### Max Divergence：

当 ![[公式]](https://www.zhihu.com/equation?tex=%5Calpha%5Crightarrow+%5Cinfty) ，

<img src="https://pic1.zhimg.com/80/v2-47e0da8d0148c13dc4149d9be9ff3868_1440w.png" alt="img" style="zoom:80%;" />

-----

对这个`Max-Divergence`进行约束之后，得到差分隐私定义：

<img src="https://pic2.zhimg.com/80/v2-a8cf934fe70f6a2dd56711c6ad9bf631_1440w.jpg" alt="img" style="zoom:80%;" />

而后续的松弛版本就考虑 ![[公式]](https://www.zhihu.com/equation?tex=%5Calpha) 是有限的，满足严格DP则同样满足松弛DP：

<img src="https://pic2.zhimg.com/80/v2-32f538357dd18ad9979294ba29c2ace9_1440w.jpg" alt="img" style="zoom:80%;" />

-----

**差分隐私的`Composition`机制，它是将多个差分隐私算法结合在一起并且仍然保证满足差分隐私，是差分隐私算法落地和的关键。**



## 第三节

### 差分隐私三大机制

- 对于`数值型`的数据，一般采用`Laplace`(严格)或者`高斯`机制(松弛)，对得到数值结果加入随机噪声即可实现差分隐私；
- 而对于`非数值型`的数据，一般采用`指数`机制并引入一个`打分函数`，对每一种可能的输出都得到一个分数，归一化之后作为查询返回的概率值。

-----

#### 数值型

##### Laplace机制：

- **定义敏感度：**

  两个`兄弟数据集（只相差一个元素）` ![[公式]](https://www.zhihu.com/equation?tex=D%2CD%27) ，一个查询函数 ![[公式]](https://www.zhihu.com/equation?tex=f%28%5Ccdot%29) **最大**的变化范围：(eg:查询数量敏感度为1)

<img src="https://pic4.zhimg.com/80/v2-3b97e148443d421acbb9b355bc3b382f_1440w.png" alt="img" style="zoom:80%;" />

- **Laplace机制的定义：**

<img src="https://pic2.zhimg.com/80/v2-91002cba7ea3cac984fde0236ab072bd_1440w.png" alt="img" style="zoom:80%;" />

其中， ![[公式]](https://www.zhihu.com/equation?tex=f%28D%29) 表示的是查询函数， ![[公式]](https://www.zhihu.com/equation?tex=Y) 表示的是Laplace随机噪声， ![[公式]](https://www.zhihu.com/equation?tex=M%28D%29) 表示的是最后的返回结果。

噪声 ![[公式]](https://www.zhihu.com/equation?tex=Y+%5Csim+L%280%2C%5Cfrac%7B%5CDelta+f%7D%7B%5Cepsilon%7D%29) 满足![[公式]](https://www.zhihu.com/equation?tex=%28%5Cepsilon%2C0%29-DP)；

- Laplace提供的是严格的 ![[公式]](https://www.zhihu.com/equation?tex=%28%5Cepsilon%2C0%29-DP)；

-----

##### 高斯机制：

- **定义-敏感度：**

<img src="https://pic1.zhimg.com/80/v2-cb21e86ceab20ba8b3664cb3a8823774_1440w.png" alt="img" style="zoom:80%;" />

刚才Laplace定义的是 ![[公式]](https://www.zhihu.com/equation?tex=l_1) ，这里的高斯定义的是 ![[公式]](https://www.zhihu.com/equation?tex=l_2) ，这和两个分布的形式有很大关系，用以证明后面的差分隐私。

- **高斯机制定义：**

  对于任意的 ![[公式]](https://www.zhihu.com/equation?tex=%5Cdelta%5Cin%280%2C1%29%2C%5Csigma%3E%5Cfrac%7B%5Csqrt%7B2ln%281.25%2F+%5Cdelta%29%7D%5CDelta+f%7D%7B%5Cepsilon%7D) ，有噪声 ![[公式]](https://www.zhihu.com/equation?tex=Y+%5Csim+N%280%2C%5Csigma%5E2%29) 满足 ![[公式]](https://www.zhihu.com/equation?tex=%28%5Cepsilon%2C%5Cdelta%29-DP.)

  <img src="https://pic2.zhimg.com/80/v2-ff13efea19fd65bf27adba6daff0ca69_1440w.png" alt="img" style="zoom:80%;" />

  

  其中， ![[公式]](https://www.zhihu.com/equation?tex=M%28D%29%3Df%28D%29%2BY) ，高斯机制的定义明显比Laplace要复杂，这里主要有三个参数，

  - 高斯分布的标准差 ![[公式]](https://www.zhihu.com/equation?tex=%5Csigma) ，这决定了噪声的尺度了；
  - ![[公式]](https://www.zhihu.com/equation?tex=%5Cepsilon) 表示隐私预算，和噪声成负相关；
  - ![[公式]](https://www.zhihu.com/equation?tex=%5Cdelta) 表示松弛项，比如设置为 ![[公式]](https://www.zhihu.com/equation?tex=10%5E%7B-5%7D) ，就表示只能容忍 ![[公式]](https://www.zhihu.com/equation?tex=10%5E%7B-5%7D) 的概率违反严格差分隐私。

- 高斯机制提供的是松弛的 ![[公式]](https://www.zhihu.com/equation?tex=%28%5Cepsilon%2C%5Cdelta%29-DP)

-----

数值型噪声的分布好像都是由敏感度和隐私预算决定的？

都是直接在查询结果加噪声，只不过噪声分布不同。

-----

#### 非数值

##### 指数机制：

- **整体思想：**

  不固定输出一个结果，而是以一定概率输出，从而达到差分隐私。概率由打分函数打的分数确定，得分高的输出概率高，得分低的输出概率低。

- **定义-敏感度：**

  <img src="https://pic3.zhimg.com/80/v2-134268ea7ac53f12f2943385633f51b2_1440w.png" alt="img" style="zoom:80%;" />

  其中，打分函数 ![[公式]](https://www.zhihu.com/equation?tex=q%28D%2CR_i%29) ， ![[公式]](https://www.zhihu.com/equation?tex=D) 表示指定数据集， ![[公式]](https://www.zhihu.com/equation?tex=q%28D%2CR_i%29+) 表示某一个输出结果 ![[公式]](https://www.zhihu.com/equation?tex=R_i) 的分数。

- **指数机制定义：**

  以 ![[公式]](https://www.zhihu.com/equation?tex=M%28D%2Cq%2CR_i%29%5Csim+e%5E%7B%5Cfrac%7B%5Cepsilon+q%28D%2CR_i%29%7D%7B2%5CDelta+q%7D%7D) 的概率输出结果 ![[公式]](https://www.zhihu.com/equation?tex=R_i) 。

  但是 ![[公式]](https://www.zhihu.com/equation?tex=e%5E%7B%5Cfrac%7B%5Cepsilon+q%28x%2CR_i%29%7D%7B2%5CDelta+q%7D%7D) 表示的不是概率值，因此需要对所有可能的值进行归一化，得到对应的概率值。

  <img src="https://pic4.zhimg.com/80/v2-40b39c6c0fbef2376283662e28f41e6b_1440w.jpg" alt="img" style="zoom:80%;" />

- 分数高，计算出的输出概率就大，大概呈**指数型增长**；
- **隐私预算和可用性成正比，和隐私保护成反比。**

-----

**差分隐私的本质就是给查询结果加噪声，但是经过足够多次的查询取平均也能推断出一部分隐私信息，原理是多次查询消耗了大量隐私预算，隐私预算高，数据可用性强，隐私保护能力就弱。**



## 第四节

在许多实际应用场景中，必须要频繁的访问数据，频繁访问数据仍会造成一部分隐私泄露，所以需要利用组成原理对隐私预算进行合理的控制，当预算被用完时，数据将被禁止访问。

### Composition Theorem 组成理论

`Composition Theorem`目的是将一系列满足差分隐私的查询组合在一起，并且保证整体仍然满足差分隐私。

#### Basic Composition Theorem基本组成原理：

**不考虑查询函数之间的关联**，假设相互独立；

- **Sequential Composition 串行组合：**

  同一数据集，不同查询函数；

   ![[公式]](https://www.zhihu.com/equation?tex=M_i%28X%29) 表示所有的算法作用于同一个数据集 ![[公式]](https://www.zhihu.com/equation?tex=X) ,那么这些算法构成的集合满足 ![[公式]](https://www.zhihu.com/equation?tex=%5Csum_i%5Cvarepsilon_i-) 差分隐私；

- **Parallel Composition 并行组合：**

  不同数据集，不同查询函数；

   ![[公式]](https://www.zhihu.com/equation?tex=M_i%28X%5Ccap+D_i%29) 表示各个差分隐私算法之间作用的数据集互不相交，那么整体满足 ![[公式]](https://www.zhihu.com/equation?tex=%5Cvarepsilon-) 差分隐私。一个推广是，如果 ![[公式]](https://www.zhihu.com/equation?tex=M_i) 满足 ![[公式]](https://www.zhihu.com/equation?tex=%5Cvarepsilon_i) 的差分隐私算法，那么整体满足 ![[公式]](https://www.zhihu.com/equation?tex=%5Cmax+%5C%7B%7B%5Cvarepsilon_i%7D%5C%7D-) 差分隐私。

#### Advanced Composition高级组成原理：

考虑攻击者可以自适应地影响数据库以及对应的查询机制，换句话说**查询与查询之间是存在关联的**；

**输出是多维的随机变量；**

两个输出分布的差异就称为`Privacy Loss`，如果是严格约束这个`Privacy Loss`，那么就是 ![[公式]](https://www.zhihu.com/equation?tex=%5Cvarepsilon-) 差分隐私；如果允许一定程度违背，那么就是 ![[公式]](https://www.zhihu.com/equation?tex=%28%5Cvarepsilon%2C%5Cdelta%29-) 差分隐私。

- **Navie Composition Throrem**

  ![img](https://pic3.zhimg.com/80/v2-566dd22a67d5e57d31d045c2e18cd8e2_1440w.jpg)

  最简单的组合机制，组合之后的 ![[公式]](https://www.zhihu.com/equation?tex=%5Cepsilon%27%3Dk%5Cepsilon) 。

  V0，V1表示两次的查询输出结果。R=0或1表示实验次数。

- **Strong Composition Throrem**

  强组合原理的基本思想就是用很小的一点 ![[公式]](https://www.zhihu.com/equation?tex=%5Cdelta) 换取很多的 ![[公式]](https://www.zhihu.com/equation?tex=%5Cvarepsilon) 。

  ![img](https://pic3.zhimg.com/80/v2-febc151bd3651264868d9f8e0540d92a_1440w.png)

  当 ![[公式]](https://www.zhihu.com/equation?tex=%5Cepsilon%3D10%5E%7B-5%7D) 的时候，后面一项 ![[公式]](https://www.zhihu.com/equation?tex=k%5Cepsilon%28e%5E%7B%5Cepsilon%7D-1%29) 近似等于0，这样整体的 ![[公式]](https://www.zhihu.com/equation?tex=%5Cepsilon%27%3D%5Cepsilon%5Csqrt%7B2k%5Cln%281%2F%5Cdelta%27%29%7D) ，相当于 ![[公式]](https://www.zhihu.com/equation?tex=O%28%5Csqrt%7Bk%7D%29) ，相对于原来的 ![[公式]](https://www.zhihu.com/equation?tex=O%28k%29) 节省了更多的隐私预算。

- **Moments Accountant**

  提出的方法就是在计算的梯度 ![[公式]](https://www.zhihu.com/equation?tex=%5Cnabla+%5Cmathcal%7BL%7D) 中加入噪声，而重要的就是噪声的大小。 ![[公式]](https://www.zhihu.com/equation?tex=%5Cdelta) 决定了加入噪声 ![[公式]](https://www.zhihu.com/equation?tex=%5Csigma) 的大小，其中

  ​						 ![[公式]](https://www.zhihu.com/equation?tex=%5Csigma%5Cgeq+c_2%5Cfrac%7Bq%5Csqrt%7BT%5Clog%281%2F%5Cdelta%29%7D%7D%7B%5Cvarepsilon%7D+) 

**总结：在三种方法中，Moment Account方法在同样的噪声花费下隐私预算最小**

-----

sigma是噪声大小（标准差）；epsilon是隐私预算，delta是松弛项；

epsilon和delta共同决定sigma；确定其中两项，就得到另外一项，

-----

