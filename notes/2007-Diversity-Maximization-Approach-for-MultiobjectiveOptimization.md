### Diversity Maximization Approach for Multi objective Optimization

基本思路无非就是目标函数加权或者绘制出pareto curve。可以证明的是每个选定参数加权目标函数得到的解其实都是在pareto curve上面的。不过在目标函数很多的时候，其实得到pareto curve是不太现实的，计算量略大。而且并不是解越多就越好。

如果是用来做决策支持的，所以求解过程不求得到全部的解，但是需要得到的每一个解差异足够大，这样在取舍的时候相对容易一些。基于此，在得到第一个解(加权目标函数)之后，把这个解重新加回到原问题里面，要求新的解跟已有解的差异最大化，以此类推。就可以在任何时候停止这个算法，但是可以确保得到的几个解差异是足够大的。

实际应用中，这样计算量大大减少，解之间的差异也足够大。如果需要话pareto curve，就多拿几个解，对pareto curve的全貌也有个大概理解了。