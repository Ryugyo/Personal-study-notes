## Linked-list
基础类型题：
1. 单链表（singly linked list）和双链表（double linked list）如何反转？
2. 如何删除？

## Stack and Queue
Stack: Last in first out
Queue: First in first out
用doubly linked-list很好实现，但用array略繁琐：
Stack：FILO正常使用array即可，
Queue：FIFO需要环形数组（即两个变量记录pop和push的index，到最后一位后需要回到index 0）
**（code见linkedList包）**

## Recursion
时间复杂度公式：
$T(N) = aT(N/b) + O(N^d)$
a指code中递归调用的次数（假设每轮调用两次递归，一次left一次right，那么a就是2），N/b指子问题是总问题的的几分之几（例如left和right刚好是整个数组的一半一半，那么N/b就是N/2），最后的big O指除了递归外剩余操作的复杂度。

如果$log(b,a) < d$，复杂度就为$O(N^d)$;
如果$log(b,a) > d$，复杂度就为$O(N^log(b,a))$；
如果$log(b,a) == d$，复杂度就为$O(N^d  logN)$。

## HashMap and HashSet
HashMap：
```
HashMap<Integer, String> map = new HashMap<>();
```
拥有key和对应value的非常快的Map，使用put添加或删改，get获取。
HashSet：
```
HashSet<String> set = new HashSet<>();
```
只有一个key的结构，用add添加，通过HashMap实现。

重点：hash结构无论add，delete，update，和在使用时时间复杂度都是O(1)。


## TreeMap
比HashMap强的点在于，就算put的顺序是乱序，TreeMap也可以把key自动排序，因此可以使用譬如floorKey（离input key最近的比input小的key）和ceilingKey（离input key最近的比input大的key）方法。但不如HashMap快，TreeMap的时间复杂度是O(logN)。