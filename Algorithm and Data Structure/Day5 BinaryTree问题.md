## Binary Tree问题
1. 如何判断一棵二叉树是否为搜索二叉树？
Binary Search Tree：没有重复值的二叉树且left node小于root，right node大于root。
判断：用中序遍历（左中右）如果遍历的结果是升序那么就是搜索二叉树，反之不是。
（code见binaryTree包下IsBinaryTree.java）

2. 如何判断一棵树是完全二叉树？
Complete Binary Tree：除leaf外每个节点都是left+right满，如果不满最后一层leaf也依次靠左，就叫完全二叉树。
判断：按宽度遍历，遇到的每个node如果有right没left直接返回false，在第一个条件不违规的情况下如果遇到第一个缺右或缺左的node，那么之后的所有node都必须是leaf。
（code见binaryTree包下IsCompleteTree.java）

3. 如何判断一棵树是否为满二叉树？
Full Binary Tree：满二叉树除了leaf外每个节点都必有两个node。假设一棵树最大depth D，node总数N，那么满二叉树node数一定满足$N = 2^L - 1$。
判断：写一个求最大深度的方法，再写一个求node数的方法，代入公式，成立则是，反之不是。

4. 如何判断一棵树是否为平衡二叉树？（难点）
Balanced Binary Tree：左树和右树的高度都不超过1。
判断：如果整个树是balanced binary tree，那么left tree和right tree也必然是balanced binary tree，且left和right的高度差不能超过1，只有上述三个条件都成立，才true，只要有一个不成立，就false。（递归套路）
（code见binaryTree包下IsBalancedTree.java）

重点：递归套路（见面试题13），有了递归套路可以攻克任何tree的DP（dynamic programming）问题。

5. 序列化
用#代表null，_代表node之间的分割，比如root 1有left node 2和right node 3，那么先序就是，1_2_3.
（code见binaryTree包下SequenceTree.java）