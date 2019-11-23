This is a note for the paper: Geometric deep learning on graphs and manifolds using mixture model CNNs (CVPR  2017)



#### 总结之前的GCN算法

作者首先将之前的GCN算法（以及一种流行学习，我不太了解）整合进一个统一的框架。这个统一的框架是一个局部信息整合模型：将邻居特征进行映射后加权求和，其中不同算法具有不同的映射或加权系数。比如DCNN采用k-步概率转移矩阵进行加权，GCN-KIPF采用拉普拉斯矩阵进行加权，GCN-DEFFER采用k-步拉普拉斯矩阵进行加权；GCN-KIPF采用MLP作为映射。

$$D_{j}(x)f=\sum\limits_{y \in \mathcal{N} (x)} w_{j}(u(x,y))f(y)$$

$f$为映射，u(x,y)为邻居间的连接特征，w为将连接特征映射为系数的函数，j为输出通道

#### 作者提出的算法（MoNet）

作者取w为高斯混合模型，其中协方差矩阵强制为对角阵，这样参数有2d个，d为输入变量的维数。可以将w的和归一化为1。

#### 实验

1、MNIST数据集，分为格点型数据和采样后的非格点数据。   

u取极坐标$(\rho,\theta)$ ，（向对中心节点x的坐标）   

输入特征就是点的像素   

2、citation dataset，包括cora和PubMed   

u取$u(x,y)=(\frac{1}{\sqrt{deg(x)}},\frac{1}{\sqrt{deg(y)}})$,在经过一个MLP得到最后的u   

输入特征为词袋(cora)，每个词的tf-idf(pubmed)    

3、FAUST数据集   

一个对象包含一个人的10个姿势，目标是将不同姿势下的人体上不同的部位对应起来，比如将跑步时人的腿和坐姿下的人的腿对应起来。具体我们先有一个姿势下的点及其类别作为输入，再将其他姿势与这个姿势进行对应。是一个对点的分类问题。

u应该是局部极坐标。  

输入特征为544维SHOT描述子

