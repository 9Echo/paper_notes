## non-dominated sorting genetic algorithm II (NSGA-II)

**主要贡献**：提出**利用了解与解之间的支配关系来进行排序**

（1）提出了快速非支配排序算法，降低了计算的 复杂度，从原先的 O(MP3 ) 变为 O(MP2 ) 。 

（2）采用拥挤度和拥挤度比较算子取代了原先 的共享小生境技术作为保证个体多样性的方法，不但克服了NSGA中需要人为指定参数的问题，而且通 过此比较方法使得种群中的个体可以更均匀地扩展 到整个Pareto域 。 

（3）增加了精英策略的使用，通过将父代种群和 子代种群中的所有个体混合后进行非支配排序的方法，很好避免了父代中优秀个体的丢失。

### 基本思路

1. 随机产生规模为 $N$ 的初始种群，对其进行**非支配排序**，然后通过遗传算法的选择、交叉、变异三个基本操作得到第一代子种群；
2. 第二代：将父代种群和子代种群结合（2N），进行**快速非支配排序**，同时对每个非支配层的个体进行**拥挤度计算**，根据非支配关系和个体的拥挤度选择合适的个体组成新的父代种群（**精英保留策略**），再利用遗传算法得到第二代子种群；
3. 重复步骤2，直到满足结束条件。



### 非支配排序

将种群中的个体根据支配关系进行分层。

> (1) 设 $j=1$;
>
> (2) 对于所有的 $g=1,2,...,N$ 且 $g \neq j$ ，基于适应度函数比较个体 $x^j$ 和个体 $x^g$ 之间的支配与非支配关系；
>
> (3) 如果不存在任何一个个体 $x^g$  优于 $x^j$ ，那么 $x^j$ 被标记为非支配个体；
>
> (4) 令 $j = j+1$，重复步骤 (1)，直到找到所有的非支配个体

步骤(1) - 步骤(4) 可得到**第一级非支配层**；忽略这些非支配个体，重复步骤(1)-步骤(4) ，得到**第二级非支配层**，以此类推，直到所有种群中的个体被分类。

**时间复杂度** ： 单个体和种群中的其他个体进行支配关系比较，判断其支配关系，复杂度为 $O(MN)$；遍历种群搜索出等级为 1 的非支配个体，复杂度为 $O(MN^2)$ ；最坏的情况是每一层存在一个解，有 $N$ 层，复杂度为 $O(MN^3)$。



### 快速非支配排序

<img src="C:\Users\lambda\AppData\Roaming\Typora\typora-user-images\image-20201221140839797.png" alt="image-20201221140839797" style="zoom:80%;" />

> 输入：假设种群为 $P$ ，个体为 $p$
>
> 输出：种群中支配个体 $p$ 的个体数： $n_p$ ，种群中被个体 $p$ 支配的个体集合： $S_p$
>
> 时间复杂度为 $O(mN^2)$

1. 找到种群中第一级占优（$n_p = 0$）的个体，对应 $p_{rank} = 1$，并保存在当前集合 $F_1$ 中，对于其他 $n_p \neq 0$ 的个体，记录个体 $p$ 对应的 $n_p$ 和 $S_p$；
2. 对于当前集合 $F_1$ 中的每个个体 $p$ ，其所支配的个体集合为 $S_p$，遍历 $S_p$ 中的每个个体 $q$ ，令 $n_q = n_q - 1$ ，如果 $n_p = 0$ ，将个体 $q$ 保存至集合 $Q$ 中。**这个步骤的目的是去掉已经筛选出的前沿中个体的影响，方便对剩下的个体进行排序。**
3. 记 $F_1$ 为第一层非支配层个体集合，以 $Q$ 为下一层支配层集合，重复上述操作，直到整个种群被分级。

**缺点**：空间复杂度上升至 $O(N^2)$



### 拥挤度计算

对于同一层非支配个体集合里的个体，为了保证解能够均匀分配在 $Pareto$ 前沿，避免个体聚集在某一处，**计算同一非支配层级中某个给定个体周围其他个体的密度**。

![image-20201221140916392](D:%5CYP%5C%E7%A0%94%E7%A9%B6%5CGithub%5Cpaper_notes%5Cnotes%5Cimage-20201221140916392.png)

个体的拥挤距离计算

![image-20201221140940426](D:%5CYP%5C%E7%A0%94%E7%A9%B6%5CGithub%5Cpaper_notes%5Cnotes%5Cimage-20201221140940426.png)



### 精英保留策略（排序算法）

**优势**：扩大采样空间，将父代种群与其产生的子代种群结合，共同竞争产生下一代种群，有利于保持父代中的优良个体进入下一代，并通过对种群中所有个体的分层存放，使得最佳个体不会丢失，迅速提高种群水平。

**非占有排序+拥挤度排序**

1. 先根据**个体层级数值排序**。计算每个个体的层级数值 $i_{rank}$ ，数值越低表明该个体越优；

2. 同层级个体依据**拥挤度排序**。计算每个个体的拥挤度，个体拥挤度越大，表明该个体越优。

![image-20201221141012201](D:%5CYP%5C%E7%A0%94%E7%A9%B6%5CGithub%5Cpaper_notes%5Cimage%5CNGSA-II-sorting.png)



#### 时间复杂度

<img src="C:\Users\lambda\AppData\Roaming\Typora\typora-user-images\image-20201221141056510.png" alt="image-20201221141056510" style="zoom:80%;" />