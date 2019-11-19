This is a note for the paper: Learning Convolutional Neural Networks for Graphs (ICML 2016)

No source code available  

#### Problem Setup

mainly focus on graph classification with application to property prediction of chemical moleculars.   

baselines: SVM with graph kernel.   

#### Method

The author tries to define convolution operation on graph structure data. However, there are no concepts of node ordering or receptive field in graph data required by convolution. To address such problem, the author defines node ordering and receptive field at first.   

Node ordering(also called graph labeling in the paper) is based on traditional methods like calculating beweeness centrality($O|V^{3}|$ with floyd algorithm) which is applied by the author or Weisfeiler-Lehman algorithm. The degree of nodes may also be used to rank nodes.   

Receptive field defined to a central point v is the k nearest vertices of v.   Then, we utilize graph labeling to sort the nodes inside the receptive field.   

The number of receptive field is assigned mannualy, such as w(called width in the paper). We choose the top w node ordered by beweeness centrality and search their receptive fields.    

Since we have got receptive fields with ordered nodes, we could use convolution happily.



#### Problem

the ordering of nodes is not data adaptive.