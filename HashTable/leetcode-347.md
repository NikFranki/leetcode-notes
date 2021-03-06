# leetcode 347题 前 K 个高频元素

给定一个非空的整数数组，返回其中出现频率前 k 高的元素。

## 示例 1

```bash
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```

## 示例 2

```bash
输入: nums = [1], k = 1
输出: [1]
```

### 思路

利用小顶堆，前k个数就是小顶堆里面维护的数据

具体操作步骤:

- 先遍历数据，用一个map记录下每一个元素出现的次数
- 遍历map，先取前k个元素建堆
- 到了第k个元素或者之后的元素，都需要与堆顶的元素做对比，如果比堆顶元素小则不作处理，如果比堆顶元素大则替换堆顶元素，并且重新堆化
- 最后堆中的元素就是所需要求的前k个元素

### 代码

```js
function topKFrequent(nums, k) {
    // 初始化堆
    const heap = [,];
    const map = new Map();

    // 先计算nums每个值出现的次数,用map存储
    nums.forEach(item => {
        if (map.has(item)) {
            map.set(item, map.get(item) + 1);
        } else {
            map.set(item, 1);
        }
    });

    // 如果元素数量小于k
    if (map.size <= k) {
        return [...map.keys()];
    }

    // 如果元素数量大于k,搭建小顶堆
    let i = 0;
    map.forEach((key, value) => {
        if (i < k) {
            // 取前k个，建堆
            heap.push(key);
            // 建立前k堆
            if (i === k-1) {
                buildHeap(heap, map, k);
            }
        } else if (map.get(heap[1]) < value) {
            // 替换并且重新堆化
            heap[1] = key;
            heapify(heap, map, k, 1);
        }
        i++;
    });

    heap.shift();
    return heap;
}

// 建堆
function buildHeap(heap, map, k) {
    if (k === 1) return;
    for (let i = Math.floor(k / 2); i>=1; i--) {
        heapify(heap, map, k, i);
    }
}

// 堆化
function heapify(heap, map, k, i) {
    // 自上而下堆化
    while (true) {
        let minIndex = i;
        if (2*i <= k && map.get(heap[2*i]) < map.get(heap[i])) {
            minIndex = 2*i;
        }
        if (2*i+1 <= k && map.get(heap[2*i+1]) < map.get(heap[minIndex])) {
            minIndex = 2*i+1;
        }
        if (i !== minIndex) {
            swap(heap, i, minIndex);
            i = minIndex;
        } else {
            break;
        }
    }
}

// 交换
function swap(arr, i, j) {
    [arr[i], arr[j]] = [arr[j], arr[i]];
}
```

### 复杂度分析

- 时间复杂度: O(nlogn)
- 空间复杂度: O(n)
