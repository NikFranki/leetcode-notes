# leetcode 814题 二叉树剪枝

给定二叉树根结点 root ，此外树的每个结点的值要么是 0，要么是 1。

返回移除了所有不包含 1 的子树的原二叉树。

( 节点 X 的子树为 X 本身，以及所有 X 的后代。)

## 示例 1

```bash
输入: [1,null,0,0,1]
输出: [1,null,0,null,1]
```

## 示例 2

```bash
输入: [1,0,1,0,0,0,1]
输出: [1,null,1,null,1]
```

题解：

### 思路

递归遍历，当node的左孩子不包含1，则node.left置为null，当node的右孩子不包含1，则node.right置为null，当node.val不为1的时候，跟节点也为null，最终返回null

### 代码

```js
function pruneTree(root) {
    return containsOne(root) ? root : null;
}

function containsOne(node) {
    if (node === null) {
        return false;
    }
    var a1 = containsOne(node.left);
    var a2 = containsOne(node.right);
    if (!a1) {
        node.left = null;
    }
    if (!a2) {
        node.right = null;
    }
    return node.val === 1 || a1 || a2;
}
```

### 复杂度分析

- 时间复杂度: O(n)
- 空间复杂度: O(1)
