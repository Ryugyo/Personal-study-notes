# Graph
常见类型：directed graph, undirected graph, complete graph（每个vertex都能链接到其余所有vertices）, finite graph（vertex和edge都有限）, infinite graph, connected graph

graph的算法简单，但是表达graph的结构很多，难点在于相同的算法写法也不同。
3种graph表达结构例子：
Adjacency List：记录每个vertex通过edge到达的其余nodes
Adjacency Matrix：正方形的matrix，row和column都是vertices，然后（vertex1，vertex2）的数值就是两个vertex之间的距离，自己到自己是0，如果没有路写作正无穷
Array：例如[5,2,2,4,2,1]，0指向5，1指向2，2指向2，3指向4，4指向2，5指向1
聪明的做法是将面试里给的数据结构类型转换成平时最喜欢使用的简单结构，如此就不用所有结构都记一遍独立的算法。

简单结构推荐：
HashMap储存vertex，hashset储存edges
转换结构例子：
将matrix储存的信息转换为graph
（code见graph包下MatrixToGraph.java）

## 遍历方法
BFS（breadth-first search）：看一个当前vertex，然后将他out出去的所有其他vertex（如果是undirected的话就是当前vertex连接到的所有其他vertex）放入序列中，接着看下一个，重复上述操作，直到遍历完所有的vertices。
DFS（depth-first search）：看一个当前vertex，然后只看它延伸出去的任何一个vertex，接着继续走下去直到这一列走到尽头（当某个vertex没有任何延申），然后回头，继续重复，直到所有vertices都被遍历。
BFS靠queue实现，DFS靠stack实现

Topological Sort：
拓扑排序：比方说安排项目，有些工程是依赖其他工程需要在其他工程都完成得基础上才可以开工，那么如何安排工作的顺序，就叫拓扑排序。
具体操作：假设一个graph，每个vertex指向另外的vertex说明后者需要前者完成后才可以开工，那么就可以：先将入度为0的vertex（意思是没有任何其他vertex指向此vertex）放入list，然后删除当前vertex所有的影响（out的edge），然后再加入下一个直到所有vertex遍历完成。

（code见graph包下HashMapGraph.java）

## 经典算法
假设给一个undirected graph，edge自带权重，将此graph多余的edge删除并且保证保证连通性还做到总权重最小。
1. kruskal算法（要求undirected graph）
首先将graph的edges全部剔除。将权重最小的edge加上，检查此时graph有没有形成loop，没有的话加第二小的，再检查，再加，如果形成loop，就不加，循环直到所有edge都被检查一遍，那么此时的graph就是总权重最小且保证连通性的graph。
如何判断是否有loop？每个node都各自独立设置一个set，假设第一个edge连接的是vertex A和B，就将AB所在的两个set合并成一个，第二个edge也是连接A和B，那么检查所有set如果发现AB的set指向的是同一个就判断此edge会构成loop，所以不添加。

（code见graph包下Kruskal.java）

2. prim算法（要求undirected graph）
创建一个hashset先添加一个node，然后解锁此node上所有的edge，从解锁的edge里挑一个weight最小的，将edge的to node添加后又可以解锁另外一些边（但必须无视连接了已经添加进set里的的node的edge），继续重复操作，直到所有的node都被添加进set，说明graph已遍历。

（code见graph包下Prim.java）

单元最短路径算法：求一个node到其他所有node最短距离
1. Dijkstra算法（可以有weight为负数的edge，但不能有weight为负数的loop，不然题就无解了）
做一张表，初始设置node A到所有其他node的距离为正无穷，然后选一个最小记录的node（一开始必然是A，因为A到A是0），然后遍历所有A延申出的edge，假设有edge A到B是3，那么就用0+3（0是A到A的距离，加上A到B的距离3）把B处的无穷大替换掉，接着继续找累计最小的node，然后用A到node的距离+edge的值替换掉已储存的距离（如果新的更小），直到表中的所有node都被如此处理后，最后的表就是A到所有其他node最短的距离。
