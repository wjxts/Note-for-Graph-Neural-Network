This is a note for the paper: Adaptive Graph Convolutional Neural Networks（2018AAAI）  

###Problem Setup

Graph classification which takes the original graph as input without coarsening the graph to fit the algorithm.    

Specifically, the author uses chemical componds as examples to predict toxicity and solubility.   

Besides, AGCN(proposed network) is tested on point cloud object classification datasets.  

#### Main Contribution

The author applies supervised metric learning to learn the similarity between node features which is used to update the Laplacian matrix furthermore.   (This layer is so-called SGC_LL)   

The similarity between node features is modeled by Mahalanobis distance:  

$$D(x_{i},x_{j})=\sqrt{(x_{i}-x_{j})^{T}M(x_{i}-x_{j})}$$

and similarity is given by Gaussian kernel:  

$$G_{x_{i},x_{j}}=exp(-D(x_{i},x_{j})/(2\sigma^{2}))$$

$$A_{ij}=G_{x_{i},x_{j}}$$

$$L_{res}=I-D^{-1/2}AD^{-1/2} \quad D=diag(row\,sum \,of \,A )$$

update Laplacian matrix:  

$$L^{'}=L+\alpha L_{res}$$

define layer combo: SGC_LL+BN+MaxPooling(element-wise of features among neighbours)    

Different from DCNN  which learns a mask of powers of transition matrix(which acts as Laplacian matrix similarly), AGCN augments Laplacian matrix by learning the residual Laplacian matrix.   