## Multi objective optimization based on SPEA for the microgrid energy dispatch

**作者**：武晓敏（中国地质大学）

**DOI**：[10.23919/ChiCC.2018.8483695](https://doi.org/10.23919/ChiCC.2018.8483695)

这篇论文是基于The Strength Pareto Evolutionary Algorithm (SPEA) 进行改进

**论文实现：**

本文基于网络物理的概念，考虑到经济成本、环境效益和能源利用率这三个多目标优化问题，建立了由分散式发电输出功率预测、负荷需求、约束条件和最优化函数组成的微电网能量分配模型，采用强度帕累托进化算法（SPEA）求解多目标最佳化问题。最大限度地利用可再生能源，合理规划分散式发电、蓄能电站和电网的能源方向，实现微网能源的合理配置和优化运行。

构建模型，模型中利用SPEA算法

文章重点在于构建电网模型，预测部分使用到了神经网络，在模型中某一层利用多目标优化算法SPEA，最后验证优化效果。