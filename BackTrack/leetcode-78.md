# leetcode 78题 子集

给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

## 示例

```bash
输入: nums = [1,2,3]
输出:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

### 思路

递归来实现子集枚举

- 记录当前位置 cur ，原序列长度 n
- 原序列中的每个位置在答案序列中的状态有选中或者不选中两种
- t 数组存放已经被选中的数字
- 在进入 dfs(cur, n)之前[0, cur-1]位置的状态是确定的，[cur, n-1]位置是不确定的
- dfs(cur, n)需要确定 cur 位置的状态，然后求解子问题dfs(cur+1, n)
- 对于 cur 位置，需要考虑取或者不取，如果取，需要把nums[cur]放入到临时数组t，再执行dfs(cur+1, n)，执行结束后对 t 进行回溯
- 如果不取，则直接执行dfs(cur+1, n)
- 在整个递归调用过程中，cur 是由小变大，当达到 n 时，记录档案并终止递归

### 代码

```js
function subsets(nums) {
    const n = nums.length;
    const ans = [];
    const t = [];

    const dfs = (cur) => {
        if (cur === n) {
            ans.push(t.slice());
            return;
        }
        t.push(nums[cur]);
        dfs(cur+1);
        t.pop();
        dfs(cur+1);
    };

    dfs(0);
    return ans;
}
```

### 复杂度分析

- 时间复杂度: O(n*2^n)
- 空间复杂度: O(n)
