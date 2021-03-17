## 2004 - Survey of multi-objective optimization methods for engineering 

**标题**：Survey of multi-objective optimization methods for engineering

**作者**：R.T.Marler and J.S.Arora

**DOI**：10.1007/s00158-003-0368-6

---

#### 概括

continuous and nonlinear mop问题的综述。主要归类为以下几种方法：

- methods with a priori articulation of preferences：先验偏好
- methods with a posteriori articulation of preferences：后验偏好
- methods with no articulation of preferences：没有表达偏好
- Genetic algorithms

除非理想点可实现（实现所有目标的最优），否则一个多目标问题的单一全局解决方案是不存在的。

#### Section 3 ：**a priori articulation of preferences** ：用户明示了目标函数/期望目标的相关重要性。

在看到解（criterion space里的点）之前，就可以quantify opinions。

在一个优化问题中考虑多个目标函数会引入额外的自由度（degree of freedom），除非这些自由度是受到限制的，否则理论上说是一组解的点，而不是一个最优点。决策者提供的偏好提供了约束，这类约束最常见的是定义utility functions。

##### Weighted global criterion method

##### Weighted sum method

- **如何设置权重值**
  1. 最不重要的目标的权重值为1，而具有一致递增性的整数权重分配给更重要的目标。（顺序比较）
  2. categorization methods中（归类法）不同的目标被归类到不同的范畴，这些范畴具有高度重要性、中度重要性，利用评价方法（rating methods）决策者赋予每个目标函数相对重要的独立值。
  3. Ratio questioning/ paired comparison methods （比率问题和配对比较法通过一次比较两个目标来对目标函数进行评分。
  4. comparison matrix：确定权重的视觉特征值
  5. based on fuzzy set theory：基于模糊集合理论的权重确定法（当相关重要性不清楚的情况下）
  6. 基于期望点和理想点的计算权重方法
- **缺陷**
  1. 尽管有很多确定权重值得方法，但先验的权重不一定保证最后的解可接受，这里的权重应该更精确的模拟成一个偏好函数（原始目标的函数），而不是常量。
  2. 在criterion space中不可能得到pareto最优集的非凸部分的点。（最然非凸pareto最优集相对少见）
  3. 同时，权重的一致性和连续性的变化不一定能得到精确的帕累托最优集和均匀分布的帕雷若最优集
  4. 权重值无法更新，可能一开始决策者也不确定目标之间的偏好程度

##### Lexicographic method

字典图解法：将目标函数按重要性排序

优点：

1. 不需要对目标函数进行规范化
2. 总能提供一个帕累托最优解

缺点：

1. 可能需要解决许多单目标问题才能获得一个解
2. 需要加入额外的约束
3. 对全局优化很有效果，但expensive

**先验方法的缺点：**

1. 如果只能通过用户的偏好来区分，可能会没有理由的排除掉潜在的解决方案，这种排除可能会妨碍决策者做出最能反映其偏好的解决方案。

#### Section 4：**a posteriori articulation of preferences**

**从一系列 equivalent solutions 里选择一个solution，这个solution是可以体现决策者的偏好的。**

决策者无法给出偏好函数的明确近似值（显示近似），因此，可以允许决策者从一系列解决方案中进行选择，即通过一种算法来确定帕累托最优集的表示形式，称为先生成后选择的方法（generate-first-choose-later）

那么此时问题变成了如何设计一个方法能够精确表示完整pareto集的pareto最优点，即不考虑哪个优化目标更重要，只考虑哪个解决方案更好。

##### 难点

1. 帕累托最优集合可能有无穷多个，如何确定有限的帕累托集合？（**如何在有限的资源下确定/找出有限个帕累托最优解集？**）
   - 通过调整方法参数（指数、权重等值），每个相对最优点都是可以达到的。
     - 通过权重向量的调整可以得到帕累托解集，但这个公式的解未必一定是帕累托最优解
     - 如果可以确定是帕累托最优解集，但实际可能无法达到
2. **如何从多个帕累托集合中寻找最终的单一解？**

##### Physical programming



##### Normal boundary intersection（NBI）method



##### Normal constraint（NC）method



#### Section 5

**no articulation of preferences**：没有偏好的情况

注意：这里还有一种情况即在运行算法的过程中，决策者的偏好是连续提供的场景论文没有讨论。



#### Section 6：**genetic global algorithms**

遗传算法不需要梯度信息，因此对目标函数和约束的形式没有限制，他们结合使用随机数和预先迭代的信息来评估和改进点（一组潜在的解决方案），而不是一次一个点。

全局优化：是所有可行域（完全可行空间），不仅仅是本地可行的区域。

