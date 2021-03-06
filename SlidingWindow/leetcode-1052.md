# leetcode 1052题 爱生气的书店老板

今天，书店老板有一家店打算试营业 customers.length 分钟。每分钟都有一些顾客（customers[i]）会进入书店，所有这些顾客都会在那一分钟结束后离开。

在某些时候，书店老板会生气。 如果书店老板在第 i 分钟生气，那么 grumpy[i] = 1，否则 grumpy[i] = 0。 当书店老板生气时，那一分钟的顾客就会不满意，不生气则他们是满意的。

书店老板知道一个秘密技巧，能抑制自己的情绪，可以让自己连续 X 分钟不生气，但却只能使用一次。

请你返回这一天营业下来，最多有多少客户能够感到满意的数量。

## 示例 1

```bash
输入：customers = [1,0,1,2,1,1,7,5], grumpy = [0,1,0,1,0,1,0,1], X = 3
输出：16
解释：
书店老板在最后 3 分钟保持冷静。
感到满意的最大客户数量 = 1 + 1 + 1 + 1 + 7 + 5 = 16.
```

### 思路

滑动窗口

- left right 都是从下标0开始
- 首先计算满意的客户量
- 其次计算用户不满意的客户量
- 这里面注意，X分钟（区间技能），如果滑动窗口超过这个X，就要去减去左边的不满意的用户量（如果left对应的是生气的话）

### 代码

```js
var maxSatisfied = function(customers, grumpy, X) {
    let max = 0, result = 0, left = 0, right = 0, temp = 0;
    while (right < customers.length) {
        result += grumpy[right] ? 0 : customers[right];
        temp +=  grumpy[right] ? customers[right] : 0;
        if (right - left + 1> X) {
            temp -= grumpy[left] ? customers[left] : 0;
            left++;
        }
        right++;
        max = Math.max(max, temp);
    }
    return result + max;
}
```

### 复杂度分析

- 时间复杂度: O(N)
- 空间复杂度: O(1)
