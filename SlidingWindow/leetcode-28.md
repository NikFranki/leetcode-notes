# leetcode 28题 实现 strStr()

实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

## 示例1

```bash
输入: haystack = "hello", needle = "ll"
输出: 2
```

## 示例2

```bash
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

### 思路

方法1：滑动窗口

- 不断移动haystack里面的窗口，滑动幅度为start+l
- 当前窗口等于needle，找到返回当前下标

方法2：双指针

haystack pn 指针 needle pl 指针

- 找到needle的第一个字符存在于haystack中的下标pn
- 计算最大的匹配字符串
- 当needle中的所有字符都被找到了，那么返回她的开始下标
- 否则，回溯

### 代码

```js
// slide window
const strStr = (haystack, needle) => {
    const n = haystack.length;
    const l = needle.length;

    for (let start=0; start<n-l+1; start++) {
        if (haystack.substring(start, start+l) === needle) {
            return start;
        }
    }

    return -1;
}

// double pointer
const strStr = (haystack, needle) => {
    const n = haystack.length;
    const l = needle.length;

    let pn = 0;
    while (pn < n-l+1) {
        while (pn < n-l+1 && haystack.charAt(pn) !== needle.charAt(0)) {
            pn++;
        }

        let pl = 0;
        let currLen = 0;
        while (pl < l && pn < n && haystack.charAt(pn) === needle.charAt(pl)) {
            pn++;
            pl++;
            currLen++;
        }

        if (currLen === l) {
            return n-l;
        }

        pn = pn - currLen + 1;
    }

    return -1;
}
```

### 复杂度分析

- 时间复杂度: O((n-l)*n)
- 空间复杂度: O(1)
