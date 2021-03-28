## Multi-Objective Optimal Dispatching of Microgrid With Large-Scale Electric Vehicles

#### 本文实现：

重新建立了微电网优化调度**模型**，同时**应用了**参数自适应粒子群优化算法。利用模拟退火算法的变异特性和 高斯 变异算子的精细搜索特性，提出了一种基于退火变异的微网格优化调度算法。

1. 提出模型：分布式生成模型

   - ELECTRIC VEHICLE MODEL
   - ATTERY CHARGE AND DISCHARGE MODEL

2. 使用方法：MICROGRID optimal dispatch strategy based on annealing mutation PARTICLE SWARM OPTIMIZATION

   > 基于**动态调整参数的粒子群算法**(PSO) ，该算法动态调整粒子群算法的惯性权重和学习因子，以提高算法的全局优化能力。然而，算法的优化能力还有待提高。为此，本文在该算法的基础上引入了多种退火机制和高斯变异算法，进一步提高了粒子群算法的全局搜索能力和局部搜索能力，帮助算法跳出局部最优解。

#### 算法设计

1. 修改 PSO 算法

   - 重新设计：更新粒子的位置和速度的参数调整策略。
   - 加入模拟退火算法：在模拟退火机制中，在每次迭代中随机生成一个 随机 数字。当粒子的变异概率大于这个随机数时，在粒子群速度更新公式中选择并用全局最优解代替目前粒子群的最优解，从而改变了粒子群优化的方向，使算法继续围绕最优解进行随机搜索，减少了计算量。

2. 引入 高斯变异

   高斯变异是从具有一定变异概率的种群中选出个体，然后以概率与高斯分布一致的方式随机改变个体的基因，即着眼于最优解附近区域的随机搜索。因此，它在附近的局部小范围内有很好的**搜索能力**。本文将高斯变异运算应用于 PSO 算法的全局搜索状态，引导个体搜索种群的最优解，加快算法寻找最优解，提高 PSO 算法的收敛能力。

![img](D:\Users\YP\github\paper_notes\image\annealing-mutation-PSO.png)

