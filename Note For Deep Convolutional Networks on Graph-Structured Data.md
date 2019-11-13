This is a note for the paper:Deep Convolutional Networks on Graph-Structured Data(2015)



####一些名词

欧式空间：定义内积$<x,y>=\sum x_{i}y_{i}$的$R^{n}$空间    

non-Euclidean domain：其中的数据点不能看作欧式空间的样本点。   

传统的图像、语音都可以看作欧式空间的样本点。但是一般的定义节点、边的图数据不行。  

stationarity：平稳性，具体解释为平移不变性。  

locality：通过网格上的度量定义局部性。  

compositionality：组合性。一个复杂的表达它的意义可以通过各个组成部分的意义来表达。  



#### 谱网络(spectral network)

这个网络在之前的论文中已经提出了，只不过这里采用更加简洁清晰的语言描述。  

基于拉普拉斯矩阵$L$定义图上的频域：$L=U \Lambda U^{T}$, 频域信号为$f=Ux$。  

图上的卷积算子为在频域上各个分量乘以一个系数，可以类比信号处理。  

当然，$U$可以被任意正交矩阵代替。并且可以变为学习参数。   

从另一个角度看，如果卷积被定义为和$L$可交换的矩阵(view convolutions as the family of linear transforms commuting with Laplacian，$LW=WL$)，则可以用$||LW-WL||$作为损失函数来约束$W$。

谱网络的前向传播过程：每个通道信号经过频域滤波后求和，得到一个新的通道。pooling通过层次聚类实现。图是固定的，最后展成一维向量通过全连接网络得到输出。  

频域滤波有如下变化：为了使滤波在图域上有局部性质(small spatial support)，可以约束滤波器系数为$w_{g}=  \mathcal{K} \widetilde{w}_{g}$ 其中$\mathcal{K}$为smoothing kernel，$\widetilde{w}_{g}$为参数。  

#### 建图

建图实际上是建立关联矩阵(affinity matrix)，即求任两个节点间的相似度。  

##### 非监督方法

求节点向量间的距离，用高斯核$exp^{-\frac{d(i,j)}{\sigma^{2}}}$或自适应核$exp^{-\frac{d(i,j)}{\sigma_{i}\sigma_{j}}}$  d是距离的平方，$\sigma_{i}$为局部节点i到其第k近的节点的距离。  

#####监督方法

输入经过若干层网络后用标签做损失，其中第一层为全连接。全连接的系数作为各分量的表示向量（类似词向量的学习）。将表示向量间的距离作为节点间的向量再用高斯核。监督方法的效果比非监督方法的效果好不少。  

#### 实验

##### Document Classification

200000文档，50个类  

图上每个节点代表一个单词，选择了2000个常用词。

效果没超过全连接网络。 

#####Molecular Activity Prediction

一个回归问题，基于分子的原子间距、化学键，预测分子活性，2800维特征(channel)。  

效果略微比全连接好。  

##### ImageNet

不需要建图这一步骤。效果略优于CNN。



#### 讨论

由于引入了图上到频域的变换，谱网络的计算复杂度太大，优点是参数少。 

建图的误差对后续影响很大。  

如何用广义的卷积(commuting with Laplacian)来处理图信号。  



我觉得各个通道分别处理可以无法很好的提取通道间的关系。如果是图像，那么每个通道的意义是相同的，都是颜色分量的强度。但如果是任意数据，那么每个通道的意义可能不同，这时候直接求和可能不合适？（放缩因子是可以学习的）。