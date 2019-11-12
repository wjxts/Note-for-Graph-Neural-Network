This is a note for the paper: Spectral Networks and Locally Connected Networks on Graphs



#### 主要贡献

将网格状数据比如图片或语音扩展到一般的图数据格式，将CNN扩展到这种数据上。扩展方式有两种：1、（Deep Locally Connected Networks）图上的数据前向传播时，相邻节点的数据加权（权重来自权重矩阵，是固定的）求和再做线性变换得到新的数据。pooling基于层次聚类，就是把近的点绑在一起再更新权重矩阵。2、（Spectral Network）将图上数据基于拉普拉斯矩阵的特征向量做正交变换，在谱域中每个分量乘以一个系数，系数为可学习参数。用cubic spline kernel构建系数时，滤波器系数较平滑，对应图域的滤波器作用效果更加局部（？）。      

测试数据：基于mnist数据集 1、将某些像素去掉，使其变为非网格状数据。2、将图片投影到三维单位球上。    

作者提出的问题：如何定义对偶图从而更好的捕获对偶坐标的几何性质？

