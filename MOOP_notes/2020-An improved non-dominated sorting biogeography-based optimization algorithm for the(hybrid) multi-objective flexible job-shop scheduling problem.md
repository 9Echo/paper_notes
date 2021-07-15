## An improved non-dominated sorting biogeography-based optimization algorithm for the(hybrid) multi-objective flexible job-shop scheduling problem

**作者**：YoujunAn, XiaohuiChen, YingheLi

**DOI**：10.1016/j.asoc.2020.106869

#### 背景

场景：生产调度中的多目标灵活作业车间调度问题——Flexible job-shop scheduling problem （FJSP）

方法：改进的基于非支配排序生物地理学的优化算法（improved non-dominated sorting biogeography-based optimization： INSBBO）

本质上即 NSGA-II 和 bogeography-based optimization (BBO) algorithm 的结合：**NS-BBO**（已经提出的算法）

#### 主要工作

1. 提出一种基于归一化目标函数值所包含体积的 V-优势（V-dominance principle）原理，从而加快种群的收敛速度，克服帕累托优势原理对种群个体进化和压力的不足
2. 为了提高局部搜索能力，提出 hybrid variable neighborhood search（HVNS）结构
3. 为了避免迭代过程中出现丢失局部（次）优解（sub-optimal solutions）的情况，提出一种精英存储策略（elite storage strategy ESS）来存储局部次优解。
4. 为了提高该算法性能，对其内部适应性指数（habitat suitability index HSI）、迁移（migration）、变异算子进行改进。

#### 算法修改

##### 1. V-dominance principle

（假设这是最小化问题），那么可行解里坐标轴原点越近肯定越好，分布越均匀表示收敛性更好。

**体积计算**：当前帕累托平面上的某一点和坐标轴构成的矩形面积

用体积来表示解与解的优劣程度：体积越小，解决方案越好，本质上是对那些原本处在同一层帕累托平面上的点进行细分（根据体积大小）即加入同层个体之间的区分性，这样可以有效地减少每一层地解的个数，可以极大地提高单选压力和算法的计算速度。

<img src="D:\Users\YP\github\paper_notes\image\V-dominance.png" alt="img" style="zoom:60%;" />

##### 2.  HVNS-based local search

VNS: variable neighborhood search 可变领域搜索

利用五个领域结构来优化加工序列和机器分配问题，在执行基于 hvs 的局部搜索算法时，采用均匀分布的方法从上述5个结构(RIN、 RWN、 RRN、 TEN 和 MITN)中随机选择一个相邻的结构来优化染色体结构。该算法从多维和多方向(即不同的邻域结构)出发，避免了单一结构的局限性

##### 3. The elite storage strategy(ESS)

​		为了在优化过程中保持最优或次优解，建立了一个“精英记忆库”。在完成了迁移、变异、局部搜索后，利用Pareto占优原则对个体进行排序，把非支配层 F1中的个体存储到 $P_e$ 中，$P_e$ 的最大容量为种群大小 $N$ ，如果 $|F_1| > N$ ，那么将 F1 中的前 $N$ 个解存储到 $P_e$ 中，否则，$P_e$  只包含帕累托前沿解。

##### 4. HSI and migration operator

​		在迭代过程中，HSI(Habitat suitability index)和适应度函数的值一样在个体选择的过程中相当重要，利用 V-dominance 原则，计算每个个体的 HSI 值，作为参考哪个habitat更好。

​		迁移本质上是一种概率算子，表示迁入和迁出的概率，用于在栖息地共享特征，选用合适的迁移模型可以更好地保护和提高种群地收敛性和多样性。这里使用的是正弦波偏移模型。

##### 5. mutation operator

​		变异算子本质上也是一个概率值，用来增加种群的多样性，首先选择一个待突变的个体，再根据突变载体选择基因（SIV）具有较高或较低的HSI的个体更可能发生突变，在平均值附近的HSI不容易突变，所以这里重新设置突变算子。

#### 实验验证

##### 1. 验证INSBBO算法的可行性

调整该算法的参数，比较帕累托平面的个数，等前文中提到的优化效果是否实现

收敛性、多样性、达到局部最优的时间节点

##### 2. 和当前热门的算法互相比较

比较 average hypervolume curves