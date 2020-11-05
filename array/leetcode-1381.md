# leetcode 394题 字符串解码

给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

来源：力扣（LeetCode）
链接：<https://leetcode-cn.com/problems/decode-string>
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 示例1

```json
输入：s = "3[a]2[bc]"
输出："aaabcbc"
```

## 示例2

```json
输入：s = "3[a2[c]]"
输出："accaccacc"
```

## 示例3

```json
输入：s = "2[abc]3[cd]ef"
输出："abcabccdcdcdef"
```

题解

### 思路

用一个数组来模拟栈，用一个变量来记录当前栈顶的位置

- 在 push 的时候, 先判断 top 的位置是否达到了 maxSize - 1，没有的话，top++ 并添加一个元素
- 在 pop 的时候, 先判断 top 是否是-1，是直接返回 -1，否则 top-- 并返回栈顶元素
- 在 increment 的时候, 直接对于栈底的第 k 个元素加 val

### 代码

```js
function CustomStack(maxSize) {
    this.maxSize = maxSize;
    this.arr = new Array(maxSize);
    this.top = -1;

    this.push = function(val) {
        if (this.top !== this.maxSize - 1) {
            this.top++;
            this.arr[this.top] = val;
        }
    }

    this.pop = function() {
        if (this.top === -1) {
            return -1;
        }
        this.top--;
        return this.arr[this.top + 1];
    }

    this.increment = function(k, val) {
        var lim = Math.min(k, this.top + 1);
        for (var i=0; i<lim; i++) {
            this.arr[i] += val;
        }
    }
}
```

### 复杂度分析

- 时间复杂度: push pop 构造函数操作的复杂度为O(1)，increment 时间复杂度为O(k)
- 空间复杂度: O(maxSize)
