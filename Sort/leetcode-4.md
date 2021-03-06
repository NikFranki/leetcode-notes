# leetcode 4题 寻找两个正序数组的中位数

给定两个大小为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。请你找出并返回这两个正序数组的中位数。

进阶：你能设计一个时间复杂度为 O(log (m+n)) 的算法解决此问题吗？

## 示例1

```bash
输入：nums1 = [1,3], nums2 = [2]
输出：2.00000
解释：合并数组 = [1,2,3] ，中位数 2
```

## 示例2

```bash
输入：nums1 = [1,2], nums2 = [3,4]
输出：2.50000
解释：合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
```

示例3:

```bash
输入：nums1 = [0,0], nums2 = [0,0]
输出：0.00000
```

### 思路

合并数组，排序，然后转化为一个数组的中位数

### 代码

```js
var findMedianSortedArrays = function(nums1, nums2) {
    const nums = [...nums1, ...nums2];
    nums.sort((a, b) => a-b);
    const len = nums.length;
    const mid = Math.floor(len / 2);

    if (len % 2 === 0) {
        return (nums[mid -  1] + nums[mid]) / 2;
    }
    return nums[mid];
};
```

### 复杂度分析

- 时间复杂度: O(NlogN)
- 空间复杂度: O(1)
