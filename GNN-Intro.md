[reference](https://distill.pub/2021/gnn-intro/)

# graph
GNN 是用于处理图数据(graph)的网络。图数据(graph)是由顶点(Vertex)，
边(Edge)组成的，因此图数据具有顶点特征、边特征以及全局特征。

# image and text
如果将图像的每个像素看作一个顶点，每个像素与相邻八个点之间建立边，那么图像也可以看作图数据；
如果将文本中的每个词或token看作一个顶点，每个词具有指向后一个紧邻的词的边，那么文本也可以认为是图数据。

# social network
图像和文本本身由更好的常规结构，将其作为图数据并无优势。图数据的优势在于可以处理没有固定结构的数据，比如
社交网络，每个人都可能认识几百到几千个不同的人，这与图像存在显著不同————图像中每个像素点只能与八个点相邻。

# display graph
通常可以使用邻接矩阵或邻接表表示图数据。

## adjacency matrices
邻接矩阵使用图中所有顶点作为行和列的索引，如果两个点 i, j 之间存在边，则将第 i 行第 j 列以及
第 j 行第 i 列对应位置格子涂黑。显然，邻接矩阵总是转置不变的，即 $A=A^T$

---

# wikipedia
根据 wikipedia ，某些现有的神经网络架构，比如 CV 领域的 CNN 和 NLP 领域的 Transformers 都可以看作是
在特定结构图上 GNN 。 

## GNN 的 key
GNN 设计的关键在于**成对消息传递(pairwise message passing)**，由此诞生了不同种类的 GNN。GNN 能否超越
**消息传递**模式，或者 GNN 都能建立在合适的图的消息传递上已经是一个开放性研究话题。

## 应用领域
GNN 可以应用在 NLP, social network, citation networks, molecular biology, chemistry,
physics, NP-hard 组合优化问题。

## 可供使用的 GNN 资源
1. pytorch Geometric
2. tensorflow GNN
3. jraph(Google JAX)

## GNN Architecture
一个通用的 GNN 包含下面几个基本层
1. Permutaion equivariant(置换等变):
2. Local pooling: 通过下采样，使图变粗糙，和 CNN 类似被用来扩大感受野
3. Global pooling: 最后的读出层，对图做全局展示，大小固定，并且必须是排列不变的（图的节点和边的顺序变化不能影响结果）

已经证明 GNN 不能比 Weisfeiler-Lehman 图同构测试更具表现力

在实践中，这意味着存在 GNN 无法区分的不同图结构（例如，具有相同原子但键不同的分子）

可以设计更强大的 GNN，在高维几何体（例如单纯复形）上运行

未来的架构是否会克服消息传递原语是一个开放的研究问题

## Message passing layers
消息传递层就是置换等边层

可以用一个消息传递神经网络(MPNNs)表示消息层

定义 G=(V,E) 表示一个图，其中 V 是节点的集合，E 是边的集合。定义 N_u 是节点 u 的邻居的集合，
x_u 是节点 u 的特征向量 e_{uv} 是边 (u, v) 的特征向量。那么 MPNN 层可以定义为

![](./f1.svg)

其中 φ 和 ψ 都是可微函数，

