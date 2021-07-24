## Fuzzy OptimalAllocation Model forTask-Resource Assignment Problem inCollaborative Logistics Network

### 论文工作

 This  paper presents an optimal allocation model of fuzzy resources for multi-stage  random  logistics  tasks  based  on  the  six-point trapezoidal  fuzzy  number  and  the  membership  function. Besides, considering task demands and resource constraints, a new cost-time-quality multi-objective programming of N-N  task-resource  assignment  is  introduced,  which  can  be divided into minimize total logistics cost and  execution time,  maximize total service quality. Furthermore, by setting the different  simulation  scenarios,  the  results  show  that  if  the decision maker has a higher risk preference and pursues the optimization of single or multi-objective, the higher degree membership and satisfaction function values can be gotten with a larger   compensation   coefficient.  

### 

### 背景

**TRA** ：task-resource assignment 任务资源分配

**CLN**：Collaborative  logistics  network 协同物流网络

每一个任务（task）分为**四个阶段**：采购、运输、仓储、包装

对应的资源分为**四类**：供应商，运输公司，仓库，包装工厂

在物流网络里，物流任务的到达是随机的，也就是说在物流网络里，需求是类似的。（每个任务要做的事是差不多的）同时，物流服务集成商拥有的物流资源总量是固定的。

每个物流任务阶段可以从资源池中分配相应的物流资源来满足任务需求，但每个阶段可用的资源数量是不确定的。每个随机任务可以从存储库中选择一个或多个资源进行分配。同时物流资源可以在有限的资源下同时服务多个随机物流任务。



> **业务背景问题：物流服务集成商拥有的物流资源总量固定，但每个阶段可用的资源数量不确定？**



### 问题定义

**解决问题：**任务阶段多样化、物流任务的随机性、物流资源的模糊性，在这种情况下多阶段随机任务与模糊资源之间的动态决策非常困难。即如何选择资源的类型和数量来满足各个阶段的任务需求。当然，不同的任务，对应的成本、时间、和服务质量也不一样。考虑在时间和资源的约束条件下，多阶段的随机任务和模糊资源之间的**最优**分配方案。

**难点：**

1. **资源选择**的问题。因为资源是有限的，所以任务的每个阶段应该分配**最合适**的资源。
2. **任务选择**的问题。每个资源可以选择多个物流任务阶段，也就是有多种资源分配方案来响应物流任务需求，需要确定该物流资源分配的合适任务阶段。
3. **综合规划**。由于任务的随机性和资源的不确定性，任务开始的时间和资源的限制都是动态变化的，所以需要考虑多阶段随机任务和模糊资源进行匹配的问题

**优化目标：**

1. 成本：尽可能使的所有任务使用的总成本最低
2. 时间：尽可能使得完成所有任务所使用的时间最少
3. 服务质量：这里采用了一个模糊数（fuzzy  number）来评估顾客的满意度，即服务质量越高越好

**约束条件：**

1. 资源数目约束：
2. 时间约束：
3. 成本约束：
4. 服务质量约束：



### 基于GA的任务-资源分配模型

1. 模糊数的转换
2. **多目标降维**。将多目标问题转化为双目标问题，再将双目标问题转化为单目标问题。模糊数中的隶属函数