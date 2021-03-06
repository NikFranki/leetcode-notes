# leetcode 47题 全排列 II

给定一个可包含重复数字的序列 nums ，按任意顺序 返回所有不重复的全排列。

## 示例1

```bash
输入：nums = [1,1,2]
输出：
[[1,1,2],
 [1,2,1],
 [2,1,1]]
```

## 示例2

```bash
输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

### 思路

递归 + 回溯

最值问题，不要重复的话，就一定需要用到剪枝，所以当i>0 && nums[i] === nums[i-1]就需要略过

### 代码

```js
function permuteUnique(nums) {
    const ans = [];
    const vis = new Array(nums.length).fill(false);
    const backtrack = (idx, perm) => {
        if (idx === nums.length) {
            ans.push(perm.slice());
            return;
        }

        for (let i=0; i<nums.length; ++i) {
            if (vis[i] || (i>0 && nums[i] === nums[i-1]) && !vis[i-1]) {
                continue;
            }
            perm.push(nums[i]);
            vis[i] = true;
            backtrack(idx+1, perm);
            vis[i] = false;
            perm.pop();
        }
   };
   nums.sort((a, b) => a-b);
   backtrack(0, []);
   return ans;
}
```

### 复杂度分析

- 时间复杂度: O(n*n^2)
- 空间复杂度: O(n)
