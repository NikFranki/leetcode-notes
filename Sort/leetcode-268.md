# leetcode 268题 缺失数字

给定一个包含 0, 1, 2, ..., n 中 n 个数的序列，找出 0 .. n 中没有出现在序列中的那个数。

## 示例1

```bash
输入: [3,0,1]
输出: 2
示例 2:
```

## 示例2

```bash
输入: [9,6,4,2,3,5,7,0,1]
输出: 8
```

### 思路

1 二分法，每次对半查找，找到中点，若中点的index与value相等，则说明缺失的数字在右边，否则在左边，退出循环是，左边界即是丢失的数字

2 排序，先排序，然后遍历数组找到下标与value不匹配的那个index，即是丢失的数字

3 异或
规则如下：

- 交换律：a^b=b^a;
- 结合律：a^b^c = a^(b^c) = (a^b)^c
- 恒等率：a^0=a
- 归零率：a^a=0
- 自反律：a^b^a=b^0=b

### 代码

```js
// binary search
var missingNumber = function(nums) {
    let l = 0, r = nums.length-1;

    while (l <= r) {
        const m = Math.floor((r-l)/2)+l;
        if (m === nums[m]) {
            l = m+1;
        } else {
            r = m-1;
        }
    }

    return l;
};

// sort
function missingNumber(nums) {
    nums.sort((a, b) => a-b);
    const len = nums.length;
    if (nums[len-1] !== len) return len;
    return nums.findIndex((item, index) => item !== index);
}

// XOR
function missingNumber(nums) {
    let miss = nums.length;
    let xOrSum = 0;
    let numOrSum = 0;

    for (let i=0; i<nums.length; i++) {
        xOrSum ^= i;
        numOrSum ^= nums[i];
    }

    xOrSum ^= miss;

    return xOrSum ^ numOrSum;
}
```

### 复杂度分析

- 时间复杂度: O(logN)/O(N)/O(1)
- 空间复杂度: O(1)
