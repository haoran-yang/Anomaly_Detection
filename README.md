## 离群点与新奇点
- 离群点检测: 训练数据包含离群点,即远离其它内围点。离群点检测估计器会尝试拟合出训练数据中内围点聚集的区域, 会忽略有偏离的观测值。
- 新奇点检测: 训练数据未被离群点污染，我们对新观测值是否为离群点感兴趣。在这个语境下，离群点被认为是新奇点。
## 欺诈和作弊
- 欺诈和作弊行为在数据上会与大部分数据(正常行为)有明显差异性的表现，通过异常检测可以辅助识别这些异常行为或客户。
### 孤立森林(IsolationForest)
- 高维数据集适合使用此方法。
- 孤立森林通过随机选择一个特征, 并随机选择所选特征的最大值和最小值之间的分割值来"隔离"观测。
- 由于递归划分可以由树形结构表示，因此隔离样本所需的分割次数等同于从根节点到终止节点的路径长度。
- 在这样的随机树的森林中取平均的路径长度是数据正态性和我们的决策功能的量度。
- 随机划分能为异常观测产生明显的较短路径。因此，当随机树的森林共同地为特定样本产生较短的路径长度时，这些样本就很有可能是异常的。
### 局部离群因子(Local Outlier Factor)
- 适合轻度高维数据集。
- 计算出反映观测异常程度的得分（称为局部离群因子）。
- 它测量给定数据点相对于其邻近点的局部密度偏差。算法思想是检测出具有比其邻近点明显更低密度的样本
- 局部密度从k个最近邻得到。观测数据的LOF得分等于其k个最近邻的平均局部密度与其本身密度的比值：正常情况预期与其近邻有着类似的局部密度，而异常数据则预计比近邻的局部密度要小得多。
- LOF算法的优点是考虑到数据集的局部和全局属性：即使在具有不同潜在密度的离群点数据集中，它也能够表现得很好。问题不在于样本是如何被分离的，而是样本与周围近邻的分离程度有多大。
### 高斯异常检测
- 适用于简单的离群点检测，要求数据服从高斯分布。在训练集上训练高斯模型，验证集上调节参数和确定阈值，验证集需要有异常标签。