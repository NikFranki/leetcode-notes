# leetcode 24题 两两交换链表中的节点

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

## 示例 1

```bash
输入：head = [1,2,3,4]
输出：[2,1,4,3]
```

## 示例 2

```bash
输入：head = []
输出：[]
```

## 示例 3

```bash
输入：head = [1]
输出：[1]
```

### 思路

利用递归的思路

递归的终止条件是，当前节点为空，或者当前节点的下一个节点为空

设置三个节点，改变三个节点的指向

### 代码

```js
function swapPairs(head) {
    if (head === null || head.next === null) {
        return head;
    }

    var first = head;
    var second = head.next;
    var temp = second.next;

    second.next = first;
    first.next = swapPairs(temp);

    return second;
}
```

### 复杂度分析

- 时间复杂度: O(n)
- 空间复杂度: O(n)
