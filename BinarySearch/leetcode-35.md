# leetcode 35题 搜索插入位置

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。

## 示例 1

```bash
输入: [1,3,5,6], 5
输出: 2
```

## 示例 2

```bash
输入: [1,3,5,6], 2
输出: 1
```

## 示例 3

```bash
输入: [1,3,5,6], 7
输出: 4
```

## 示例 4

```bash
输入: [1,3,5,6], 0
输出: 0
```

### 思路

利用二分法，如果找到target就直接返回当前找到的index，若没有找到，就直接返回左指针

### 代码

```js
var searchInsert = function(nums, target) {
    var left = 0, right = nums.length - 1;

    while (left <= right) {
        let mid = Math.floor((right - left) / 2) + left;

        const result = nums[mid];
        if (result === target) {
            return mid;
        } else if (result > target) {
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    return left;
};
```

### 复杂度分析

- 时间复杂度: O(logn)
- 空间复杂度: O(1)
