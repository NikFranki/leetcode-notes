# leetcode 61题 旋转链表

给定一个链表，旋转链表，将链表每个节点向右移动 k 个位置，其中 k 是非负数。

## 示例 1

```bash
输入: 1->2->3->4->5->NULL, k = 2
输出: 4->5->1->2->3->NULL
解释:
向右旋转 1 步: 5->1->2->3->4->NULL
向右旋转 2 步: 4->5->1->2->3->NULL
```

## 示例 2

```bash
输入: 0->1->2->NULL, k = 4
输出: 2->0->1->NULL
解释:
向右旋转 1 步: 2->0->1->NULL
向右旋转 2 步: 1->2->0->NULL
向右旋转 3 步: 0->1->2->NULL
向右旋转 4 步: 2->0->1->NULL
```

### 思路

统计出链表的长度，链表移动 len - k 次

### 代码

```js
function rotateRight(head, k) {
    if (head === null) {
        return head;
    }

    var curr = head;
    var len = 1;
    while (curr.next !== null) {
        curr = curr.next;
        len++;
    }
    curr.next = head;
    k %= len;
    for (var i=0; i<len-k; i++) {
        head = head.next;
        curr = curr.next;
    }
    curr.next = null;
    return head;
}
```

### 复杂度分析

- 时间复杂度: O(n)
- 空间复杂度: O(1)
