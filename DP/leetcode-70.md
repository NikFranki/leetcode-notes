# leetcode 70题 爬楼梯

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。

## 示例 1

```bash
输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶
```

## 示例 2

```bash
输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶
```

题解：

### 思路

使用动态规划的思想，把问题划分成一系列的子问题，最终还原于最终问题的求解

### 代码

```js
const climbStairs = (n) => {
    const arr = [];
    arr[1] = 1;
    arr[2] = 2;

    for (let i=3; i<=n; i++) {
        arr[i] = arr[i-1] + arr[i-2];
    }

    return arr[n];
}

const climbStairs = (n) => {

    let prev = 1;
    let cur = 1;

    for (let i=2; i<=n; i++) {
        const temp = cur;
        cur += prev;
        prev = temp;
    }

    return cur;
}
```

### 复杂度分析

- 时间复杂度: O(n)
- 空间复杂度: O(n)
