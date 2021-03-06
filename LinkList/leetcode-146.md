# leetcode 146题 LRU缓存机制

运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制 。

实现 LRUCache 类：

LRUCache(int capacity) 以正整数作为容量 capacity 初始化 LRU 缓存

int get(int key) 如果关键字 key 存在于缓存中，则返回关键字的值，否则返回 -1 。

void put(int key, int value) 如果关键字已经存在，则变更其数据值；如果关键字不存在，则插入该组

「关键字-值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。

进阶：你是否可以在 O(1) 时间复杂度内完成这两种操作？

来源：力扣（LeetCode）
链接：<https://leetcode-cn.com/problems/lru-cache>
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 思路

LRU 全称 least recently used

get 获取 hash 双向链表数据，如果存在则把这个节点提取到链表的最前面，否则直接返回-1

put 如果当前的 key 已经存在 hash 双向链表中，那么直接修改这个节点的 val，否则把新节点插入到 hash 双向链表的头部

### 代码

```js
// es5
function Node(key, value) {
    this.key = key;
    this.value = value;
    this.prev = null;
    this.next = null;
}

var LRUCache = function(capacity) {
    this.count = 0;
    this.capacity = capacity;
    this.hash = {};
    this.dummyHead = new Node(); 
    this.dummyTail = new Node();
    this.dummyHead.next = this.dummyTail;
    this.dummyTail.prev = this.dummyHead;
};

/**
 * @param {number} key
 * @return {number}
 */
LRUCache.prototype.get = function(key) {
    var node = this.hash[key] || null;

    if (node === null) {
        return -1;
    }

    this.removeFromList(node);
    this.moveToHead(node);
    return node.value;
};

LRUCache.prototype.removeFromList = function(node) {
    node.prev.next = node.next;
    node.next.prev = node.prev;
};

LRUCache.prototype.moveToHead = function(node) {
    this.removeFromList(node);
    this.addToHead(node);
};

LRUCache.prototype.addToHead = function(node) {
    node.prev = this.dummyHead;
    node.next = this.dummyHead.next;
    this.dummyHead.next.prev = node;
    this.dummyHead.next = node;
};

/**
 * @param {number} key 
 * @param {number} value
 * @return {void}
 */
LRUCache.prototype.put = function(key, value) {
    let node = this.hash[key] || null;

    if (node === null) {
        if (this.count === this.capacity) {
            this.removeLRUItem();
        }
        var newNode = new Node(key, value);
        this.hash[key] = newNode;
        this.addToHead(newNode);
        this.count++;
    } else {
        node.value = value;
        this.moveToHead(node);
    }
};

LRUCache.prototype.removeLRUItem = function() {
    let tail = this.popTail();
    delete this.hash[tail.key];
    this.count--;
}

LRUCache.prototype.popTail = function() {
    let tail = this.dummyTail.prev;
    this.removeFromList(tail);
    return tail;
}

// =========

// es6
class Node {
    constructor(key, val) {
        this.key = key;
        this.val = val;
        this.prev = null;
        this.next = null;
    }
}

class LRUCache {
    constructor(capacity) {
        this.capacity = capacity;
        this.hash = {};
        this.count = 0;
        this.dummyHead = new Node();
        this.dummyTail = new Node();
        this.dummyHead.next = this.dummyTail;
        this.dummyTail.prev = this.dummyHead;
    }

    get(key) {
        let node = this.hash[key] || null;
        if (node === null) {
            return -1;
        }
        this.moveToHead(node);
        return node.val;
    }

    moveToHead(node) {
        this.removeFromList(node);
        this.addToHead(node);
    }

    removeFromList(node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    addToHead(node) {
        node.prev = this.dummyHead;
        node.next = this.dummyHead.next;
        this.dummyHead.next.prev = node;
        this.dummyHead.next = node;
    }

    put(key, value) {
        let node = this.hash[key] || null;
        if (node === null) {
            if (this.count === this.capacity) {
                this.removeLRYItem();
            }
            const newNode = new Node(key, value);
            this.hash[key] = newNode;
            this.addToHead(newNode);
            this.count++;
        } else {
            node.val = value;
            this.moveToHead(node);
        }
    }

    removeLRYItem() {
        let tail = this.popTail();
        delete this.hasn[tail.key];
        this.count--;
    }

    popTail() {
        let tail = this.dummyTail.prev;
        this.removeFromList(tail);
        return tail;
    }
}
```

### 复杂度分析

- 时间复杂度: get: O(1 ~ n) put: O(1 ~ n)
- 空间复杂度: O(n)
