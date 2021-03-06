# leetcode 208题 实现 Trie (前缀树)

实现一个 Trie (前缀树)，包含 insert, search, 和 startsWith 这三个操作。

## 示例 1

```bash
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // 返回 true
trie.search("app");     // 返回 false
trie.startsWith("app"); // 返回 true
trie.insert("app");   
trie.search("app");     // 返回 true
```

题解：

### 思路

利用字典树，把字符串依次存入 hash 表，转化成这种结构: {a: {b: {c: {isEnd: true}, d: {isEnd: true}}}}

查找的时候，层层往里面寻找

- 找单词: 找 abc 顺序 a-b-c-isEnd 到达末尾，abc 在前缀树中
- 找前缀，找 ab 顺序 a-b，isEnd 是 undefined，ab 在前缀树中，是别的单词的前缀

### 代码

```js
class Trie {
    constructor() {
        this.hash = {};
    }

    insert(word) {
        let hash = this.hash;
        for (const w of word) {
            if (!hash[w]) {
                hash[w] = {};
            }
            hash = hash[w];
        }
        hash.isEnd = true;
    }

    s(word) {
        let hash = this.hash;
        for (const w of word) {
            if (!hash[w]) {
                return false;
            }
            hash = hash[w];
        }
        return hash;
    }

    search(word) {
        return this.s(word).isEnd === true;
    }

    startsWith(prefix) {
        return this.s(prefix) !== false;
    }
}
```

### 复杂度分析

- 时间复杂度: O(n)
- 空间复杂度: O(n)
