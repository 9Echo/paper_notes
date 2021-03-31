## MOEA/D: A Multiobjective Evolutionary Algorithm Based on Decomposition

> **雏形**：根据每一个目标分配一个权重作为其重要程度，设置权重，把多目标问题转化为单目标问题。但这种方法只能得到一个解，然而对于多目标问题而言，并不存在一个解可以同时使得所有目标最优，为了得到一组多样性的解，**设置一组不同的权重向量**将该多目标优化问题分解为一组单目标优化问题来同时求解。

**基于分解的多目标进化算法**

> 为了使种群更快的收敛，给每一个权重向量都分配了一个个体，使用邻近权重向量的替换策略，即相隔较近的权重向量附着的个体之间才有机会根据相同的权重向量来比较优劣。此外，种群也以一定概率只能临近区域交叉产生后代。该算法可以使种群较快的逼近POF

基于分解的方法首先需要得到一组均匀分布的**参照向量**来指导选择操作。对于每个参照向量，其指导选择的过程需要**比较解的优劣**，这就需要用到一些标量函数来定量衡量一个解对于这个参照向量的适应度值。

### Tchebycheff Approach

<img src="C:\Users\lambda\AppData\Roaming\Typora\typora-user-images\image-20201221142136462.png" alt="image-20201221142136462" style="zoom:50%;" />

<img src="C:\Users\lambda\AppData\Roaming\Typora\typora-user-images\image-20201221142248459.png" alt="image-20201221142248459" style="zoom:80%;" />

1. 变换坐标系。把 $Z^*$ 作为坐标原点。
2. 确定等高线。对于 $f_1$ 来说，要max的式子中 $f_1$ 相等，即纵坐标相等，所以等高线和 x 轴平行， $f_2$ 的等高线和 y 轴平行。
3. 收敛过程。如果某个个题在权重向量方向的上方，那么max之后得到的是 $f_1$ 一部分，优化过程为减小对应 $f_1$ 的值，即该个体往下移动。相反，如果是落在权重向量下方，往左移动，也就是最终保证个体目标值落在 A 点附近。



## 性能评价指标

- 分布性：衡量所得到的解在Pareto前沿上的分布情况。
  - 得到的近似解是否分布均匀。
  - 分布范围是否在整个Pareto前沿上
- 收敛性：衡量得到的解逼近真实Pareto前沿的程度。

目前常用的两个性能评估指标：

- **IGD(Inverted Generational Distance)**

  > 假定 PF 是目标空间中真实帕累托前沿上分布均匀的点的集合， PF* 是进化算法得到的近似解，那么 IGD 即 PF 到 PF* 的平均距离。如果 IGD 的值越小，说明得到的解越好。

  <img src="C:\Users\lambda\AppData\Roaming\Typora\typora-user-images\image-20201221141256024.png" alt="image-20201221141256024" style="zoom:80%;" />

- **HV(Hypervolume)**

  > 计算时需要一个参考点，一般设置为真实帕累托前沿中每个目标的最大值，假设为 $R = (R_1, ..., R_m)^T$ 
  >
  > Leb(A) 是集合 A 的 lebesgue测度。
  >
  > HV 值越大，说明得到的解越好。

  <img src="C:\Users\lambda\AppData\Roaming\Typora\typora-user-images\image-20201221141319305.png" alt="image-20201221141319305" style="zoom:80%;" />

  一般对于一个未知的多目标优化问题，想要知道真实的 Pareto Front 数据比较困难，所以 HV 更容易用来作为一个测度在种群进化过程中来选择个体。

- **结果可视化**

![image-20201221141931931](D:%5CYP%5C%E7%A0%94%E7%A9%B6%5CGithub%5Cpaper_notes%5Cnotes%5Cimage-20201221141931931.png)













