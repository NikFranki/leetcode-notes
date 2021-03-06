# leetcode 232题 用栈实现队列

请你仅使用两个栈实现先入先出队列。队列应当支持一般队列的支持的所有操作（push、pop、peek、empty）：

实现 MyQueue 类：

void push(int x) 将元素 x 推到队列的末尾
int pop() 从队列的开头移除并返回元素
int peek() 返回队列开头的元素
boolean empty() 如果队列为空，返回 true ；否则，返回 false

说明：

你只能使用标准的栈操作 —— 也就是只有 push to top, peek/pop from top, size, 和 is empty 操作是合法的。
你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可。

进阶：

你能否实现每个操作均摊时间复杂度为 O(1) 的队列？换句话说，执行 n 个操作的总时间复杂度为 O(n) ，即使其中一个操作可能花费较长时间。

来源：力扣（LeetCode）
链接：<https://leetcode-cn.com/problems/implement-queue-using-stacks>
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 示例 1

```json
输入：
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
输出：
[null, null, null, 1, 1, false]

解释：
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
```

题解：

### 思路

- 使用两个栈 s1, s2
- push 操作时，从 s1 里面依次入栈
- peek 操作时，先判断 s2 是否为空，若为空，从 s1 的元素依次出栈，并同时从 s2 依次进栈，这样 s2 就可以想队列头一样，模拟队列先进先出
- pop 操作时，先 peek 操作，然后让 s2 执行出栈
- empay 当 s1、s2 同时都为空才为true

### 代码

```js
function Stack() {
    this.arr = [];
    this.length = 0;

    this.push = function(val) {
        this.arr.push(val);
        this.length++;
    }

    this.pop = function() {
        if (this.length === 0) {
            return -1;
        }
        this.length--;
        return this.arr.pop();
    }

    this.peek = function() {
        if (this.length === 0) {
            return -1;
        }
        return this.arr[this.length - 1];
    }

    this.empty = function() {
        return this.length === 0;
    }
}

function MyQueue() {
    this.s1 = new Stack();
    this.s2 = new Stack();

    this.push = function(val) {
        this.s1.push(val);
    }

    this.pop = function() {
        this.peek();
        return this.s2.pop();
    }

    this.peek = function() {
        if (this.s2.empty()) {
            while (!this.s1.empty()) {
                this.s2.push(this.s1.pop());
            }
        }
        return this.s2.peek();
    }

    this.empty = function() {
        return this.s1.empty() && this.s2.empty();
    }
}
```

### 复杂度分析

- 时间复杂度: O(n)
- 空间复杂度: O(1)
