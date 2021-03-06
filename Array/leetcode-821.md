# leetcode 821题 字符的最短距离

给定一个字符串 S 和一个字符 C。返回一个代表字符串 S 中每个字符到字符串 S 中的字符 C 的最短距离的数组。

## 示例 1

输入: S = "loveleetcode", C = 'e'
输出: [3, 2, 1, 0, 1, 0, 0, 1, 2, 2, 1, 0]
说明:

字符串 S 的长度范围为 [1, 10000]。
C 是一个单字符，且保证是字符串 S 里的字符。
S 和 C 中的所有字母均为小写字母。

来源：力扣（LeetCode）
链接：<https://leetcode-cn.com/problems/shortest-distance-to-a-character>
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

题解：

### 思路

利用前后遍历

第一次遍历，从前往后开始遍历，首先记录第一个出现C在S中的位置prev，遇到当前的字符与C相等，更新prev为当前index，把index与prev的差值作为结果，存到一个数组里面

第二次遍历，从后往前遍历，首先记录最后一个出现C在S中出现的位置last，遇到当前的字符与C相等，更新last，此时计算的index与last的差值需要与当前数组里面的对应下标的结果进行对比，取小的重新赋值

### 代码

```js
var shortestToChar = function(S, C) {
    // 利用前后遍历

    // 先顺着遍历（从前往后）
    var len = S.length;
    // 第一次C出现在S的位置
    var prev = S.indexOf(C);
    // 结果数组（存放每一个字符距离C的结果）
    var res = new Array(len);
    for (var i=0; i<len; i++) {
        if (S[i] === C) {
            prev = i;
        }
        res[i] = Math.abs(prev - i);
    }

    // 逆着遍历
    // C在字符串S中最后一次出现的位置
    var last = S.lastIndexOf(C);
    for (var j=len-1; j>0; j--) {
        if (C === S[j]) {
            last = j;
        }
        res[j] = Math.min(Math.abs(last - j), res[j]);
    }

    return res;
};

```

### 复杂度分析

- 时间复杂度: O(n)
- 空间复杂度: O(n)
