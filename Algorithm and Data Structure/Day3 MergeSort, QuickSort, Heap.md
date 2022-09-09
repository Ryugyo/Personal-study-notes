## O(logN) Sorting Algorithms
1. MergeSort
   把数组分成两份左和右，两个指针分别指向左右数组第一位，谁小先放谁。

2. QuickSort
   1.0版本即是使用荷兰国旗算法逻辑，将一组数列中最后一位规定为target然后将数组变形为“target左边的数都比target小，右边的数都比target大”，再以target为界限把数组分成左右两半并丢入recursion循环排序，最终得到的就是完全sorted好的数组。2.0版本将数组变形为“targer和一众相等的数在中间，左边是小于，右边是大于”不仅固定了target的位置还固定了所有等于target的数的位置，所以复杂度比1.0更快些。

## Heap结构
Heap是一个complete binary tree结构（除了最底层外每层都是满的并且最后一层所有node连续靠左）
可以将数组转换为heap结构，i位置的左node为：$2i+1$，i位置右node为：$2i+2$，i位置的parent node为$(i-1)/2$。（i从0开始记录）

3. HeapSort
   将数组heapify（把每个parent node放入heapify方法），接着把0位和末尾交换（将最大值移动到最后），缩少heap size再次heapify，直到heap size变为0数组也就sorted完成了。

（上述code详见sortAlgorithms包）