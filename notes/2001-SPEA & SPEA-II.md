## SPEA:  A Comparative Case Study and the Strength Pareto Approach

#### 主要思想

> 并行地找到更多地帕累托最优解，基于NSGA进行优化

1. 在第二个连续更新的种群中存储非支配解
2. 根据支配该个体的非支配点的数量来评估个体的适应性
3. 利用pareto占优关系来保持种群多样性
4. 结合聚类的方法，以便在不破坏其特性的基础上减少非支配集

**与其他算法的区别：**

1. 个体的适应度值只取决于其非支配解的集合有关，群体成员之间是否支配不重要
2. 外部的非支配集中的所有解都参与了选择
3. 为了保持群体的多样性，提出了一个新的 niching method 方法，相对于NGSA，不需要距离参数

#### 算法设计

**step1.** 生成初始解 P，建立一个空集合（精英解集合）$P^*$

**step2.** 复制 P->$P^*$

**step3.** 删除P`中被其他个体支配的解

**step4.** 如果 $P^*$ 中的解超过给定的最大值 $N^*$, 用聚类的方式修剪 $P^*$

**step5.** 计算 P 和 $P^*$ 中个体的适应值

**step6.** 从P+$P^*$中选出个体放到交配池(这里应该为P)中。

**step7.** 对交配池里面的元素进行杂交变异。

**step8.** 判断循环。

#### 算法细节

##### 适应度分配

1. 对 $P^*$ 中的元素 i 给定一个强度值 Si，该强度值和这个点支配 P 集合里点得数目有关，设定 n 代表点（$P^*$ 中的非支配点）支配的点（在 P 中的点）的数目，N 代表 P 集合中点的总数目，那么 Si = n / (N+1)
2.  P 集合里的点的适应度等于 $P^*$ 中支配该点的非支配解的 Si 值 + 1

![image-20210330151641901](D:%5CYP%5C%E7%A0%94%E7%A9%B6%5CGithub%5Cpaper_notes%5Cimage%5Cformula1)

**举例**

图a 中实心点表示支配解，x表示外部的非支配解

最上方的3/8，因为支配它的有左下角矩阵里的3个解，N 中解的个数是7个+1，所以是3/8，矩形框内计算同理，如果有交叉区域的话求和，比如左下角的19/8，是三个非支配解的和+1（3/8+5/8+3/8+1=19/8）

![image-20210330152507968](D:%5CYP%5C%E7%A0%94%E7%A9%B6%5CGithub%5Cpaper_notes%5Cimage%5CSPEA.png)

上面两个图反映：

a：浅色区域的fitness值会比深色的更小，多样性更好

b：一个solution 如果有更多的neighbor 它的fitness就越大，应该受到更大的惩罚

如果pareto解集过大，外部非支配解集的大小会影响SPEA的性能，（选了等于没选）如果解分布不均匀，fitness assignment可能会偏向某个搜索区域而导致种群分布的不均衡，这个问题可以用average linkage method聚类解决。

##### 聚类算法 Redcuing the Pareto Set by Clustering

1. 初始化聚类集合 C，每一个 P1中的点都构建一个聚类集合
2. 如果 |C| <= N1，执行5，否则3
3. 计算每两个cluster的距离d，个体i1和i2的欧式距离
4. 选择最小距离的两个cluster，合并
5. 计算合并后的非支配解集，每个cluster选择一个代表individual，这里选的聚类中心（与类中其他点的平均距离最小）作为代表解。

![image-20210330153705520](D:%5CYP%5C%E7%A0%94%E7%A9%B6%5CGithub%5Cpaper_notes%5Cimage%5CSPEA-formula2)

#### 实验

和四种算法：HLGA, NPGA, VEGA, and NSGA做对比





## SPEA2: Improving the Strength Pareto Evolutionary Algorithm

#### 主要思想

1. 提出了一种改进的适应度分配方案，该方案考虑了每个个体支配和被支配个体的数量。
2. 引入邻密度估计（neighbor density estimation），使得搜索过程得到更精确的引导。
3. 使用了一种新的存档截断的方法可以保留边界解。

**SPEA 的缺点**

1. fitness assignment 过程，被同一个存档个体支配的其他个体具有相同的fitness值，降低了选择压力，使得SPEA退化为随即搜索
2. density estimation过程，如果多个个体之间不相关，不互相支配，这样支配关系就失去作用，（目标数大于等于3的情况很常见），聚类的方式只使用了archive的个体，而不是整个种群
3. archive truncation 存档截断，聚类可以减少非支配解个数，但是丢失了外部的solution，但这些解应该被保存在archive中，保持多样性。

#### 算法设计

1. 初始化(Initialization)：生成初始种群P0和一个空的存档（外部存档）P0*,P0*为空集，t=0
2. 适应度分配（Fitness assignment）：计算PT和PT*的适应度值
3. 环境选择（Environmental selection）：将所有 PT 和 PT* 的个体复制到 PT\*+1 ,如果种群个数超过 N\*(archive size)，采用截断操作（truncation operator），如果合并后的种群个数少于 N* 则用 PT 和 PT\* 中的支配解填充 PT\*+1
4. 终止条件（Termination）：如果当前迭代数t>=T或者其他停止标准满足，将A作为PT+1中非支配解所代表的决策变量集合输出
5. 选择方式（Mating selection）：对 PT\*+1 采用binary tournament selection放入mating pool
6. 变异（Variation）：对mating pool中的个体进行重组和变异，PT+1作为最后的种群，t=t+1，转到步骤2



> SPEA2使用的是更加细粒度的适应度值计算方法，还包含了density information，而且外部存档大小的值是固定的（也就是说进一步增加个体和个体之间的区分度）



##### fitness assignment

为了避免同一个外部存档中个体支配的其他个体具有相同的适应度值，SPEA2同时考虑支配解和非支配解

#####   Environmental Selection















