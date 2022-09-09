## BucketSort
将数组的最大值最小值选取出来，根据最大最小值创建很多桶，然后将数字塞入桶内，再sort每个桶，然后按照桶从小到大的顺序将桶内数据倒出，就完成了从小到大的排序。

改进版（RadixSort）：创建0-9共十个桶，首先按照个位将数字放入对应的桶，再依次倒出后按十位数依次放入桶，再倒出最后按百位放入桶，最后倒出的数字就是按照从小到大顺序排列的有序数列。

## Sort算法的稳定性和时间/空间复杂度
1. SelectionSort
   $时间O(N^2) 空间O(1)$, 无法维持稳定性
2. BubbleSort
   $时间O(N^2) 空间O(1)$, 如果遇到==的情况下不交换就能维持稳定性，否则就无法维持稳定性
3. InsertionSort
   $时间O(N^2) 空间O(1)$, 如果遇到==不交换就能维持稳定性
4. MergeSort
   $时间O(NlogN) 空间O(N)$, merge时遇到==先处理左边（先把左边放入数组）就能维持稳定性，反之则不行（比如小和问题改良后的merge算法）
5. QuickSort（随机）
   $时间O(NlogN) 空间O(logN)$, 无法做到稳定，比如一个数组[6,7,6,6,3]和比较值5，当指针指向3时partition过程会把3和第一个6做交换，所以第一个6会跑到两个6之后，因此做不到稳定
6. HeapSort
   $时间O(NlogN) 空间O(1)$, heapify过程无法做到稳定
7. BucketSort, RadixSort
   $O(Nd)$, 稳定性佳，只要不基于比较的sort都可以维持稳定性

基于比较的算法，有没有时间复杂度在$O(NlogN)$以下？不行！
时间复杂度$O(NlogN)$且空间复杂度$O(1)$并且能维持稳定性的算法？没有！
所以每个算法都有优劣需要根据实际情况选择。

结论：一般sort选择quicksort，根据实验情况quicksort比heap和merge都要快。需要稳定性时一般用merge。还可以充分利用$O(N^2)$和$O(NlogN)$各自的优势构建混合排序算法，顺便还得考虑稳定性。

## Binary Tree
Root：顶node
inner node：中间的node
leaf node：最底层没有child的node
depth：深度，root是0，下一层是1，以此类推
height：此node最高的高度，比如一个3层full binary tree，root的height就是2，第二层的height就是1，最后一层的leaf的height就是0.

递归遍历二叉树每个节点都能回来3次，在此之上可以进阶出三种顺序的遍历：
先序：对于所有sub tree，都是先打印root再打印leaf node和right node；
中序：先打印左，再打印head，再打印右；
后序：先打印右，在打印head，再打印左。

不用递归的话，可以靠stack：
先序：放入root，从stack弹出root，打印，再放入弹出node的right再放入left，弹出，打印，继续循环；
中序：准备一个stack，将root和其所有的左node全push进去，随后弹出打印，再将right node和其所有left node全push进，再弹出再打印，以此类推；
后序：准备两个stack，主stack和辅stack，主stack放入root，弹出，放入辅stack，主stack放入弹出的左再右，持续循环直到主stack没有elem。然后把辅stack的elem弹出打印，就是中序的效果。

宽度遍历：
用queue，先进root，弹出打印，再放左后放右，弹出再打印，直到queue为empty。
（code见binaryTree包下BinaryTree.java）