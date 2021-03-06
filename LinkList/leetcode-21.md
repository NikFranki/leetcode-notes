# leetcode 21题 合并两个有序链表

将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

## 示例 1

```bash
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

### 思路

使用 prehead prev 记录 l1 l2 走过的节点，当前 l1 当前的值小于 l2 当前的值，prev.next 指向 l1并且 l1 向后移动一位，反则指向 l2 并且 l2 向后移动一位

当两者都有其一为 null 时，则让 prev.next 指向不为空的那个节点

最终返回 prehead 的 next

### 代码

```js
var mergeTwoLists = function(l1, l2) {
    var prehead = prev = new ListNode(-1);
    while (l1 !== null && l2 !== null) {
        if (l1.val <= l2.val) {
            prev.next = l1;
            l1 = l1.next;
        } else {
            prev.next = l2;
            l2 = l2.next;
        }
        prev = prev.next;
    }
    if (l1 === null) {
        prev.next = l2;
    }
    if (l2 === null) {
        prev.next = l1;
    }
    return prehead.next;
};
```

### 复杂度分析

- 时间复杂度: O(n)
- 空间复杂度: O(1)
