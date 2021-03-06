# leetcode 1456题 定长子串中元音的最大数目

给你字符串 s 和整数 k 。

请返回字符串 s 中长度为 k 的单个子字符串中可能包含的最大元音字母数。

英文中的 元音字母 为（a, e, i, o, u）。

## 示例1

```bash
输入：s = "abciiidef", k = 3
输出：3
解释：子字符串 "iii" 包含 3 个元音字母。
```

## 示例2

```bash
输入：s = "aeiou", k = 2
输出：2
解释：任意长度为 2 的子字符串都包含 2 个元音字母。
```

## 示例3

```bash
输入：s = "leetcode", k = 3
输出：2
解释："lee"、"eet" 和 "ode" 都包含 2 个元音字母。
```

### 思路

双指针

### 代码

```js
var maxVowels = function(s, k) {
    let i = 0, j = 0, res = 0, temp = 0;
    const set = new Set(['a', 'e', 'i', 'o', 'u'])
    while (j < k) {
        if (set.has(s[j])) {
            temp++;
        }
        j++;
        if (j === k) {
            res = Math.max(res, temp);
        }
    }

    while (j < s.length) {
        if (set.has(s[i])) {
            temp--;
        }
        i++;
        if (set.has(s[j])) {
            temp++;
        }
        j++;
        res = Math.max(res, temp);
    }

    return res;
};
```

### 复杂度分析

- 时间复杂度: O(N)
- 空间复杂度: O(1)
