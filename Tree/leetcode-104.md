# leetcode 104题 二叉树的最大深度

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

## 示例

给定二叉树 [3,9,20,null,null,15,7]，

```bash
   3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度 3 。

### 思路

使用广度优先搜索，遍历一层，深度+1，直到所有的节点遍历完成，返回最终的深度。

### 代码

```js
function maxDepth(root) {
    if (root === null) {
        return 0;
    }
    return bfs(root);
}

function bfs(root) {
    var queue = [root];
    var depth = 0;

    while (queue.length) {
        var size = queue.length;
        while (size) {
            var node = queue.shift();
            if (node.left) {
                queue.push(node.left);
            }
            if (node.right) {
                queue.push(node.right);
            }
            size--;
        }
        depth++;
    }
    return depth;
}
```

### 复杂度分析

- 时间复杂度: O(n)
- 空间复杂度: O(n)
