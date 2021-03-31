---
typora-root-url: ..\image
---

## A two-stage solution method based on NSGA-II for Green Multi-Objective integrated process planning and scheduling in a battery packaging machinery workshop

#### 背景

Integrated Process Planning and Scheduling(IPPS)：集成工艺规划与调度

green manufacturing mode：绿色制造模式（环保）

Green Multi-Objective IPPS ：GMOIPPS

#### 创新点

1. 设计了一个基于改进 NSGA-II 的 GMOIPPS 两阶段求解框架。
2. 采用基本的 NSGA-II 对柔性工艺规划阶段进行了优化。
3. 设计了一种改进的 N5邻域结构的 NSGA-II (INSGA-II) ，用于在 JSP 阶段寻找非支配的调度方案。
4. 设计了三种整合策略来实现两个阶段之间的信息交互。

#### 算法设计

##### 1. 基于GMOIPPS的两阶段框架

![img](GMOIPPS-model.png)

- FPP 阶段

  > 基础的 NSGA-II 算法被用来为每个job生成近似最优的绿色方案，而且不同的方案是动态的输入到 JSP 阶段。

- JSP 阶段

  > **优化的 NSGA-II 算法**用来优化解决方案，以得到最优的调度方案。

##### 2. Three intergrated strategies

> 根据这两个阶段之间不同的信息交互方式，设计了三种不同的集成策略

- 第一种策略：在最下层判断 $j < MaxSize1$ 时跳转到 FPP 阶段第一步骤（生成初始种群）
  - 每次迭代都会更新初始化流程计划，即可获得新的Pareto解决方案集
  - 可保证 FPP 阶段的多样性，但会牺牲计算时间
- 第二种策略：在最下层判断 $j < MaxSize1$ 时跳转到 FPP 阶段第三步骤（随机选择Pareto set）
  - 每次迭代都会为 job 重新从帕累托解集种选择一个计划
- 第三种策略：设置两个循环，综合第一种和第二种，这时需要设计最大迭代次数来结束这一层循环
  - 内部循环执行第一种策略，获取新的Pareto解集。保证个体的局部搜索能力。
  - 外部循环执行第二种策略，更行Pareto解集。提高全部搜索能力，保证种群的多样性。



