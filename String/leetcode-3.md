# leetcode 3题 无重复字符的最长子串

给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

## 示例 1

```bash
输入: "abcabcbb"
输出: 3
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

## 示例 2

```bash
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

示例 3

```bash
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

### 思路

利用 slide window，通过扩大、收缩窗口，枚举不重复子串的窗口的大小，枚举结束，即可得到结果

注意：

- 使用两个指针代表某个子串的左右边界，左指针代表枚举子串的左边界，右指针代表子串的右边界
- 每一次开始，左指针会向右移动一个单位，代表枚举子串的起始位置，然后不断移动右指针，移动过程中，需要保证子串是不重复的，移动结束后，这个子串就是无重复的子串。
- 枚举结束，得到最长子串的长度

### 代码

```js
function lengthOfLongestSubstring(str) {
    // 利用slide window，左右指针的移动，通过扩大、收缩窗口，不断更新结果
    const set = new Set();
    const n = str.length;
    let ans = 0, rk = -1;
    for (let i=0; i<n; i++) {
        if (i !== 0) {
            set.delete(str.charAt(i-1));
        }

        while (rk+1 < n && !set.has(str.charAt(rk+1))) {
            set.add(str.charAt(rk+1));
            rk++;
        }

        ans = Math.max(ans, rk-i+1);
    }

    return ans;
}
```

### 复杂度分析

- 时间复杂度: O(n)
- 空间复杂度: O(n)
