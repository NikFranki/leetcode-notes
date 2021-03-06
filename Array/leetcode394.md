# leetcode 394题 字符串解码

给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

来源：力扣（LeetCode）
链接：<https://leetcode-cn.com/problems/decode-string>
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

示例1

```json
输入：s = "3[a]2[bc]"
输出："aaabcbc"
```

示例2

```json
输入：s = "3[a2[c]]"
输出："accaccacc"
```

示例3

```json
输入：s = "2[abc]3[cd]ef"
输出："abcabccdcdcdef"
```

题解

## 思路

- 直接让 ] 之前的所有字符逐个入栈 stack
- 然后一个个出栈考察，顺序就是先构建内层
- 首先遇到的肯定是[]中的字母，一个个拼成子串，直到遇到 [ 停下来
- 接着遇到数字，数字出栈，组成倍数，直到遇到 “非数字”
- 现在有了字母串和倍数，就构建出局部子串，一整个子串推入栈
- 这样，一个 [] 中的子串就构建好了放在 stack 里
- 它再和可能有的别的字母一起组成子串，再一起被倍数拷贝
- 再回到 stack 里，最后将 stack 里的项剩下都是字符串， join 拼接成字符串返回

## 代码

```js
function decodeString(s) {
  let stack = []
  for (const item of s) {
    if (item !== ']') { 
      stack.push(item);
      continue;
    }
    let curr = stack.pop(); 
    let str = ''; 
    while (curr !== '[') {
      str = curr + str;
      curr = stack.pop();
    }
    let number = '';
    curr = stack.pop();
    while (!isNaN(curr)) {
      number = curr + number;
      curr = stack.pop();
    }
    stack.push(curr);
    stack.push(str.repeat(number));
  }
  return stack.join('');
}
```

## 复杂度分析

- 时间复杂度: O(n)
- 空间复杂度: O(n)
