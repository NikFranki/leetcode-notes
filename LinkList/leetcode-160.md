# leetcode 160题 相交链表

编写一个程序，找到两个单链表相交的起始节点。

## 如下面的两个链表

![ss](http://qiniu.sevenyuan.cn/link-list.png)

在节点 c1 开始相交。

### 思路

利用双指针

pa、pb同时在链表a、链表b上行走，假设链表b比较短，pb先走完，会去到链表a的头结点开始继续走

pa在链表上走完后，会继续去到链表b上的头结点继续走，最终会消除高度差，相遇的节点即为要求出的节点

### 代码

```js
function getIntersectionNode(l1, l2) {
    if (l1 === null || l2 === null) {
        return null;
    }

    var pa = l1, pb = l2;

    while (pa || pb) {
        if (pa === pb) {
            return pa;
        }
        pa = pa === null ? l2 : pa.next;
        pb = pb === null ? l1 : pb.next;
    }

    return null;
}
```

### 复杂度分析

- 时间复杂度: O(m + n)
- 空间复杂度: O(1)
