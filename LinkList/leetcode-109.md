# 有序链表转换二叉搜索树

## 思路

先把链表的值逐一存入数组

利用二分，把数组的值先确定中位数为root，然后根据root划分左子树、右子树

### 代码

```js
function sortedListToBST(head) {
    var arr = [];

    while (head) {
        arr.push(head.val);
        head = head.next;
    }

    function buildBST(start, end) {
        if (start > end) return null;
        var mid = start + end >>> 1;
        var root = new TreeNode(arr[mid]);
        root.left = buildBST(start, mid - 1);
        root.right = buildBST(mid + 1, end);
        return root;
    }

    return buildBST(0, arr.length - 1);
}
```

### 复杂度分析

- 时间复杂度：O(nlogn)
- 空间复杂度：O(n)
