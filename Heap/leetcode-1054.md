# leetcode 1054题 距离相等的条形码

在一个仓库里，有一排条形码，其中第 i 个条形码为 barcodes[i]。

请你重新排列这些条形码，使其中两个相邻的条形码 不能 相等。 你可以返回任何满足该要求的答案，此题保证存在答案。

## 示例1

```bash
输入：[1,1,1,2,2,2]
输出：[2,1,2,1,2,1]
```

## 示例2

```bash
输入：[1,1,1,1,2,2,3,3]
输出：[1,3,1,3,2,1,2,1]
```

### 思路

1 排序 + hash

2 堆排序

### 代码

```js
function rearrangeBarcodes(barcodes) {
    const hash = {};

    for (let i=0; i<barcodes.length; i++) {
        const barcode = barcodes[i];
        hash[barcode] = (hash[barcode] || 0) + 1;
    }

    const arr = Object.keys(hash).map(item => [item, hash[item]]);
    arr.sort((a, b) => a[1] - b[1]);

    let res = new Array(arr.length);
    let i = 0;
    

    while (arr.length) {
        let [barcode, count] = arr.pop();
        while (count-- > 0) {
            if (i >= barcodes.length) {
                i = 1;
            }
            res[i] = barcode;
            i += 2;
        }
    }
    return res;
}

function rearrangeBarcodes(barcodes) {
    const hash = {};

    for (let i=0; i<barcodes.length; i++) {
        const barcode = barcodes[i];
        hash[barcode] = (hash[barcode] || 0) + 1;
    }

    const arr = Object.keys(hash).map(item => [item, hash[item]]);
    const heap = new MaxHeap(arr, function comparator(inserted, compared) {
        return inserted[1] < compared[1];
    });

    let res = new Array(arr.length);
    let i = 0;
    

    while (heap.size() > 0) {
        let [barcode, count] = heap.poll();
        while (count-- > 0) {
            if (i >= barcodes.length) {
                i = 1;
            }
            res[i] = barcode;
            i += 2;
        }
    }
    return res;
}

// max heap another implement
class Heap {
    constructor(data = [], comparator = function comparator(inserted, compared) {
        return inserted < compared;
    }) {
        this.data = data;
        this.comparator = comparator;

        this.init();
    }

    init() {
        const size = this.size();
        for (let i = Math.floor(size / 2) - 1; i >= 0; i--) {
            this.heapify(this.data, size, i);
        }
    }

    insert(val) {
        this.data.push(val);
        this.init();
    }

    poll() {
        const last = this.data.pop();
        if (this.size() === 0) {
            return last;
        }
        const returnValue = this.data[0];
        this.data[0] = last;
        this.heapify(this.data, this.size(), 0);
        return returnValue;
    }

    peek() {
        return this.data[0];
    }

    size() {
        return this.data.length;
    }
}

class MaxHeap extends Heap {
    constructor(data, comparator) {
        super(data, comparator);
    }

    heapify(arr, size, i) {
        let largetest = i;
        const left = Math.floor(2 * i + 1);
        const right = Math.floor(2 * i + 2);

        if (left < size && this.comparator(arr[largetest], arr[left])) {
            largetest = left;
        }
        if (right < size && this.comparator(arr[largetest], arr[right])) {
            largetest = right;
        }

        if (largetest !== i) {
            [arr[i], arr[largetest]] = [arr[largetest], arr[i]];
            this.heapify(arr, size, largetest);
        }
    }
}
```

### 复杂度分析

- 时间复杂度: O(NlogN)
- 空间复杂度: O(N)
