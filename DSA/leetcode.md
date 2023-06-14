本文收集了前端面试中常见的leetcode算法题，并配套了图文解法和代码，本人也在持续学习算法中，后续会一直更新~

# 数组

## 704.二分查找

> 给定一个 `n` 个元素有序的（升序）整型数组 `nums` 和一个目标值 `target` ，写一个函数搜索 `nums` 中的 `target`，如果目标值存在返回下标，否则返回 `-1`。
>
> **示例 1:**
>
> ```
> 输入: nums = [-1,0,3,5,9,12], target = 9
> 输出: 4
> 解释: 9 出现在 nums 中并且下标为 4
> ```
>
> **示例 2:**
>
> ```
> 输入: nums = [-1,0,3,5,9,12], target = 2
> 输出: -1
> 解释: 2 不存在 nums 中因此返回 -1
> ```
>
> **提示：**
>
> 1. 你可以假设 `nums` 中的所有元素是不重复的。
> 2. `n` 将在 `[1, 10000]`之间。
> 3. `nums` 的每个元素都将在 `[-9999, 9999]`之间。

### 二分查找

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_14_iShot_2023-06-14_14.32.01.gif" alt="iShot_2023-06-14_14.32.01" style="zoom:80%;" />

- 时间复杂度：$O(logn)$，其中 n 是数组的长度。
- 空间复杂度：$O(1)$。

```typescript
function search(nums: number[], target: number): number {
    let low = 0;
    let high = nums.length - 1;
    while (low <= high) {
        let mid = Math.floor((low + high) / 2);
        if (nums[mid] < target) {
            low = mid + 1;
        }
        else if (nums[mid] > target) {
            high = mid - 1;
        }
        else {
            return mid
        }
    }
    return -1
};
```



## 27.移除元素

> 给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。
>
> 不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并**原地**修改输入数组。
>
> 元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。
>
> 示例 1: 给定 nums = [3,2,2,3], val = 3, 函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。 你不需要考虑数组中超出新长度后面的元素。
>
> 示例 2: 给定 nums = [0,1,2,2,3,0,4,2], val = 2, 函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。
>
> **你不需要考虑数组中超出新长度后面的元素。**

### 双指针

时间复杂度：O(n)

空间复杂度：O(1)

![iShot_2023-05-09_15.15.27](https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_09_iShot_2023-05-09_15.15.27.gif)

```typescript
function removeElement(nums: number[], val: number): number {
    let slowIndex = 0;
    for (let fastIndex = 0; fastIndex < nums.length; fastIndex++) {
        if (val !== nums[fastIndex]) {
            nums[slowIndex++] = nums[fastIndex];
        }
    }
    return slowIndex;
};
```



## 977.有序数组的平方

> 给你一个按 非递减顺序 排序的整数数组 nums，返回 每个数字的平方 组成的新数组，要求也按 非递减顺序 排序。
>
> 示例 1： 输入：nums = [-4,-1,0,3,10] 输出：[0,1,9,16,100] 解释：平方后，数组变为 [16,1,0,9,100]，排序后，数组变为 [0,1,9,16,100]
>
> 示例 2： 输入：nums = [-7,-3,2,3,11] 输出：[4,9,9,49,121]

### 双指针

时间复杂度：O(n)

空间复杂度：O(1)

![iShot_2023-05-09_15.20.11](https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_09_iShot_2023-05-09_15.20.11.gif)

```typescript
function sortedSquares(nums: number[]): number[] {
    let result = Array.of(nums.length);
    let k = nums.length - 1;
    let left = 0;
    let right = nums.length - 1;
    while (left <= right) {
        if (nums[left] * nums[left] > nums[right] * nums[right]) {
            result[k--] = nums[left] * nums[left];
            left++;
        } else if (nums[left] * nums[left] <= nums[right] * nums[right]) {
            result[k--] = nums[right] * nums[right];
            right--;
        }
    }
    return result;
};
```



## 209.长度最小的子数组

> 给定一个含有 n 个正整数的数组和一个正整数 s ，找出该数组中满足其和 ≥ s 的长度最小的 连续 子数组，并返回其长度。如果不存在符合条件的子数组，返回 0。
>
> 示例：
>
> 输入：s = 7, nums = [2,3,1,2,4,3] 输出：2 解释：子数组 [4,3] 是该条件下的长度最小的子数组。
>
> 提示：
>
> - 1 <= target <= 10^9
> - 1 <= nums.length <= 10^5
> - 1 <= nums[i] <= 10^5

### 滑动窗口

时间复杂度：O(n)

空间复杂度：O(1)

![iShot_2023-05-09_15.32.16](https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_09_iShot_2023-05-09_15.32.16.gif)

```typescript
function minSubArrayLen(target: number, nums: number[]): number {
    let sum = 0;
    let ans = Infinity;
    let start = 0;
    let end = 0;
    while (end < nums.length) {
        sum += nums[end];
        while (sum >= target) {
            ans = Math.min(ans, end - start + 1);
            sum -= nums[start++];
        }
        end++;
    }
    return ans === Infinity ? 0 : ans;
};
```



## 59.螺旋矩阵Ⅱ

> 给定一个正整数 n，生成一个包含 1 到 n^2 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。
>
> <img src="https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg" alt="img" style="float: left"/>
>
> 示例:
>
> 输入: 3 输出: [ [ 1, 2, 3 ], [ 8, 9, 4 ], [ 7, 6, 5 ] ]

### 模拟法

时间复杂度：$O(n^2)$，其中几是给定的正整数。矩阵的大小是 $n * n$，需要填入矩阵中的每个元素。
空间复杂度：$0(1)$。除了返回的矩阵以外，空间复杂度是常数。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_12_ccff416fa39887c938d36fec8e490e1861813d3bba7836eda941426f13420759-Picture1.png" alt="ccff416fa39887c938d36fec8e490e1861813d3bba7836eda941426f13420759-Picture1" style="zoom:37%;" />

```typescript
function generateMatrix(n: number): number[][] {
    let mat: number[][] = Array.from(new Array(n)).map(() => Array.from(new Array(n)));
    let l = 0, r = n - 1, b = n - 1, t = 0;
    let num = 1, target = n * n;
    while(num <= target) {
        for (let i = l; i <= r; i++) mat[t][i] = num++;
        t++;
        for (let i = t; i <= b; i++) mat[i][r] = num++;
        r--;
        for (let i = r; i >= l; i--) mat[b][i] = num++;
        b--;
        for (let i = b; i >= t; i--) mat[i][l] = num++;
        l++;
    }
    return mat;
};
```



# 链表

## 203.移除链表元素

> 题意：删除链表中等于给定值 val 的所有节点。
>
> 示例 1： 输入：head = [1,2,6,3,4,5,6], val = 6 输出：[1,2,3,4,5]
>
> 示例 2： 输入：head = [], val = 1 输出：[]
>
> 示例 3： 输入：head = [7,7,7,7], val = 7 输出：[]

### 虚拟头节点

![iShot_2023-05-11_11.59.24](https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_11_iShot_2023-05-11_11.59.24.gif)

```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function removeElements(head: ListNode | null, val: number): ListNode | null {
    const dummyHead = new ListNode();
    dummyHead.next = head;
    let temp = dummyHead;
    while (temp.next) {
        if (temp.next.val === val) {
            temp.next = temp.next.next
        } else {
            temp = temp.next;
        }
    }
    return dummyHead.next;
};
```



## 707.设计链表

> 在链表类中实现这些功能：
>
> - get(index)：获取链表中第 index 个节点的值。如果索引无效，则返回-1。
> - addAtHead(val)：在链表的第一个元素之前添加一个值为 val 的节点。插入后，新节点将成为链表的第一个节点。
> - addAtTail(val)：将值为 val 的节点追加到链表的最后一个元素。
> - addAtIndex(index,val)：在链表中的第 index 个节点之前添加值为 val 的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 index 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。
> - deleteAtIndex(index)：如果索引 index 有效，则删除链表中的第 index 个节点。

### 虚拟头节点

时间复杂度：初始化O(1)，get消耗O(index)，addAtHead消耗O(1)，addAtTail消耗O(1)，addAtIndex消耗O(index)。

空间复杂度：所有函数单词调用的空间复杂度均为O(1)，总体空间复杂度O(n)，其中n为addAtHead,addAtTail和addAtIndex的调用次数之和。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_11_1663892191-cHQUiq-LeetCode707%E6%8F%92%E5%85%A5%E5%A4%B4%E7%BB%93%E7%82%B9.gif" alt="1663892191-cHQUiq-LeetCode707插入头结点" style="zoom:50%;" />

```typescript
class N {
    next: N;
    val: number;

    constructor(val?: number) {
        this.val = val;
    }
}

class MyLinkedList {
    dummyNode: N = new N(0);
    size = 0;

    constructor() {

    }

    get(index: number): number {
        if (index < 0 || index >= this.size) return -1;
        let temp = this.dummyNode;
        for (let i = 0; i <= index; i++) {
            temp = temp.next;
        }
        return temp.val;
    }

    addAtHead(val: number): void {
        this.addAtIndex(0, val);
    }

    addAtTail(val: number): void {
        this.addAtIndex(this.size, val);
    }

    addAtIndex(index: number, val: number): void {
        if (index > this.size) return;
        index = Math.max(0, index);
        this.size++;
        let pred = this.dummyNode;
        for (let i = 0; i < index; i++) {
            pred = pred.next;
        }
        const n = new N(val);
        n.next = pred.next;
        pred.next = n;
    }

    deleteAtIndex(index: number): void {
        if (index < 0 || index >= this.size) return;
        this.size--;
        let pred = this.dummyNode;
        for (let i = 0; i < index; i++) {
            pred = pred.next;
        }
        pred.next = pred.next.next;
    }
}

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * var obj = new MyLinkedList()
 * var param_1 = obj.get(index)
 * obj.addAtHead(val)
 * obj.addAtTail(val)
 * obj.addAtIndex(index,val)
 * obj.deleteAtIndex(index)
 */
```



## 206.反转链表

> 题意：反转一个单链表。
>
> <img src="https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg" alt="img" style="float: left"/>
>
> 示例: 输入: 1->2->3->4->5->NULL 输出: 5->4->3->2->1->NULL

### 双指针

时间复杂度：$O(n)$，其中n是链表的长度。需要遍历链表一次。

空间复杂度：$O(1)$。

![iShot_2023-05-12_17.05.49](https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_12_iShot_2023-05-12_17.05.49.gif)

```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function reverseList(head: ListNode | null): ListNode | null {
    let prev: ListNode = null;
    let cur: ListNode = head;
    while (cur) {
        const temp: ListNode = cur.next;
        cur.next = prev;
        prev = cur;
        cur = temp;
    }
    return prev;
};
```

### 递归

时间复杂度：$O(n)$，其中n是链表的长度。需要对链表的每个节点进行反转操作。
空间复杂度：$O(n)$，其中几是链表的长度。空间复杂度主要取决于递归调用的栈空间，最多为n层。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_12_8951bc3b8b7eb4da2a46063c1bb96932e7a69910c0a93d973bd8aa5517e59fc8.gif" alt="8951bc3b8b7eb4da2a46063c1bb96932e7a69910c0a93d973bd8aa5517e59fc8" style="zoom:67%;" />

```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function reverseList(head: ListNode | null): ListNode | null {
    if (!head || !head.next) return head;
    const ret = reverseList(head.next);
    head.next.next = head;
    head.next = null;
    return ret;
};
```



## 24.两两交换链表中的节点

> 给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。
>
> 你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_15_swap_ex1.jpg" alt="img" style="float: left;"/>
>
> ```
> 输入：head = [1,2,3,4]
> 输出：[2,1,4,3]
> 
> 输入：head = []
> 输出：[]
> 
> 输入：head = [1]
> 输出：[1]
> ```

### 迭代

- 时间复杂度：$O(n)$，其中 n是链表的节点数量。需要对每个节点进行更新指针的操作。
- 空间复杂度：$O(1)$。

![iShot_2023-05-15_10.03.01](https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_15_iShot_2023-05-15_10.03.01.gif)

```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function swapPairs(head: ListNode | null): ListNode | null {
    if (!head || !head.next) return head;
    const dummyNode = new ListNode();
    dummyNode.next = head;
    let temp = dummyNode;
    while (temp.next && temp.next.next) {
        let node1 = temp.next;
        let node2 = temp.next.next;
        temp.next = node2;
        node1.next = node2.next;
        node2.next = node1;
        temp = node1;
    }
    return dummyNode.next;
};
```

### 递归

- 时间复杂度：$O(n)$，其中n是链表的节点数量。需要对每个节点进行更新指针的操作。
- 空间复杂度：$O(n)$，其中n是链表的节点数量。空间复杂度主要取决于递归调用的栈空间。

![iShot_2023-05-15_10.19.47](https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_15_iShot_2023-05-15_10.19.47.gif)

```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function swapPairs(head: ListNode | null): ListNode | null {
    if (head === null || head.next === null) return head;
    const newHead = head.next;
    head.next = swapPairs(newHead.next);
    newHead.next = head;
    return newHead;
};
```





## 19.删除链表的倒数第N个结点

> 给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_15_remove_ex1.jpg" alt="img" style="float: left;"/>
>
> ```
> 输入：head = [1,2,3,4,5], n = 2
> 输出：[1,2,3,5]
> 
> 输入：head = [1], n = 1
> 输出：[]
> 
> 输入：head = [1,2], n = 1
> 输出：[1]
> ```

### 栈

- 时间复杂度：$O(L)$，其中 $L$ 是链表的长度。
- 空间复杂度：$O(L)$，其中 $L$ 是链表的长度。主要为栈的开销。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_15_iShot_2023-05-15_11.03.27.gif" alt="iShot_2023-05-15_11.03.27" style="zoom:67%;" />

```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function removeNthFromEnd(head: ListNode | null, n: number): ListNode | null {
    if (!head) return head;
    const dummyNode = new ListNode(0);
    dummyNode.next = head;
    const stack: ListNode[] = [];
    let cur = dummyNode;
    let prev: ListNode = null;
    while (cur.next) {
        stack.unshift(cur);
        cur = cur.next;
    }
    while (n > 0) {
        n--;
        prev = stack.shift();
    }
    prev.next = prev.next.next;
    return dummyNode.next;
};
```

### 双指针

- 时间复杂度：$O(L)$，其中 $L$ 是链表的长度。
- 空间复杂度：$O(1)$。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_15_p3.png" alt="p3" style="zoom: 43%;" />

```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function removeNthFromEnd(head: ListNode | null, n: number): ListNode | null {
    if (!head) return head;
    const dummyNode = new ListNode(0);
    dummyNode.next = head;
    let first: ListNode = head;
    let second: ListNode = dummyNode;
    for (let i = 0; i < n; i++) {
        first = first.next;
    }
    while(first) {
        first = first.next;
        second = second.next;
    }
    second.next = second.next.next;
    return dummyNode.next;
};
```



## 160.链表相交

> 给你两个单链表的头节点 headA 和 headB ，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回 null 。
>
> 图示两个链表在节点 c1 开始相交：
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_15_160_statement.png" alt="img" style="float: left;"/>
>
> 题目数据 保证 整个链式结构中不存在环。
>
> 注意，函数返回结果后，链表必须 保持其原始结构 。

### 双指针

- 时间复杂度：$O(m+n)$，其中 $m$ 和 $n$ 是分别是链表 $headA$ 和 $headB$ 的长度。两个指针同时遍历两个链表，每个指针遍历两个链表各一次。
- 空间复杂度：$O(1)$。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_15_iShot_2023-05-15_11.51.45.gif" alt="iShot_2023-05-15_11.51.45" style="zoom:80%;" />

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) return null;
        ListNode pA = headA;
        ListNode pB = headB;
        while (pA != pB) {
            pA = pA == null ? headB : pA.next;
            pB = pB == null ? headA : pB.next;
        }
        return pA;
    }
}
```



## 142.环形链表Ⅱ

> 题意： 给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。
>
> 为了表示给定链表中的环，使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。
>
> **说明**：不允许修改给定的链表。
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_16_image-20230516101038026.png" alt="image-20230516101038026" style="zoom:33%;float:left;" />
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_16_image-20230516101130412.png" alt="image-20230516101130412" style="zoom:33%;float:left;" />

### 哈希表

思路：遍历链表中的每个节点，并将它记录下来；一旦遇到了此前遍历过的节点，就可以判定链表中存在环。

- 时间复杂度：$O(N)$，其中 $N$ 为链表中节点的数目。我们恰好需要访问链表中的每一个节点。
- 空间复杂度：$O(N)$，其中 $N$ 为链表中节点的数目。我们需要将链表中的每个节点都保存在哈希表当中。

```
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function detectCycle(head: ListNode | null): ListNode | null {
    if (!head) return head;
    const set = new Set();
    let temp = head;
    while (temp) {
        if (set.has(temp)) {
            return temp;
        }
        set.add(temp);
        temp = temp.next;
    }
    return null;
};
```

### 快慢双指针

- 时间复杂度：$O(N)$，其中 $N$ 为链表中节点的数目。在最初判断快慢指针是否相遇时，$slow$ 指针走过的距离不会超过链表的总长度；随后寻找入环点时，走过的距离也不会超过链表的总长度。因此，总的执行时间为 $O(N)+O(N) =O(N)$。
- 空间复杂度：$O(1)$。我们只使用了 $slou,fast$ 两个指针。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_16_iShot_2023-05-16_10.15.12.gif" alt="iShot_2023-05-16_10.15.12" style="zoom:80%;" />

```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function detectCycle(head: ListNode | null): ListNode | null {
    if (!head) return null;
    let slow = head, fast = head;
    while (true) {
        if (!fast || !fast.next) return null;
        slow = slow.next;
        fast = fast.next.next;
        if (slow === fast) break;
    }
    fast = head;
    while (slow !== fast) {
        slow = slow.next;
        fast = fast.next;
    }
    return fast;
};
```



# 哈希表

## 242.有效的字母异位词

> 给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。
>
> **注意：**若 `s` 和 `t` 中每个字符出现的次数都相同，则称 `s` 和 `t` 互为字母异位词。
>
> 示例 1: 输入: s = "anagram", t = "nagaram" 输出: true
>
> 示例 2: 输入: s = "rat", t = "car" 输出: false
>
> **说明:** 你可以假设字符串只包含小写字母。

### 哈希表

时间复杂度：O(n)，其中n为s的长度

空间复杂度：O(S)，其中S为字符集大小

![iShot_2023-05-11_16.14.42](https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_11_iShot_2023-05-11_16.14.42.gif)

```typescript
function isAnagram(s: string, t: string): boolean {
    if (s.length !== t.length) return false;
    const map = new Map<string, number>();
    for (let i = 0; i < s.length; i++) {
        map.set(s[i], (map.get(s[i]) || 0) + 1);
    }
    for (let i = 0; i < t.length; i++) {
        map.set(t[i], (map.get(t[i]) || 0) - 1);
        if (map.get(t[i]) < 0) return false;
    }
    return true
};
```



## 1002.查找共用字符

> 给你一个字符串数组 words ，请你找出所有在 words 的每个字符串中都出现的共用字符（ 包括重复字符），并以数组形式返回。你可以按 任意顺序 返回答案。
>
> 示例 1：
>
> 输入：words = ["bella","label","roller"] 输出：["e","l","l"] 示例 2：
>
> 输入：words = ["cool","lock","cook"] 输出：["c","o"]
>
> 提示：
>
> 1 <= words.length <= 100 1 <= words[i].length <= 100 words[i] 由小写英文字母组成

### 哈希表

- 时间复杂度：$O(n(m+|∑|)$，其中 $n$ 是数组 A 的长度（即字符串的数目），$m$ 是字符串的平均长度，$∑$ 为字符集，在本题中字符集为所有小写字母，$∑$=26。
- 空间复杂度：$O(|∑|)$。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_16_1632105856-qqFVxc-image.png" alt="1002.查找常用字符.png" style="zoom:33%;" />

```java
class Solution {
    public List<String> commonChars(String[] words) {
        List<String> result = new ArrayList<String>();
        if (words.length == 0) return result;
        int[] hash = new int[26];
        for (int i = 0; i < words[0].length(); i++) {
            hash[words[0].charAt(i) - 'a']++;
        }
        for (int i = 1; i < words.length; i++) {
            int[] hashOtherStr = new int[26];
            for (int j = 0; j < words[i].length(); j++) {
                hashOtherStr[words[i].charAt(j) - 'a']++;
            }
            for (int k = 0; k < 26; k++) {
                hash[k] = Math.min(hash[k], hashOtherStr[k]);
            }
        }

        for (int i = 0; i < 26; i++) {
            while (hash[i] != 0) {
                char c = (char) (i + 'a');
                result.add(String.valueOf(c));
                hash[i]--;
            }
        }
        return result;
    }
}
```



## 349.两个数组的交集

> 给定两个数组 `nums1` 和 `nums2` ，返回 *它们的交集* 。输出结果中的每个元素一定是 **唯一** 的。我们可以 **不考虑输出结果的顺序** 。
>
> 示例 1：
>
> ```
> 输入：nums1 = [1,2,2,1], nums2 = [2,2]
> 输出：[2]
> ```
>
> 示例 2：
>
> ```
> 输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
> 输出：[9,4]
> 解释：[4,9] 也是可通过的
> ```

### 两个集合

使用两个集合分别存储两个数组中的元素，然后遍历较小的集合，判断其中的每个元素是否在另一个集合中，如果元素也在另一个集合中，则将该元素添加到返回值。

- 时间复杂度：$O(m+n)$，其中 $m$ 和 $n$ 分别是两个数组的长度。使用两个集合分别存储两个数组中的元素需要 $O(m+n)$ 的时间，遍历较小的集合并判断元素是否在另一个集合中需要 $O(min(m,n))$ 的时间，因此总时间复杂度是 $O(m+n)$。
- 空间复杂度：$O(m+n)$，其中 $m$ 和 $n$ 分别是两个数组的长度。空间复杂度主要取决于两个集合。

```typescript
function intersection(nums1: number[], nums2: number[]): number[] {
    let set1 = new Set(nums1);
    let set2 = new Set(nums2);
    const res = new Set<number>();

    if (set1.size > set2.size) {
        [set1, set2] = [set2, set1];
    }

    for (let num of set1) {
        if (set2.has(num)) {
            res.add(num);
        }
    }

    return [...res];;
};
```

### 排序+双指针

思路：数组排序，然后用两个指针分别遍历数组，如果两个指针指向的元素相等就是其中一个交集，否则比较两个指针指向的元素的大小，较小的向前移动。

- 时间复杂度：$O(mlogm+n logn)$，其中m和n分别是两个数组的长度。对两个数组排序的时间复杂度分别是 $O(mlog m)$ 和 $O(nlogn)$，双指针寻找交集元素的时间复杂度是 $O(m+n)$，因此总时间复杂度是 $O(mlog m + nlog n)$。
- 空间复杂度：$O(logm + logn)$，其中 $m$ 和 $n$ 分别是两个数组的长度。空间复杂度主要取决于排序使用的额外空间。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_17_iShot_2023-05-17_14.51.41.gif" alt="iShot_2023-05-17_14.51.41" style="zoom:80%;" />

```typescript
function intersection(nums1: number[], nums2: number[]): number[] {
    nums1.sort((x, y) => x - y);
    nums2.sort((x, y) => x - y);
    let index1 = 0;
    let index2 = 0;
    const intersection = new Set<number>();
    while (index1 < nums1.length && index2 < nums2.length) {
        if (nums1[index1] === nums2[index2]) {
            intersection.add(nums1[index1]);
            index1++;
            index2++;
        } else if (nums1[index1] > nums2[index2]) {
            index2++;
        } else {
            index1++;
        }
    }
    return [...intersection];
};
```



## 202.快乐数

### 哈希表

思路：通过持续计算数字的平方和并将结果添加到集合中，如果最终得到1（快乐数），则结束；如果产生的数字已经在集合中（表示陷入循环且循环中没有1），则可以确定该数不是快乐数。

- 时间复杂度：$O(log n)$。
- 空间复杂度：$O(log n)$。

```typescript
function getNext(n: number) {
    let totalSum = 0;
    while (n > 0) {
        let d = n % 10;
        n = Math.floor(n / 10);
        totalSum += d * d;
    }
    return totalSum;
}

function isHappy(n: number): boolean {
    const set = new Set<Number>();
    let sum = n;
    while (sum !== 1) {
        let newSum = getNext(sum);
        if (set.has(newSum)) return false;
        set.add(newSum);
        sum = newSum;
    }
    return true;
};
```

### 【推荐】快慢指针

思路：通过快慢两个指针（一个一次计算一步，另一个一次计算两步）遍历数字的平方和序列，如果这个序列能够到达1（快乐数），则快指针将首先到达1；如果序列陷入循环且循环中没有1，那么快慢指针最终将相遇，此时可以确定该数不是快乐数。

- 时间复杂度：$O(log n)$。
- 空间复杂度：$O(1)$。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_17_iShot_2023-05-17_17.23.16.gif" alt="iShot_2023-05-17_17.23.16" style="zoom:80%;" />

```typescript
function getNext(n: number) {
    let totalSum = 0;
    while (n > 0) {
        let d = n % 10;
        n = Math.floor(n / 10);
        totalSum += d * d;
    }
    return totalSum;
}

function isHappy(n: number): boolean {
    let slow = n;
    let fast = getNext(n);
    while (fast !== 1) {
        if (slow === fast) return false;
        slow = getNext(slow);
        fast = getNext(getNext(fast));
    }
    return true;
};
```



## 1.两数之和

> 给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。
>
> 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。
>
> **示例:**
>
> 给定 nums = [2, 7, 11, 15], target = 9
>
> 因为 nums[0] + nums[1] = 2 + 7 = 9
>
> 所以返回 [0, 1]

### 哈希表

- 时间复杂度：$O(N)$，其中 $N$ 是数组中的元素数量。对于每一个元素 `x`，我们可以 $O(1)$ 地寻找 `target - x`。
- 空间复杂度：$O(N)$，其中 $N$ 是数组中的元素数量。主要为哈希表的开销。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_18_iShot_2023-05-18_09.43.57.gif" alt="iShot_2023-05-18_09.43.57" style="zoom:80%;" />

```typescript
function twoSum(nums: number[], target: number): number[] {
    const map = new Map<number, number>();
    for (let i = 0; i < nums.length; i++) {
        const index = map.get(target - nums[i])
        if (index !== undefined) {
            return [index, i];
        }
        map.set(nums[i], i);
    }
    return [];
};
```



## 454.四数相加Ⅱ

### 哈希表

> 给定四个包含整数的数组列表 A , B , C , D ,计算有多少个元组 (i, j, k, l) ，使得 A[i] + B[j] + C[k] + D[l] = 0。
>
> 为了使问题简单化，所有的 A, B, C, D 具有相同的长度 N，且 0 ≤ N ≤ 500 。所有整数的范围在 -2^28 到 2^28 - 1 之间，最终结果不会超过 2^31 - 1 。
>
> 例如:
>
> 输入:
>
> - A = [ 1, 2]
> - B = [-2,-1]
> - C = [-1, 2]
> - D = [ 0, 2]
>
> 输出: 2
>
> 解释:
>
> 两个元组如下:
>
> 1. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
> 2. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0

1. 先计算列表A和B中所有可能的两数之和，并在一个哈希表中记录每种两数之和出现的次数。对于每一对(A[i], B[j])，将A[i] + B[j]加入到哈希表，并更新哈希表中对应的计数。
2. 然后，对于列表C和D中的每一对(C[k], D[l])，计算-(C[k] + D[l])，看它是否在哈希表中。如果在，那么就找到了一种组合，使得A[i] + B[j] + C[k] + D[l]等于0。
3. 将哈希表中与-(C[k] + D[l])相对应的值加到结果中，因为这个值表示存在多少种可能的(A[i], B[j])组合，使得A[i] + B[j]的和等于-(C[k] + D[l])，也就是说，存在多少种可能的四元组使得他们的和等于0。

这个方法将原问题从四个列表的四重循环简化为了两个两重循环，大大减少了计算的复杂性。使用哈希表记录两数之和的频率，也提高了查找的效率。这种方法的时间复杂度是$O(n^2)$，空间复杂度也是$O(n^2)$，其中n是列表A, B, C, D的长度。

```typescript
function fourSumCount(nums1: number[], nums2: number[], nums3: number[], nums4: number[]): number {
    const map = new Map<number, number>();

    for (let num1 of nums1) {
        for (let num2 of nums2) {
            const sum = num1 + num2
            map.set(sum, map.has(sum) ? map.get(sum) + 1 : 1);
        }
    }

    let ans = 0
    for (let num3 of nums3) {
        for (let num4 of nums4) {
            if (map.get(-num3 - num4) !== undefined) {
                ans += map.get(-num3 - num4);
            }
        }
    }

    return ans
};
```



## 383.赎金信

### 字符统计

> 给定一个赎金信 (ransom) 字符串和一个杂志(magazine)字符串，判断第一个字符串 ransom 能不能由第二个字符串 magazines 里面的字符构成。如果可以构成，返回 true ；否则返回 false。
>
> (题目说明：为了不暴露赎金信字迹，要从杂志上搜索各个需要的字母，组成单词来表达意思。杂志字符串中的每个字符只能在赎金信字符串中使用一次。)
>
> **注意：**
>
> 你可以假设两个字符串均只含有小写字母。
>
> canConstruct("a", "b") -> false
> canConstruct("aa", "ab") -> false
> canConstruct("aa", "aab") -> true

- 时间复杂度：$O(m+n)$，只需遍历两个字符一次即可。
- 空间复杂度：$O(S)$，$S$ 是字符集，这道题中 $S$ 为全部小写英语字母，因此 $S=26$。

```typescript
function canConstruct(ransomNote: string, magazine: string): boolean {
    if (ransomNote.length > magazine.length) return false;
    const arr = Array.from(new Array(26), () => 0);
    for (let s of magazine) {
        const index = s.charCodeAt(0) - 'a'.charCodeAt(0);
        arr[index]++;
    }
    for (let s of ransomNote) {
        const index = s.charCodeAt(0) - 'a'.charCodeAt(0);
        if (arr[index] - 1 < 0) {
            return false
        }
        arr[index]--;
    }
    return true;
};
```



## 15.三数之和

> 给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有满足条件且不重复的三元组。
>
> **注意：** 答案中不可以包含重复的三元组。
>
> 示例：
>
> 给定数组 nums = [-1, 0, 1, 2, -1, -4]，
>
> 满足要求的三元组集合为： [ [-1, 0, 1], [-1, -1, 2] ]
>
> **示例1**
>
> ```
> 输入：nums = [-1,0,1,2,-1,-4]
> 输出：[[-1,-1,2],[-1,0,1]]
> 解释：
> nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0 。
> nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0 。
> nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0 。
> 不同的三元组是 [-1,0,1] 和 [-1,-1,2] 。
> 注意，输出的顺序和三元组的顺序并不重要。
> ```
>
> **示例2**
>
> ```
> 输入：nums = [0,1,1]
> 输出：[]
> 解释：唯一可能的三元组和不为 0 。
> ```
>
> **示例3**
>
> ```
> 输入：nums = [0,0,0]
> 输出：[[0,0,0]]
> 解释：唯一可能的三元组和为 0 。
> ```

### 排序+双指针

- 时间复杂度：$O(N^2)$，其中 $N$ 是数组的长度。
- 空间复杂度：$O(log N)$

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_21_iShot_2023-05-21_16.44.47.gif" alt="iShot_2023-05-21_16.44.47" style="zoom:80%;" />

```typescript
function threeSum(nums: number[]): number[][] {
    if (nums.length < 3) return [];
    nums.sort((a, b) => a - b);
    const ans: number[][] = [];
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] > 0) break;;
        if (i > 0 && nums[i] === nums[i - 1]) continue;
        let L = i + 1;
        let R = nums.length - 1;
        while (L < R) {
            const sum = nums[i] + nums[L] + nums[R];
            if (sum < 0) {
                L++;
            } else if (sum > 0) {
                R--;
            } else {
                while (nums[L] === nums[L + 1]) L++; // 去重
                while (nums[R] === nums[R - 1]) R--; // 去重
                ans.push([nums[i], nums[L], nums[R]]);
                L++;
                R--;
            }
        }
    }
    return ans;
};
```



## 18.四数之和

> 题意：给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，使得 a + b + c + d 的值与 target 相等？找出所有满足条件且不重复的四元组。
>
> **注意：**
>
> 答案中不可以包含重复的四元组。
>
> 示例： 给定数组 nums = [1, 0, -1, 0, -2, 2]，和 target = 0。 满足要求的四元组集合为： [ [-1, 0, 0, 1], [-2, -1, 1, 2], [-2, 0, 0, 2] ]

### 排序+双指针

- 时间复杂度：$O(n^3)$，其中 $n$ 是数组的长度。排序的时间复杂度是 $O(nlog n)$，枚举四元组的时间复杂度是 $O(n^3)$，因此总时间复杂度为 $O(n^3 + nlog n) = O(n^3)$。
- 空间复杂度：$O(logn)$，其中 $n$ 是数组的长度。空间复杂度主要取决于排序额外使用的空间。此外排序修改了输入数组 $nums$，实际情况中不一定允许，因此也可以看成使用了一个额外的数组存储了数组 $nums$ 的副本并排序，空间复杂度为 $O(n)$。

和三数之和解法一样。

```typescript
function fourSum(nums: number[], target: number): number[][] {
    const quadruplets: number[][] = [];
    if (nums.length < 4) {
        return quadruplets;
    }
    nums.sort((x, y) => x - y);
    const length = nums.length;
    for (let i = 0; i < length - 3; i++) {
        if (i > 0 && nums[i] === nums[i - 1]) {
            continue;
        }
      	// 最小值大于target，退出循环
        if (nums[i] + nums[i + 1] + nums[i + 2] + nums[i + 3] > target) {
            break;
        }
        // 最大值小于target，跳过当前循环
        if (nums[i] + nums[length - 3] + nums[length - 2] + nums[length - 1] < target) {
            continue;
        }
        for (let j = i + 1; j < length - 2; j++) {
            if (j > i + 1 && nums[j] === nums[j - 1]) {
                continue;
            }
          	// 最小值大于target，退出循环
            if (nums[i] + nums[j] + nums[j + 1] + nums[j + 2] > target) {
                break;
            }
	          // 最大值小于target，跳过当前循环
            if (nums[i] + nums[j] + nums[length - 2] + nums[length - 1] < target) {
                continue;
            }
            let left = j + 1, right = length - 1;
            while (left < right) {
                const sum = nums[i] + nums[j] + nums[left] + nums[right];
                if (sum === target) {
                    quadruplets.push([nums[i], nums[j], nums[left], nums[right]]);
                    while (left < right && nums[left] === nums[left + 1]) {
                        left++;
                    }
                    left++;
                    while (left < right && nums[right] === nums[right - 1]) {
                        right--;
                    }
                    right--;
                } else if (sum < target) {
                    left++;
                } else {
                    right--;
                }
            }
        }
    }
    return quadruplets;
};
```



# 字符串



## 344.反转字符串

> 编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 char[] 的形式给出。
>
> 不要给另外的数组分配额外的空间，你必须原地修改输入数组、使用 O(1) 的额外空间解决这一问题。
>
> 你可以假设数组中的所有字符都是 ASCII 码表中的可打印字符。
>
> 示例 1：
> 输入：["h","e","l","l","o"]
> 输出：["o","l","l","e","h"]
>
> 示例 2：
> 输入：["H","a","n","n","a","h"]
> 输出：["h","a","n","n","a","H"]

### 双指针

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_22_344_fig1.png" alt="fig1" style="zoom: 33%;" />

- 时间复杂度：$O(N)$，其中 $N$ 为字符数组的长度。一共执行了 $N/2$ 的交换。
- 空间复杂度：$O(1)$。 只使用了常数空间来存放若干变量。

```typescript
/**
 Do not return anything, modify s in-place instead.
 */
function reverseString(s: string[]): void {
    let L = 0
    let R = s.length - 1;
    while (L < R) {
        const temp = s[L];
        s[L] = s[R];
        s[R] = temp;
        L++;
        R--;
    }
};
```



## 541.反转字符串Ⅱ

> 给定一个字符串 s 和一个整数 k，从字符串开头算起, 每计数至 2k 个字符，就反转这 2k 个字符中的前 k 个字符。
>
> 如果剩余字符少于 k 个，则将剩余字符全部反转。
>
> 如果剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符，其余字符保持原样。
>
> 示例:
>
> 输入: s = "abcdefg", k = 2
> 输出: "bacdfeg"

### 模拟

- 时间复杂度：$O(n)$，其中n是字符串 $s$ 的长度。
- 空间复杂度：$O(1$）或 $O(n)$，取决于使用的语言中字符串类型的性质。如果字符串是可修改的，那么我们可以直接在原字符串上修改，空间复杂度为 $O(1)$，否则需要使用 $O(n)$ 的空间将字符串临时转换为可以修改的数据结构（例如数组），空间复杂度为 $O(n)$。

反转每个下标从 $2k$ 的倍数开始的，长度为 $k$ 的子串。若该子串长度不足 $k$，则反转整个子串。

```typescript
function reverse(arr: string[], left: number, right: number) {
    while (left < right) {
        [arr[left], arr[right]] = [arr[right], arr[left]];
        left++;
        right--;
    }
}

function reverseStr(s: string, k: number): string {
    const arr = s.split('');
    for (let i = 0; i < arr.length; i += 2 * k) {
        reverse(arr, i, Math.min(i + k, arr.length) - 1);
    }
    return arr.join('');
};
```



## 05.替换空格

> 请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。
>
> **示例 1：**
>
> ```
> 输入：s = "We are happy."
> 输出："We%20are%20happy."
> ```

### 字符数组

- 时间复杂度：$O(N)$
- 空间复杂度：$O(N)$

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_23_iShot_2023-05-23_09.54.38.gif" alt="iShot_2023-05-23_09.54.38" />

```typescript
function replaceSpace(s: string): string {
    let arr = [];
    for (let i of s) {
        if (i === " ") {
            arr.push("%20");
        } else {
            arr.push(i);
        }
    }
    return arr.join("");
};
```



## 151.反转字符串中的单词

> 给定一个字符串，逐个翻转字符串中的每个单词。
>
> 示例 1：
>
> ```
> 输入: "the sky is blue"
> 输出: "blue is sky the"
> ```
>
> 示例 2：
>
> ```
> 输入: "  hello world!  "
> 输出: "world! hello"
> 解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
> ```
>
> 示例 3：
>
> ```
> 输入: "a good  example"
> 输出: "example good a"
> 解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
> ```
>
> 

### 语言特性

思路：很多语言对字符串提供了 split（拆分），reverse（翻转）和 join（连接）等方法，因此我们可以简单的调用内置的 API 完成操作：

- 使用 split 将字符串按空格分割成字符串数组；

- 使用 reverse 将字符串数组进行反转；
- 使用 join 方法将字符串数组拼成一个字符串。

复杂度分析：

- 时间复杂度：$O(n)$，其中 $n$ 为输入字符串的长度。
- 空间复杂度：$O(n)$，用来存储字符串分割之后的结果。

```typescript
function reverseWords(s: string): string {
    return s.trim().split(/\s+/).reverse().join(" ");
};
```

### 双端队列

- 时间复杂度：$O(n)$，其中 $n$ 为输入字符串的长度。
- 空间复杂度：$O(n)$，双端队列存储单词需要 $O(n)$ 的空间。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_23_deque2.png" alt="fig" style="zoom: 33%;" />

```typescript
function reverseWords(s: string): string {
    let left = 0;
    let right = s.length - 1;
    let queue: string[] = [];
    let temp: string[] = [];
    while (left <= right && s[left] === " ") left++;
    while (left <= right && s[right] === " ") right--;

    while (left <= right) {
        if (s[left] !== " ") {
            temp.push(s[left]);
        } else if (s[left] === " " && temp.length !== 0) {
            queue.unshift(temp.join(""));
            temp = [];
        }
        left++;
    }

    queue.unshift(temp.join(""));
    return queue.join(" ");
};
```



## 剑指 Offer 58 - II. 左旋转字符串

> 字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。
>
> **示例 1：**
>
> ```
> 输入: s = "abcdefg", k = 2
> 输出: "cdefgab"
> ```
>
> **示例 2：**
>
> ```
> 输入: s = "lrloseumgh", k = 6
> 输出: "umghlrlose"
> ```

### 字符串切片

- 时间复杂度：$O(N)$，$N$ 为字符串s的长度。
- 空间复杂度：$O(N)$，两个字符串切片的总长度为 $N$。

```typescript
function reverseLeftWords(s: string, n: number): string {
    return s.slice(n) + s.slice(0, n)
};
```

### 列表遍历拼接

- 时间复杂度：$O(N)$，线性遍历 $s$ 并添加。
- 空间复杂度：$O(N)$，新建的辅助 $arr$ 使用 $O(N)$ 大小的额外空间。

```typescript
function reverseLeftWords(s: string, n: number): string {
    const arr: string[] = [];
    for (let i = n; i < s.length; i++) {
        arr.push(s[i]);
    }
    for (let i = 0; i < n; i++) {
        arr.push(s[i]);
    }
    return arr.join("");
};
```



## 28.找出字符串中第一个匹配项的下标

> xxx

### 暴力匹配

我们可以让字符串 *needle* 与字符串 *haystack* 的所有长度为 $m$ 的子串均匹配一次。

为了减少不必要的匹配，我们每次匹配失败即立刻停止当前子串的匹配，对下一个子串继续匹配。如果当前子串匹配成功，我们返回当前子串的开始位置即可。如果所有子串都匹配失败，则返回 *-1*。

- 时间复杂度：$O(m*n)$。
- 空间复杂度：$O(1)$。

```typescript
function strStr(haystack: string, needle: string): number {
    for (let i = 0; i < haystack.length; i++) {
        let a = i;
        let b = 0;
        if (haystack[i] === needle[b]) {
            while (b < needle.length && haystack[a] === needle[b]) {
                a++;
                b++;
            }
            if (b === needle.length) {
                return i;
            }
        }
    }
    return -1;
};
```

### KMP

> KMP算法是一种改进的字符串匹配算法，避免了朴素算法中不必要的字符比较，提高了匹配效率。它的主要思想是当出现字符比较不匹配时，可以记录一部分之前已经匹配的文本内容，利用这些信息使得下一步的搜索更加快捷。

- 时间复杂度：$O(m+n)$。
- 空间复杂度：$O(m)$，其中 $m$ 是字符串 *needle* 的长度。

思路：

1. 首先，函数检查needle的长度。如果needle的长度为0，那么函数就立即返回0（因为空字符串在任何位置都能被找到）。
2. 然后，函数初始化next数组，并且开始填充它。这个过程就是在计算needle中**每个位置的前缀和后缀的最长公共长度**。
3. 接下来，函数开始在haystack中查找needle。它从haystack的第一个字符开始，同时也从needle的第一个字符开始。每当找到一个匹配的字符，就将needle的当前位置向前移动一位（即j++）。如果在某个位置找不到匹配的字符，就回溯到needle的某个较早位置（即设置j为next[j - 1]），然后再从那里开始比较。这就是利用next数组进行快速跳跃的关键步骤。
4. 如果在某个位置找到了整个needle（即j等于needle的长度），那么函数就返回这个位置（即返回i - m + 1，其中m是needle的长度）。
5. 如果遍历了整个haystack都没有找到needle，那么函数就返回-1。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_25_1599638458-sHaHqX-KMP%E7%B2%BE%E8%AE%B23.gif" alt="KMP精讲3.gif" />

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_24_1599638354-SppDsh-KMP%E7%B2%BE%E8%AE%B22.gif" alt="KMP精讲2.gif" />

```typescript
function strStr(haystack: string, needle: string): number {
    let n = haystack.length, m = needle.length;
    if (m === 0) return 0;
    let next = new Array(m).fill(0);
    // 构建前缀表
    for (let i = 1, j = 0; i < m; i++) {
        while (j > 0 && needle[i] !== needle[j]) {
            j = next[j - 1];
        }
        if (needle[i] === needle[j]) {
            j++;
        }
        next[i] = j;
    }
    for (let i = 0, j = 0; i < n; i++) {
        while (j > 0 && haystack[i] !== needle[j]) {
            j = next[j - 1];
        }
        if (haystack[i] === needle[j]) {
            j++;
        }
        if (j === m) {
            return i - m + 1;
        }
    }
    return -1;
};
```



## 459.重复的子字符串

> 给定一个非空的字符串，判断它是否可以由它的一个子串重复多次构成。给定的字符串只含有小写英文字母，并且长度不超过10000。
>
> 示例 1:
> 输入: "abab"
> 输出: True
> 解释: 可由子字符串 "ab" 重复两次构成。
>
> 示例 2:
> 输入: "aba"
> 输出: False
>
> 示例 3:
> 输入: "abcabcabcabc"
> 输出: True
> 解释: 可由子字符串 "abc" 重复四次构成。 (或者子字符串 "abcabc" 重复两次构成。)

### 双倍长度字符串

思路：

1. 将原始字符串 `s` 复制并连接到自身，形成 `s + s`，其长度为原始字符串的两倍。
2. 移除新字符串的第一个和最后一个字符，也就是执行 `.slice(1, -1)` 操作。
3. 在这个新生成的字符串中搜索原始字符串 `s`。如果找到了（即 `indexOf(s)` 的结果不为 `-1`），那么原始字符串 `s` 包含重复的子字符串。如果没有找到，那么 `s` 不存在重复的子字符串。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_25_1659015254-yaMcUI-image.png" alt="image.png" style="zoom:50%;" />

```typescript
function repeatedSubstringPattern(s: string): boolean {
    return (s+s).slice(1, -1).indexOf(s) !== -1;
};
```

### KMP

方法一中使用了语言自带的查找函数`indexOf`。同样我们也可以自己实现这个函数，例如使用比较经典的KMP算法。

```typescript
// KMP算法
function kmp(str: string, substr: string) {
    let n = str.length, m = substr.length;
    let next: number[] = new Array(m).fill(0);
    for (let i = 1, j = 0; i < m; i++) {
        while (j > 0 && substr[i] !== substr[j]) {
            j = next[j - 1];
        }
        if (substr[i] === substr[j]) {
            j++;
        }
        next[i] = j;
    }
    for (let i = 0, j = 0; i < n; i++) {
        while (j > 0 && str[i] !== substr[j]) {
            j = next[j - 1];
        }
        if (str[i] === substr[j]) {
            j++;
        }
        if (j === m) {
            return i - m + 1;
        }
    }
    return -1;
}

function repeatedSubstringPattern(s: string): boolean {
    return kmp((s+s).slice(1, -1), s) !== -1;
};
```

# 栈与队列



## 232.用栈实现队列

> 使用栈实现队列的下列操作：
>
> `push(x)` -- 将一个元素放入队列的尾部。
> `pop()` -- 从队列首部移除元素。
> `peek()` -- 返回队列首部的元素。
> `empty()` -- 返回队列是否为空。
>
> 示例:
>
> ```
> MyQueue queue = new MyQueue();
> queue.push(1);
> queue.push(2);
> queue.peek();  // 返回 1
> queue.pop();   // 返回 1
> queue.empty(); // 返回 false
> ```
>
> 说明:
>
> - 你只能使用标准的栈操作 -- 也就是只有 push to top, peek/pop from top, size, 和 is empty 操作是合法的。
> - 你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可。
> - 假设所有操作都是有效的 （例如，一个空的队列不会调用 pop 或者 peek 操作）。

### 双栈

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_26_iShot_2023-05-26_10.00.57.gif" alt="iShot_2023-05-26_10.00.57" />



```typescript
class MyQueue {
    inStack: number[] = [];
    outStack: number[] = [];

    push(x: number): void {
        this.inStack.push(x);
    }

    provide() {
        if (this.outStack.length === 0) {
            while (this.inStack.length !== 0) {
                this.outStack.push(this.inStack.pop())
            }
        }
    }

    pop(): number {
        this.provide();
        return this.outStack.pop();
    }

    peek(): number {
        this.provide();
        return this.outStack[this.outStack.length - 1];
    }

    empty(): boolean {
        return this.inStack.length === 0 && this.outStack.length === 0;
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * var obj = new MyQueue()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.peek()
 * var param_4 = obj.empty()
 */
```



## 225.用队列实现栈

> 使用队列实现栈的下列操作：
>
> - push(x) -- 元素 x 入栈
> - pop() -- 移除栈顶元素
> - top() -- 获取栈顶元素
> - empty() -- 返回栈是否为空
>
> 注意:
>
> - 你只能使用队列的基本操作-- 也就是 push to back, peek/pop from front, size, 和 is empty 这些操作是合法的。
> - 你所使用的语言也许不支持队列。 你可以使用 list 或者 deque（双端队列）来模拟一个队列 , 只要是标准的队列操作即可。
> - 你可以假设所有操作都是有效的（例如, 对一个空的栈不会调用 pop 或者 top 操作）。

### 两个队列

- 时间复杂度：入栈操作 $O(n)$，其余操作都是 $O(1)$，其中 n 是栈内的元素个数。

  入栈操作需要将 $queue_1$ 中的几 个元素出队，并入队 $n+1$ 个元素到 $queue_2$，共有$2n +1$次操作，每次出队和入队操作的时间复杂度都是$O(1)$，因此入栈操作的时间复杂度是 $O(n)$。
  出栈操作对应将 $queue_1$ 的前端元素出队，时间复杂度是 $O(1)$。
  获得栈顶元素操作对应获得 $queue_1$ 的前端元素，时间复杂度是 $O(1)$。
  判断栈是否为空操作只需要判断 $queue_1$，是否为空，时间复杂度是 $O(1)$。

- 空间复杂度：$O(n)$，其中 $n$ 是栈内的元素个数。需要使用两个队列存储栈内的元素。

  

  

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_26_225_fig1.gif" alt="fig1" style="zoom:80%;" />

```typescript
class MyStack {
    queue1: number[] = [];
    queue2: number[] = [];
    constructor() {

    }

    push(x: number): void {
         this.queue2.push(x);
         while(this.queue1.length !== 0) {
             this.queue2.push(this.queue1.shift());
         }
         [this.queue1, this.queue2] = [this.queue2, this.queue1];
    }

    pop(): number {
        return this.queue1.shift();
    }

    top(): number {
        return this.queue1[0];
    }

    empty(): boolean {
        return this.queue1.length === 0;
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * var obj = new MyStack()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.empty()
 */
```

### 一个队列

- 时间复杂度：入栈操作 $O(n)$，其余操作都是 $O(1)$，其中 n 是栈内的元素个数。

  入栈操作需要将 $queue_1$ 中的几 个元素出队，并入队 $n+1$ 个元素到 $queue_2$，共有$2n +1$次操作，每次出队和入队操作的时间复杂度都是$O(1)$，因此入栈操作的时间复杂度是 $O(n)$。
  出栈操作对应将 $queue_1$ 的前端元素出队，时间复杂度是 $O(1)$。
  获得栈顶元素操作对应获得 $queue_1$ 的前端元素，时间复杂度是 $O(1)$。
  判断栈是否为空操作只需要判断 $queue_1$，是否为空，时间复杂度是 $O(1)$。

- 空间复杂度：$O(n)$，其中 $n$ 是栈内的元素个数。需要使用一个队列存储栈内的元素。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_26_225_fig2.gif" alt="fig2" style="zoom:80%;" />

```typescript
class MyStack {
    queue: number[] = [];
    constructor() {

    }

    push(x: number): void {
        let n = this.queue.length;
        this.queue.push(x);
        while (n > 0) {
            n--;
            this.queue.push(this.queue.shift());
        }
    }

    pop(): number {
        return this.queue.shift();
    }

    top(): number {
        return this.queue[0];
    }

    empty(): boolean {
        return this.queue.length === 0;
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * var obj = new MyStack()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.empty()
 */
```



## 20. 有效的括号

> 给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。
>
> 有效字符串需满足：
>
> - 左括号必须用相同类型的右括号闭合。
> - 左括号必须以正确的顺序闭合。
> - 注意空字符串可被认为是有效字符串。
>
> 示例 1:
>
> - 输入: "()"
> - 输出: true
>
> 示例 2:
>
> - 输入: "()[]{}"
> - 输出: true
>
> 示例 3:
>
> - 输入: "(]"
> - 输出: false
>
> 示例 4:
>
> - 输入: "([)]"
> - 输出: false
>
> 示例 5:
>
> - 输入: "{[]}"
> - 输出: true

###  栈

- 时间复杂度：$O(N)$ ，$N$ 为字符串的长度。
- 空间复杂度：$O(N)$，哈希表和栈使用线性的空间大小。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_29_iShot_2023-05-29_09.49.53.gif" alt="iShot_2023-05-29_09.49.53" />

```typescript
function isValid(s: string): boolean {
		if (s.length % 2 === 1) return false;
    const stack: string[] = [];
    for (let str of s) {
        switch (str) {
            case '(':
            case '[':
            case '{':
                stack.unshift(str);
                break;
            case ')':
                if (stack.shift() !== '(') return false;
                break;
            case ']':
                if (stack.shift() !== '[') return false;
                break;
            case '}':
                if (stack.shift() !== '{') return false;
                break;
        }
    }
    return stack.length === 0;
};
```



## 1047.删除字符串中的所有相邻重复项

> 给出由小写字母组成的字符串 S，重复项删除操作会选择两个相邻且相同的字母，并删除它们。
>
> 在 S 上反复执行重复项删除操作，直到无法继续删除。
>
> 在完成所有重复项删除操作后返回最终的字符串。答案保证唯一。
>
> 示例：
>
> - 输入："abbaca"
> - 输出："ca"
> - 解释：例如，在 "abbaca" 中，我们可以删除 "bb" 由于两字母相邻且相同，这是此时唯一可以执行删除操作的重复项。之后我们得到字符串 "aaca"，其中又只有 "aa" 可以执行重复项删除操作，所以最后的字符串为 "ca"。
>
> 提示：
>
> - 1 <= S.length <= 20000
> - S 仅由小写英文字母组成。

### 栈

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$或$O(1)$，取决于使用的语言提供的字符串类是否提供了类似「入栈」和「出栈」的接口。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_29_iShot_2023-05-29_10.06.14.gif" alt="iShot_2023-05-29_10.06.14" />

```typescript
function removeDuplicates(s: string): string {
    const stack: string[] = [];
    for (let str of s) {
        if (stack[stack.length - 1] === str) {
            stack.pop();
        } else {
            stack.push(str);
        }
    }
    return stack.join("");
};
```



## 0150.逆波兰表达式求值

> 根据 逆波兰表示法，求表达式的值。
>
> 有效的运算符包括 + , - , * , / 。每个运算对象可以是整数，也可以是另一个逆波兰表达式。
>
> 说明：
>
> 整数除法只保留整数部分。 给定逆波兰表达式总是有效的。换句话说，表达式总会得出有效数值且不存在除数为 0 的情况。
>
> 示例 1：
>
> - 输入: ["2", "1", "+", "3", " * "]
> - 输出: 9
> - 解释: 该算式转化为常见的中缀算术表达式为：((2 + 1) * 3) = 9
>
> 示例 2：
>
> - 输入: ["4", "13", "5", "/", "+"]
> - 输出: 6
> - 解释: 该算式转化为常见的中缀算术表达式为：(4 + (13 / 5)) = 6
>
> 示例 3：
>
> - 输入: ["10", "6", "9", "3", "+", "-11", " * ", "/", " * ", "17", "+", "5", "+"]
>
> - 输出: 22
>
> - 解释:该算式转化为常见的中缀算术表达式为：
>
>   ```
>   ((10 * (6 / ((9 + 3) * -11))) + 17) + 5       
>   = ((10 * (6 / (12 * -11))) + 17) + 5       
>   = ((10 * (6 / -132)) + 17) + 5     
>   = ((10 * 0) + 17) + 5     
>   = (0 + 17) + 5    
>   = 17 + 5    
>   = 22    
>   ```
>
> 逆波兰表达式：是一种后缀表达式，所谓后缀就是指运算符写在后面。
>
> 平常使用的算式则是一种中缀表达式，如 ( 1 + 2 ) * ( 3 + 4 ) 。
>
> 该算式的逆波兰表达式写法为 ( ( 1 2 + ) ( 3 4 + ) * ) 。
>
> 逆波兰表达式主要有以下两个优点：
>
> - 去掉括号后表达式无歧义，上式即便写成 1 2 + 3 4 + * 也可以依据次序计算出正确结果。
> - 适合用栈操作运算：遇到数字则入栈；遇到运算符则取出栈顶两个数字进行计算，并将结果压入栈中。

### 栈

- 时间复杂度：$O(n)$，其中 $n$ 是数组 tokens 的长度。
- 空间复杂度：$O(n)$，其中 $n$ 是数组 tokens 的长度。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_29_iShot_2023-05-29_10.42.12.gif" alt="iShot_2023-05-29_10.42.12" />

```typescript
function evalRPN(tokens: string[]): number {
    const stack: number[] = [];
    for (let token of tokens) {
        switch (token) {
            case '+':
                stack.unshift(stack.shift() + stack.shift());
                break;
            case '-':
                let sub = stack.shift();
                stack.unshift(stack.shift() - sub);
                break;
            case '*':
                stack.unshift(stack.shift() * stack.shift());
                break;
            case '/':
                let divided = stack.shift()
                let res = stack.shift() / divided;
                stack.unshift(res > 0 ? Math.floor(res) : Math.ceil(res));
                break;
            default:
                stack.unshift(Number(token));
        }
    }
    return stack.shift();
};
```



## 239.滑动窗口最大值

> 给你一个整数数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。
>
> 返回 滑动窗口中的最大值 。
>
> **示例1：**
>
> ```
> 输入：nums = [1,3,-1,-3,5,3,6,7], k = 3
> 输出：[3,3,5,5,6,7]
> 解释：
> 滑动窗口的位置                最大值
> ---------------               -----
> [1  3  -1] -3  5  3  6  7       3
>  1 [3  -1  -3] 5  3  6  7       3
>  1  3 [-1  -3  5] 3  6  7       5
>  1  3  -1 [-3  5  3] 6  7       5
>  1  3  -1  -3 [5  3  6] 7       6
>  1  3  -1  -3  5 [3  6  7]      7
> ```
>
> **示例 2：**
>
> ```
> 输入：nums = [1], k = 1
> 输出：[1]
> ```
>
> **提示：**
>
> - `1 <= nums.length <= 105`
> - `-104 <= nums[i] <= 104`
> - `1 <= k <= nums.length`

### 单调队列

> 双端队列（Deque，全称double-ended queue）是一种具有队列和栈的性质的数据结构。双端队列的元素可以从两端弹出，其限制插入和删除操作在表的两端进行。这意味着你可以在其前端以及后端进行插入和删除操作。
>
> 双端队列就像是一个队列和栈的结合体，结合了它们的一些功能。你可以将元素添加或删除到队列的前面或后面，就像在栈中一样。
>
> 当双端队列用来维护滑动窗口中的最大值或最小值时，我们通常将其称为单调队列。在这种情况下，双端队列将始终保持单调递增或递减的顺序。新元素从队列一端加入，在另一端移出。为了保持队列的单调性，有些元素可能会在其正常出队前就被提前移出。因此，双端队列在此应用中也被称为单调双端队列。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_30_iShot_2023-05-30_10.53.23.gif" alt="iShot_2023-05-30_10.53.23" />

- 时间复杂度：$O(n)$，其中 n 是数组 $nums$ 的长度。
- 空间复杂度：$O(k)$。

```typescript
function maxSlidingWindow(nums: number[], k: number): number[] {
    if (nums.length === 0) return [];
    const res: number[] = [];
    const deque: number[] = [];
    for (let i = 0; i < k; i++) {
        while (deque.length !== 0 && deque[deque.length - 1] < nums[i]) {
            deque.pop();
        }
        deque.push(nums[i]);
    }
    res.push(deque[0]);
    for (let i = k; i < nums.length; i++) {
        if (nums[i - k] === deque[0]) {
            deque.shift();
        }
        while (deque.length !== 0 && deque[deque.length - 1] < nums[i]) {
            deque.pop();
        }
        deque.push(nums[i]);
        res.push(deque[0]);
    }
    return res;
};
```



## 347.前K个高频元素

> 给定一个非空的整数数组，返回其中出现频率前 k 高的元素。
>
> 示例 1:
>
> - 输入: nums = [1,1,1,2,2,3], k = 2
> - 输出: [1,2]
>
> 示例 2:
>
> - 输入: nums = [1], k = 1
> - 输出: [1]
>
> 提示：
>
> - 你可以假设给定的 k 总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。
> - 你的算法的时间复杂度必须优于 $O(n longn)$ , n 是数组的大小。
> - 题目数据保证答案唯一，换句话说，数组中前 k 个高频元素的集合是唯一的。
> - 你可以按任意顺序返回答案。

### 哈希表+优先队列

> 优先级队列是一种抽象数据类型，它类似于一个常规的队列或栈数据结构，但每个元素都有一定的关联优先级。在优先级队列中，元素被赋予优先级。当访问元素时，具有最高优先级的元素首先被删除。当两个元素具有相同优先级时，按照它们在队列中的顺序进行访问。优先级队列在许多算法中都有应用，包括Dijkstra's algorithm和heap sort。
>
> 优先级队列通常使用堆（Heap）数据结构来实现，但也可以使用其他数据结构，如有序数组、有序链表、平衡树等。在堆的实现中，元素可以在O(1)时间内获取（查看）最大/最小元素，而删除最大元素和插入新元素则需要O(log n)的时间。其中，n是队列中的元素数量。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_05_30_image-20230530152420887.png" alt="image-20230530152420887" style="zoom: 50%;" />

- 时间复杂度：$O(Nlogk)$，其中 N 为数组的长度。由于堆的大小至多为 k，因此每次堆操作需要 $O(log k)$的时间。
- 空间复杂度：$O(N)$。哈希表的大小为$O(N)$，而堆的大小为$O(k)$，共计为$O(N)$。

```typescript
class MiniHeap {
    private heap: [number, number][] = [[0, 0]];
    getHeap() {
        return this.heap;
    }
    swap(i1: number, i2: number) {
        [this.heap[i1], this.heap[i2]] = [this.heap[i2], this.heap[i1]];
    }
    getParentIndex(i: number) {
        return Math.floor(i / 2);
    }
    getLeftIndex(i: number) {
        return 2 * i;
    }
    getRightIndex(i: number) {
        return 2 * i + 1;
    }
    swim(index: number) {
        if (index === 1) return;
        const parentIndex = this.getParentIndex(index);
        if (this.heap[parentIndex][1] > this.heap[index][1]) {
            this.swap(parentIndex, index);
            this.swim(parentIndex);
        }
    }
    sink(index: number) {
        const leftIndex = this.getLeftIndex(index);
        const rightIndex = this.getRightIndex(index);
        if (this.heap[leftIndex] && this.heap[leftIndex][1] < this.heap[index][1]) {
            this.swap(leftIndex, index);
            this.sink(leftIndex);
        }
        if (this.heap[rightIndex] && this.heap[rightIndex][1] < this.heap[index][1]) {
            this.swap(rightIndex, index);
            this.sink(rightIndex);
        }
    }
    insert(value: [number, number]) {
        this.heap.push(value);
        this.swim(this.heap.length - 1);
    }
    pop() {
        if (this.size() === 1) return this.heap.splice(1, 1)[0];
        const top = this.heap[1];
        this.heap[1] = this.heap.pop();
        this.sink(1);
        return top;
    }
    peek() {
        return this.heap[1];
    }
    size() {
        return this.heap.length - 1;
    }
}

function topKFrequent(nums: number[], k: number): number[] {
    const map = new Map<number, number>();
    for (let i = 0; i < nums.length; i++) {
        map.set(nums[i], map.has(nums[i]) ? map.get(nums[i]) + 1 : 1);
    }
    const heap = new MiniHeap();
    for (let [key, value] of map.entries()) {
        heap.insert([key, value]);
        if (heap.size() > k) {
            heap.pop();
        }
    }
    return heap.getHeap().slice(1).map(item => item[0]);
};
```



# 二叉树

## 144.二叉树的前序遍历

> 给定一个二叉树的根节点 `root` ，返回 *它的 **前序** 遍历* 。
>
> **示例1：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_01_inorder_1.jpg" alt="img" style="zoom:100%; float: left;" />
>
> ```
> 输入：root = [1,null,2,3]
> 输出：[1,2,3]
> ```
>
> **示例 2：**
>
> ```
> 输入：root = []
> 输出：[]
> ```
>
> **示例 3：**
>
> ```
> 输入：root = [1]
> 输出：[1]
> ```

### 递归

- 时间复杂度：$O(n)$，其中 $n$ 是二叉树的节点数。
- 空间复杂度：$O(n)$，为递归过程中栈的开销，平均情况下为 $O(log n)$，最坏情况下树呈现链栈，为 $O(n)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function preorderTraversal(root: TreeNode | null): number[] {
    if (root === null) return;
    let res = [];
    res.push(root.val);
    res = res.concat(preorderTraversal(root.left));
    res = res.concat(preorderTraversal(root.right));
    return res;
};
```

### 迭代

迭代与递归的区别在于递归的时候隐式地维护了一个栈，而迭代需要显式将这个栈模拟出来。

- 时间复杂度：$O(n)$，其中 $n$ 是二叉树的节点数。
- 空间复杂度：$O(n)$，为递归过程中栈的开销，平均情况下为 $O(log n)$，最坏情况下树呈现链栈，为 $O(n)$。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_01_iShot_2023-06-01_11.39.08.gif" alt="iShot_2023-06-01_11.39.08" />

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_01_6233a9685447d0b4d7b513f739151ca065e5697e24070bcafc1ee5d28f9155a6.png" alt="中序遍历流程图" style="zoom: 50%;" />

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_01_c455ec4e7f33352334ceb3af14e3b53297a36cc7891dab2abf66be35b239d664.gif" alt="img" style="zoom:67%;" />

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function preorderTraversal(root: TreeNode | null): number[] {
    const stack: TreeNode[] = [];
    const res: number[] = [];
    stack.push(root);
    while (stack.length > 0) {
        let temp = stack.pop();
        res.push(temp.val);
        if (temp.right !== null) {
            stack.push(temp.right);
        }
        if (temp.left !== null) {
            stack.push(temp.left);
        }
        console.log(stack.length)
    }
    return res;
};
```

### Morris遍历

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_01_143b40666eebb8992b1ed7e6c35d4d5f3b93c6f20ab436e5c9ffa54032c392c0.png" alt="在这里插入图片描述" style="zoom: 50%;" />

- 时间复杂度：$O(n)$，其中 $n$ 是二叉树的节点数。没有左子树的节点只被访问依次，有左子树的节点被访问两次。
- 空间复杂度：$O(1)$。只操作已经存在的指针，因此只需要常数的额外空间。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function preorderTraversal(root: TreeNode | null): number[] {
    if (root === null) return;
    let cur1: TreeNode = root;
    let cur2: TreeNode = null;
    const res: number[] = [];
    while (cur1 !== null) {
        cur2 = cur1.left;
        if (cur2 !== null) {
            while (cur2.right !== null && cur2.right !== cur1) {
                cur2 = cur2.right;
            }
            if (cur2.right === null) {
                cur2.right = cur1;
                res.push(cur1.val);
                cur1 = cur1.left;
                continue;
            } else {
                cur2.right = null;
            }
        } else {
            res.push(cur1.val);
        }
        cur1 = cur1.right;
    }
    return res;
};
```

### 颜色标记法

其核心思想如下：

- 使用颜色标记节点的状态，新节点为白色，已访问的节点为灰色。

- 如果遇到的节点为白色，则将其标记为灰色，然后将其右子节点、自身、左子节点依次入栈。
- 如果遇到的节点为灰色，则将节点的值输出。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function preorderTraversal(root: TreeNode | null): number[] {
    const WHITE = 0, GRAY = 1;
    const res: number[] = [];
    const stack: [number, TreeNode][] = [[WHITE, root]];
    while (stack.length > 0) {
        const [color, node] = stack.pop();
        if (node === null) continue;
        if (color === WHITE) {
            stack.push([WHITE, node.right]);
            stack.push([WHITE, node.left]);
            stack.push([GRAY, node]);
        } else {
            res.push(node.val);
        }
    }
    return res;
};
```



## 94.二叉树的中序遍历

> 给定一个二叉树的根节点 `root` ，返回 *它的 **中序** 遍历* 。
>
> **示例1：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_01_inorder_1.jpg" alt="img" style="zoom:100%; float: left;" />
>
> ```
> 输入：root = [1,null,2,3]
> 输出：[1,3,2]
> ```
>
> **示例 2：**
>
> ```
> 输入：root = []
> 输出：[]
> ```
>
> **示例 3：**
>
> ```
> 输入：root = [1]
> 输出：[1]
> ```

### 递归

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function inorderTraversal(root: TreeNode | null): number[] {
    if (root === null) return [];
    let res: number[] = [];
    res = res.concat(inorderTraversal(root.left));
    res.push(root.val);
    res = res.concat(inorderTraversal(root.right));
    return res;
};
```

### 迭代

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_01_iShot_2023-06-01_15.21.27.gif" alt="iShot_2023-06-01_15.21.27" />

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function inorderTraversal(root: TreeNode | null): number[] {
    let res: number[] = [];
    let stack: TreeNode[] = [];
    while (stack.length > 0 || root !== null) {
        while (root !== null) {
            stack.push(root);
            root = root.left;
        }
        root = stack.pop();
        res.push(root.val);
        root = root.right;
    }
    return res;
};
```

### 颜色标记法

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function inorderTraversal(root: TreeNode | null): number[] {
    const WHITE = 0, GRAY = 1;
    const res: number[] = [];
    const stack: [number, TreeNode][] = [[WHITE, root]];
    while (stack.length > 0) {
        const [color, node] = stack.pop();
        if (node === null) continue;
        if (color === WHITE) {
            stack.push([WHITE, node.right]);
            stack.push([GRAY, node]);
            stack.push([WHITE, node.left]);
        } else {
            res.push(node.val);
        }
    }
    return res;
};
```



## 145.二叉树的后序遍历

> 给定一个二叉树的根节点 `root` ，返回 *它的 **后序** 遍历* 。
>
> **示例1：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_01_inorder_1.jpg" alt="img" style="zoom:100%; float: left;" />
>
> ```
> 输入：root = [1,null,2,3]
> 输出：[3,2,1]
> ```
>
> **示例 2：**
>
> ```
> 输入：root = []
> 输出：[]
> ```
>
> **示例 3：**
>
> ```
> 输入：root = [1]
> 输出：[1]
> ```

### 递归

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function postorderTraversal(root: TreeNode | null): number[] {
    if (root === null) return [];
    let res: number[] = [];
    res = res.concat(postorderTraversal(root.left));
    res = res.concat(postorderTraversal(root.right));
    res.push(root.val);
    return res;
};
```

### 颜色标记法

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function postorderTraversal(root: TreeNode | null): number[] {
    const WHITE = 0, GRAY = 1;
    const res: number[] = [];
    const stack: [number, TreeNode][] = [[WHITE, root]];
    while (stack.length > 0) {
        const [color, node] = stack.pop();
        if (node === null) {
            continue;
        }
        if (color === WHITE) {
            stack.push([GRAY, node]);
            stack.push([WHITE, node.right]);
            stack.push([WHITE, node.left]);
        } else {
            res.push(node.val);
        }
    }
    return res;
};
```



## 102.二叉树的层序遍历

> 给你二叉树的根节点 `root` ，返回其节点值的 **层序遍历** 。 （即逐层地，从左到右访问所有节点）。

### BFS

使用队列维护节点。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_02_fdcd3bd27f4008948084f6ec86b58535e71f66862bd89a34bd6fe4cc42d68e89.gif" alt="DFS 与 BFS 对比" style="zoom: 50%;" />

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_02_94cd1fa999df0276f1dae77a9cca83f4cabda9e2e0b8571cd9550a8ee3545f56.gif" alt="img" style="zoom:50%;" />

- 时间复杂度：每个点进队出队各一次，故复杂度为$O(n)$。
- 空间复杂度：队列中元素的个数不超过 $n$ 个，故复杂度为$O(n)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function levelOrder(root: TreeNode | null): number[][] {
    if (root === null) return [];
    const queue: TreeNode[] = [root];
    const res: number[][] = [];
    while (queue.length > 0) {
        let n = queue.length;
        const temp: number[] = [];
        for (let i = 0; i < n; i++) {
            let node = queue.shift();
            temp.push(node.val);
            if (node.left !== null) {
                queue.push(node.left);
            }
            if (node.right !== null) {
                queue.push(node.right);
            }
        }
        res.push(temp);
    }
    return res;
};
```



## 226.翻转二叉树

> 给你一棵二叉树的根节点 `root` ，翻转这棵二叉树，并返回其根节点。
>
> **示例 1：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_05_invert1-tree.jpg" alt="img" style="float: left; zoom: 50%;" />
>
> ```
> 输入：root = [4,2,7,1,3,6,9]
> 输出：[4,7,2,9,6,3,1]
> ```
>
> **示例 2：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_05_invert2-tree.jpg" alt="img" style="zoom:50%;float:left;" />
>
> ```
> 输入：root = [2,1,3]
> 输出：[2,3,1]
> ```

### BFS-迭代

用一个队列来临时存放需要遍历到的元素。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_05_f9e06159617cbf8372b544daee37be70286c3d9b762c016664e225044fc4d479-226_%E8%BF%AD%E4%BB%A3.gif" alt="226_迭代.gif" style="zoom:33%;" />

- 时间复杂度：$O(N)$，每个节点需要入队/出队一次。
- 空间复杂度：$O(N)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function invertTree(root: TreeNode | null): TreeNode | null {
    if (root === null) return null;
    let queue: TreeNode[] = [root];
    while (queue.length !== 0) {
        let node = queue.shift();
        if (node.left) {
            queue.push(node.left);
        }
        if (node.right) {
            queue.push(node.right);
        }
        [node.left, node.right] = [node.right, node.left];
    }
    return root;
};
```

### DFS-递归

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_05_0f91f7cbf5740de86e881eb7427c6c3993f4eca3624ca275d71e21c5e3e2c550-226_2.gif" alt="226_2.gif" style="zoom:40%;" />

- 时间复杂度：$O(N)$，每个元素都必须访问一次。
- 空间复杂度：$O(N)$。使用的空间由递归栈的深度决定，它等于当前节点在二叉树中的高度。在平均情况下，二叉树的高度与节点个数为对数关系，即$O(log N)$。而在最坏情况下，树形成链状，空间复杂度为$O(N)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function invertTree(root: TreeNode | null): TreeNode | null {
    if (root === null) return null;
    if (root.left) invertTree(root.left);
    if (root.right) invertTree(root.right);
    [root.left, root.right] = [root.right, root.left];
    return root;
};
```



## 100.相同的树

> 给你两棵二叉树的根节点 `p` 和 `q` ，编写一个函数来检验这两棵树是否相同。
>
> 如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

### DFS

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_08_iShot_2023-06-08_15.01.47.gif" alt="iShot_2023-06-08_15.01.47" style="zoom:80%;" />

- 时间复杂度：$O(min(m,n))$，其中 m 和 n 分别是两个二叉树的节点数。对两个二叉树同时进行深度优先搜索，只有当两个二叉树中的对应节点都不为空时才会访问到该节点，因此被访问的节点数不会超过较小的二叉树的节点数。
- 空间复杂度：$O(min(m,n))$，其中 m 和 n 分别是两个二叉树的节点数。空间复杂度取决于递归调用的层数，递归调用的层数不会超过较小的二叉树的最大高度，最坏情况下，二叉树的高度等于节点数。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function isSameTree(p: TreeNode | null, q: TreeNode | null): boolean {
    if (p === null && q === null) return true;
    if (p === null || q === null) return false;
    return p.val === q.val && isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
};
```



## 101.对称二叉树

> 给你一个二叉树的根节点 `root` ， 检查它是否轴对称。
>
> **示例 1：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_05_symtree1.jpg" alt="img" style="float:left;" />
>
> ```
> 输入：root = [1,2,2,3,4,4,3]
> 输出：true
> ```
>
> **示例 2：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_05_symtree2.jpg" alt="img" style="float:left;" />
>
> ```
> 输入：root = [1,2,2,null,3,null,3]
> 输出：false
> ```

### 递归

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_05_2449af8862537df2cbbc45a07764415c1a10769677c822fa271ea7447c8fa128-2.gif" alt="2.gif" style="zoom:33%;" />

- 时间复杂度：$O(N)$，遍历整棵树。
- 空间复杂度：$O(N)$，空间复杂度与递归使用的栈空间有关，递归层树不超过n。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function check(p: TreeNode, q: TreeNode): boolean {
    if (p === null && q === null) return true;
    if (p === null || q === null) return false;
    return p.val === q.val && check(p.left, q.right) && check(p.right, q.left);
}

function isSymmetric(root: TreeNode | null): boolean {
    if (root === null) return;
    return check(root.left, root.right);
};
```

### 迭代

用一个队列来维护节点，一次取出两个节点进行比较。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_05_45a663b08efaa14193d63ef63ae3d1d130807467d13707f584906ad3af4adc36-1.gif" alt="1.gif" style="zoom:33%;" />

- 时间复杂度：$O(N)$。
- 空间复杂度：这里需要用一个队列来维护节点，每个节点最多进队一次，出队一次，队列中最多不会超过n个点，故为$O(N)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function isSymmetric(root: TreeNode | null): boolean {
    const queue: TreeNode[] = [root, root];
    while (queue.length !== 0) {
        const u = queue.shift();
        const v = queue.shift();
        if (u === null && v === null) continue;
        if ((u === null || v === null) || (u.val !== v.val)) return false;
        
        queue.push(u.left);
        queue.push(v.right);

        queue.push(u.right);
        queue.push(v.left);
    }
    return true;
};
```



## 104.二叉树的最大深度

> 给定一个二叉树，找出其最大深度。
>
> 二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。
>
> 说明: 叶子节点是指没有子节点的节点。
>
> 示例：
> 给定二叉树 [3,9,20,null,null,15,7]，
>
> ```
>     3
>    / \
>   9  20
>     /  \
>    15   7
> ```
>
> 返回它的最大深度 3 。

### DFS-递归

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_06_iShot_2023-06-06_17.02.40.gif" alt="iShot_2023-06-06_17.02.40" style="zoom:80%;" />

- 时间复杂度：$O(n)$，其中n为二叉树的个数。每个节点在递归中只被遍历一次。
- 空间复杂度：$O(height)$，其中 $height$ 表示二叉树的高度。递归函数需要栈空间，而栈空间取决于递归的深度，因此空间复杂度等于二叉树的高度。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function maxDepth(root: TreeNode | null, level = 1): number {
    if (root === null) return 0;
    if (root.left === null && root.right === null) return level;
    let leftLevel = 0;
    let rightLevel = 0;
    if (root.left) {
        leftLevel = maxDepth(root.left, level + 1);
    }
    if (root.right) {
        rightLevel = maxDepth(root.right, level + 1);
    }
    level = Math.max(leftLevel, rightLevel);
    return level;
};
```

### BFS-迭代

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_06_iShot_2023-06-06_17.52.57.gif" alt="iShot_2023-06-06_17.52.57" style="zoom:80%;" />

- 时间复杂度：$O(n)$，其中 n 为二叉树的节点个数。与方法一同样的分析，每个节点只会被访问一次。
- 空间复杂度：此方法空间的消耗取决于队列存储的元素数量，其在最坏情况下会达到 $O(n)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function maxDepth(root: TreeNode | null): number {
    if (root === null) return 0;
    const queue: TreeNode[] = [root];
    let ans = 0;
    while (queue.length > 0) {
        let size = queue.length;
        while (size > 0) {
            const node = queue.shift();
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
            size -= 1;
        }
        ans += 1;
    }
    return ans;
};
```



## 111.二叉树的最小深度

> 给定一个二叉树，找出其最小深度。
>
> 最小深度是从根节点到最近叶子节点的最短路径上的节点数量。
>
> **说明：**叶子节点是指没有子节点的节点。
>
> **示例 1：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_06_ex_depth.jpg" alt="img" style="float: left; zoom: 67%;" />
>
> ```
> 输入：root = [3,9,20,null,null,15,7]
> 输出：2
> ```
>
> **示例 2：**
>
> ```
> 输入：root = [2,null,3,null,4,null,5,null,6]
> 输出：5
> ```

### DFS-递归

与上一题是同样的套路。

- 时间复杂度：$O(N)$，其中 N 是数的节点数。对每个节点访问一次。
- 空间复杂度：$O(H)$，其中 H 是树的高度。空间复杂度主要取决于递归时栈空间的开销，最坏情况下，树呈现链状，空间复杂度为$O(N)$。平均情况下树的高度与节点数的对数正相关，空间复杂度为$O(logN)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function minDepth(root: TreeNode | null, level = 1): number {
    if (root === null) return 0;
    if (root.left === null && root.right === null) return level;
    let leftLevel = Infinity;
    let rightLevel = Infinity;
    if (root.left) {
        leftLevel = minDepth(root.left, level + 1);
    }
    if (root.right) {
        rightLevel = minDepth(root.right, level + 1);
    }
    level = Math.min(leftLevel, rightLevel);
    return level;
};
```

### BFS-迭代

- 时间复杂度：$O(N)$，其中 N 是树的节点数。对每个节点访问一次。
- 空间复杂度：$O(N)$，其中 N 是树的节点数。空间复杂度主要取决于队列的开销，队列中的元素个数不会超过树的节点数。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function minDepth(root: TreeNode | null): number {
    if (root === null) return 0;
    const queue: TreeNode[] = [root];
    let ans = 1;
    while (queue.length > 0) {
        let size = queue.length;
        while (size > 0) {
            const node = queue.shift();
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
            size -= 1;
            if (node.left === null && node.right === null) {
                return ans;
            }
        }
        ans += 1;
    }
};
```



## 222.完全二叉树的节点个数

> 给你一棵 完全二叉树 的根节点 root ，求出该树的节点个数。
>
> 完全二叉树 的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 h 层，则该层包含 1~ 2h 个节点。
>
> **示例 1：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_07_complete.jpg" alt="img" style="zoom:67%;float:left;" />
>
> ```
> 输入：root = [1,2,3,4,5,6]
> 输出：6
> ```
>
> **示例 2：**
>
> ```
> 输入：root = []
> 输出：0
> ```
>
> **示例 3：**
>
> ```
> 输入：root = [1]
> 输出：1
> ```

### 满二叉树+递归

思路：利用满二叉树的特性，判断左右子树如果深度相同，则直接返回$2^h-1$（可以利用位移特性）。否则继续递归传入左右子节点并加+1，继续计算子树的节点，也是利用满二叉树的特性。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_07_68747470733a2f2f636f64652d7468696e6b696e672d313235333835353039332e66696c652e6d7971636c6f75642e636f6d2f706963732f32303230313132343039323534333636322e706e67.png" alt="222.完全二叉树的节点个数" style="zoom:33%;" />

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_07_68747470733a2f2f636f64652d7468696e6b696e672d313235333835353039332e66696c652e6d7971636c6f75642e636f6d2f706963732f32303230313132343039323633343133382e706e67.png" alt="222.完全二叉树的节点个数1" style="zoom:33%;" />

- 时间复杂度：$O(logn * logn)$。
- 空间复杂度：$O(logn)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function countNodes(root: TreeNode | null): number {
    if (root === null) return 0;
    let leftCount = 0;
    let rightCount = 0;
    let leftNode = root.left;
    let rightNode= root.right;
    while (leftNode) {
        leftNode = leftNode.left;
        leftCount++;
    }
    while (rightCount) {
        rightNode = rightNode.right;
        rightCount++;
    }
    if (leftCount === rightCount) {
        return (2 << leftCount) - 1;
    }
    return countNodes(root.left) + countNodes(root.right) + 1;
};
```



## 110.平衡二叉树

> xxxx

### 自底向上递归

自底向上使用后序遍历。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_07_iShot_2023-06-07_18.35.44.gif" alt="iShot_2023-06-07_18.35.44" style="zoom:80%;" />

- 时间复杂度：$O(n)$，其中 n 是二叉树中的节点个数。使用自底向上的递归，每个节点的计算高度和判断是否平衡都只需要处理一次，最坏情况下需要遍历二叉树中的所有节点，因此时间复杂度是$O(n)$。
- 空间复杂度：$O(n)$，其中 n 是二叉树中的节点个数。空间复杂度主要取决于递归调用的层树，递归调用的层树不会超过 n。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function height(root: TreeNode): number {
    if (root === null) return 0;
    let leftHeight = height(root.left);
    let rightHeight = height(root.right);
    if (leftHeight === -1 || rightHeight === -1 || Math.abs(leftHeight - rightHeight) > 1) {
        return -1
    } else {
        return Math.max(leftHeight, rightHeight) + 1;
    }
}

function isBalanced(root: TreeNode | null): boolean {
    return height(root) >= 0;
};
```



## 257.二叉树的所有路径

> 给你一个二叉树的根节点 `root` ，按 **任意顺序** ，返回所有从根节点到叶子节点的路径。
>
> **叶子节点** 是指没有子节点的节点。
>
> **示例 1：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_08_paths-tree.jpg" alt="img" style="zoom:67%;float:left;" />
>
> ```
> 输入：root = [1,2,3,null,5]
> 输出：["1->2->5","1->3"]
> ```
>
> **示例 2：**
>
> ```
> 输入：root = [1]
> 输出：["1"]
> ```

### DFS-前序遍历-递归-回溯

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_08_68747470733a2f2f636f64652d7468696e6b696e672d313235333835353039332e66696c652e6d7971636c6f75642e636f6d2f706963732f32303231303230343135313730323434332e706e67.png" alt="257.二叉树的所有路径" style="zoom: 50%;" />

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function binaryTreePaths(root: TreeNode | null, path: number[] = []): string[] {
    if (root === null) return [];
    path = path.concat([root.val]);
    if (root.left === null && root.right === null) {
        return [path.join("->")];
    }
    let leftPath: string[] = [];
    let rightPath: string[] = [];
    if (root.left) {
        leftPath = binaryTreePaths(root.left, path);
    }
    if (root.right) {
        rightPath = binaryTreePaths(root.right, path);
    }
    return leftPath.concat(rightPath);
};
```



## 404.左叶子之和

> 给定二叉树的根节点 `root` ，返回所有左叶子之和。
>
> **示例 1：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_09_leftsum-tree.jpg" alt="img" style="zoom:67%;float:left;" />
>
> ```
> 输入: root = [3,9,20,null,null,15,7] 
> 输出: 24 
> 解释: 在这个二叉树中，有两个左叶子，分别是 9 和 15，所以返回 24
> ```
>
> **示例 2:**
>
> ```
> 输入: root = [1]
> 输出: 0
> ```

### DFS-递归

- 时间复杂度：$O(n)$，其中 n 是树中的节点个数。
- 空间复杂度：$O(n)$。空间复杂度与深度优先搜索使用的栈的最大深度相关。在最坏的情况下，树呈现链式结构，深度为 $O(n)$，对应的空间复杂度也为 $O(n)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function sumOfLeftLeaves(root: TreeNode | null, isLeft = false): number {
    if (root === null) return 0;
    if (root.left === null && root.right === null) {
        if (isLeft) return root.val;
        else {
            return 0;
        }
    }
    let sum = 0;
    if (root.left) {
        sum += sumOfLeftLeaves(root.left, true);
    }
    if (root.right) {
        sum += sumOfLeftLeaves(root.right, false);
    }
    return sum;
};
```

### BFS-队列

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function isLeafNode(node: TreeNode) {
    return node.left === null && node.right === null;
}

function sumOfLeftLeaves(root: TreeNode | null): number {
    if (root === null) return 0;
    const queue: TreeNode[] = [root];
    let sum = 0;
    while (queue.length > 0) {
        let node = queue.shift();
        if (node.left) {
            if (isLeafNode(node.left)) {
                sum += node.left.val;
            }
            else {
                queue.push(node.left);
            }
        }
        if (node.right) {
            queue.push(node.right);
        }
    }
    return sum;
};
```



## 513.找树左下角的值

> 给定一个二叉树的 **根节点** `root`，请找出该二叉树的 **最底层 最左边** 节点的值。
>
> 假设二叉树中至少有一个节点。
>
> **示例 1:**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_09_tree1.jpg" alt="img" style="zoom:80%;float:left;" />
>
> ```
> 输入: root = [2,1,3]
> 输出: 1
> ```
>
> **示例 2:**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_09_tree2.jpg" alt="img" style="zoom:80%;float:left;" />
>
> ```
> 输入: [1,2,3,4,null,5,6,null,null,7]
> 输出: 7
> ```

### BFS-层序遍历-队列

- 时间复杂度：$O(n)$，其中 n 是二叉树的节点数目。
- 空间复杂度：$O(n)$。如果二叉树是满完全二叉树，那么队列 q 最多保存 $[n/2]$ 个节点。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function isLeafNode(root: TreeNode) {
    return root.left === null && root.right === null;
}

function findBottomLeftValue(root: TreeNode | null): number {
    if (root === null) return root.val;
    const queue: TreeNode[] = [root];
    let res = 0;
    while (queue.length > 0) {
        let size = queue.length;
        let isRecord = false;
        while (size > 0) {
            let node = queue.shift();
            if (isLeafNode(node) && !isRecord) {
                res = node.val;
                isRecord = true;
            }
            if (node.left) {
                queue.push(node.left);
            }
            if (node.right) {
                queue.push(node.right);
            }
            size--;
        }
    }
    return res;
};
```



## 112.路径总和

> 给你二叉树的根节点 root 和一个表示目标和的整数 targetSum 。判断该树中是否存在 根节点到叶子节点 的路径，这条路径上所有节点值相加等于目标和 targetSum 。如果存在，返回 true ；否则，返回 false 。
>
> 叶子节点 是指没有子节点的节点。
>
> **示例 1：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_09_pathsum1.jpg" alt="img" style="zoom:67%;float:left;" />
>
> 输入：root = [5,4,8,11,null,13,4,7,2,null,null,null,1], targetSum = 22
> 输出：true
> 解释：等于目标和的根节点到叶节点路径如上图所示。
>
> 

### DFS+递归

- 时间复杂度：$O(N)$，其中 N 是树的节点数。对每个节点访问一次。
- 空间复杂度：$O(H)$，其中 H 是树的高度。空间复杂度主要取决于递归时栈空间的开销，最坏情况下，树呈现链状，空间复杂度为$O(N)$。平均情况下树的高度与节点数的对数正相关，空间复杂度为$O(logN)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function hasPathSum(root: TreeNode | null, targetSum: number): boolean {
    if (root === null) return false;
    targetSum = targetSum - root.val;
    if (root.left === null && root.right === null) {
        return targetSum === 0;
    }
    return hasPathSum(root.left, targetSum) || hasPathSum(root.right, targetSum);
};
```

### BFS-层序遍历-双队列

- 时间复杂度：$O(N)$，其中 N 是树的节点数。对每一个节点访问一次。
- 空间复杂度：$O(N)$，其中 N 是树的节点数。空间复杂度主要取决于队列的开销，队列中的元素个数不会超过树的节点数。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_09_iShot_2023-06-09_16.05.51.gif" alt="iShot_2023-06-09_16.05.51" style="zoom:80%;" />

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function hasPathSum(root: TreeNode | null, targetSum: number): boolean {
    if (root === null) return false;
    const nodeQueue: TreeNode[] = [root];
    const valQueue: number[] = [root.val];
    while (nodeQueue.length > 0) {
        let node = nodeQueue.shift();
        let nodeVal = valQueue.shift();
        if (node.left === null && node.right === null && nodeVal === targetSum) return true;
        if (node.left) {
            nodeQueue.push(node.left);
            valQueue.push(nodeVal + node.left.val);
        }
        if (node.right) {
            nodeQueue.push(node.right);
            valQueue.push(nodeVal + node.right.val);
        }
    }
    return false;
};
```



## 105.从前序与中序遍历序列构造二叉树

> 给定两个整数数组 `preorder` 和 `inorder` ，其中 `preorder` 是二叉树的先序遍历， `inorder` 是同一棵树的中序遍历，请构造二叉树并返回其根节点。
>
> **示例 1:**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_12_tree-20230612121838646.jpg" alt="img" style="zoom:67%;float:left;" />
>
> ```
> 输入: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
> 输出: [3,9,20,null,null,15,7]
> ```
>
> **示例 2:**
>
> ```
> 输入: preorder = [-1], inorder = [-1]
> 输出: [-1]
> ```

### 递归

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_12_1686543450874.png" alt="1686543450874" style="zoom:33%;" />

- 时间复杂度：$O(n)$，其中 n 是树中的节点个数。
- 空间复杂度：$O(n)$。我们需要使用 $O(n)$的空间存储哈希表，以及 $O(h)$的空间表示递归时栈空间。这里 $h<m$， 所以总空间复杂度为 $O(n)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function buildTree(preorder: number[], inorder: number[]): TreeNode | null {
    let preIndex = 0;
    const mapIndex = new Map<number, number>();
    inorder.forEach((item, index) => {
        mapIndex.set(item, index);
    })
    const helper = (left: number, right: number): TreeNode | null => {
        if (left > right) return null;
        const rootVal = preorder[preIndex];
        const root = new TreeNode(rootVal);
        const index = mapIndex.get(rootVal);
        preIndex++;
        root.left = helper(left, index - 1);
        root.right = helper(index + 1, right);
        return root;
    }
    return helper(0, inorder.length - 1);
};
```



## 106.从中序与后序遍历序列构造二叉树

> 给定两个整数数组 inorder 和 postorder ，其中 inorder 是二叉树的中序遍历， postorder 是同一棵树的后序遍历，请你构造并返回这颗 二叉树 。
>
> 示例 1:
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_12_tree.jpg" alt="img" style="zoom:67%;float:left;" />
>
> ```
> 输入：inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
> 输出：[3,9,20,null,null,15,7]
> ```
>
> **示例 2:**
>
> ```
> 输入：inorder = [-1], postorder = [-1]
> 输出：[-1]
> ```

### 递归

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_12_iShot_2023-06-12_11.16.43.gif" alt="iShot_2023-06-12_11.16.43" style="zoom:80%;" />

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_12_1686541122376.png" alt="1686541122376" style="zoom: 33%;" />

- 时间复杂度：$O(n)$，其中 n 是树中的节点个数。
- 空间复杂度：$O(n)$。我们需要使用 $O(n)$的空间存储哈希表，以及 $O(h)$的空间表示递归时栈空间。这里 $h<m$， 所以总空间复杂度为 $O(n)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function buildTree(inorder: number[], postorder: number[]): TreeNode | null {
    let postIndex = postorder.length - 1;
    const mapIndex = new Map<number, number>();
    inorder.forEach((item, index) => {
        mapIndex.set(item, index);
    })
    const helper = (left: number, right: number): TreeNode | null => {
        if (left > right) return null;
        let rootVal = postorder[postIndex];
        const root = new TreeNode(rootVal);
        const index = mapIndex.get(rootVal);
        postIndex--;
        root.right = helper(index + 1, right);
        root.left = helper(left, index - 1);
        return root;
    }
    return helper(0, inorder.length - 1);
};
```



## 654.最大二叉树

> 给定一个不重复的整数数组 `nums` 。 最大二叉树 可以用下面的算法从 `nums` 递归地构建:
>
> 1. 创建一个根节点，其值为 `nums` 中的最大值。
> 2. 递归地在最大值 左边 的 子数组前缀上 构建左子树。
> 3. 递归地在最大值 右边 的 子数组后缀上 构建右子树。
>
> 返回 `nums` 构建的 最大二叉树 。
>
> **示例 1：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_12_tree1-20230612154401288.jpg" alt="img" style="zoom:80%;float:left;" />
>
> ```
> 输入：nums = [3,2,1,6,0,5]
> 输出：[6,3,5,null,2,0,null,null,1]
> 解释：递归调用如下所示：
> 
> - [3,2,1,6,0,5] 中的最大值是 6 ，左边部分是 [3,2,1] ，右边部分是 [0,5] 。
>   - [3,2,1] 中的最大值是 3 ，左边部分是 [] ，右边部分是 [2,1] 。
>     - 空数组，无子节点。
>     - [2,1] 中的最大值是 2 ，左边部分是 [] ，右边部分是 [1] 。
>       - 空数组，无子节点。
>       - 只有一个元素，所以子节点是一个值为 1 的节点。
>   - [0,5] 中的最大值是 5 ，左边部分是 [0] ，右边部分是 [] 。
>     - 只有一个元素，所以子节点是一个值为 0 的节点。
>     - 空数组，无子节点。
> ```

### 递归

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_12_1686556064389.png" alt="1686556064389" style="zoom:33%;" />

- 时间复杂度：$O(n^2)$，其中 n 是数组 `nums` 的长度。在最坏情况下，数组严格递增或递减，需要递归 n 层，第 $i(o \le i \le n)$ 层需要遍历 $n-i$ 个元素以找出最大值，总时间复杂度为 $O(n^2)$。
- 空间复杂度：$O(n)$，即最坏情况下需要使用的栈空间。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function constructMaximumBinaryTree(nums: number[]): TreeNode | null {
    if (nums.length === 0) return null;
    let maxNum: number = nums[0];
    let index: number = 0;
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] > maxNum) {
            maxNum = nums[i];
            index = i;
        }
    }
    const root = new TreeNode(maxNum);
    root.left = constructMaximumBinaryTree(nums.slice(0, index));
    root.right = constructMaximumBinaryTree(nums.slice(index + 1));
    return root;
};
```

### 单调栈

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_12_1660983435-LSVAnP-1.png" alt="1.png" style="zoom:33%;" />

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_12_1660983463-ErjdMy-1.png" alt="1.png" style="zoom:33%;" />

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_12_image-20230612162824600.png" alt="image-20230612162824600" style="zoom:50%;" />

- 时间复杂度：$O(n)$，其中 n 是数组 `nums` 的长度。单调栈求解左右边界和构造树均需要 $O(n)$ 的时间。
- 空间复杂度：$O(n)$，即为单调栈和数组 `tree` 需要使用的空间。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function constructMaximumBinaryTree(nums: number[]): TreeNode | null {
    if (nums.length === 0) return null;
    const dequeue: TreeNode[] = [];
    for (let i = 0; i < nums.length; i++) {
        const node = new TreeNode(nums[i]);
        if (dequeue.length === 0) {
            dequeue.push(node);
            continue;
        }
        while (dequeue.length > 0) {
          	// 入栈元素小于栈顶元素，入队
            if (dequeue[dequeue.length - 1].val > nums[i]) {
                dequeue[dequeue.length - 1].right = node;
                break;
            } 
            // 入栈元素大于栈顶元素，出队
          	else if (dequeue[dequeue.length - 1].val < nums[i]) {
                node.left = dequeue.pop();
            }
        }
        dequeue.push(node);
    }
    return dequeue[0];
};
```



## 617.合并二叉树

> 给你两棵二叉树： `root1` 和 `root2` 。
>
> 想象一下，当你将其中一棵覆盖到另一棵之上时，两棵树上的一些节点将会重叠（而另一些不会）。你需要将这两棵树合并成一棵新二叉树。合并的规则是：如果两个节点重叠，那么将这两个节点的值相加作为合并后节点的新值；否则，不为 null 的节点将直接作为新二叉树的节点。
>
> 返回合并后的二叉树。
>
> 注意: 合并过程必须从两个树的根节点开始。
>
> **示例 1：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_13_merge.jpg" alt="img" style="zoom:67%;float:left;" />
>
> ```
> 输入：root1 = [1,3,2,5], root2 = [2,1,3,null,4,null,7]
> 输出：[3,4,5,5,4,null,7]
> ```
>
> **示例 2：**
>
> ```
> 输入：root1 = [1], root2 = [1,2]
> 输出：[2,2]
> ```

### DFS-递归

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_13_iShot_2023-06-13_10.35.17.gif" alt="iShot_2023-06-13_10.35.17" style="zoom:67%;" />

- 时间复杂度：$O(min(m,n))$，其中 m 和 n 分别是两个二叉树的节点个数。对两个二叉树同时进行深度优先搜索，只有当两个二叉树的对应节点都不为空时才会对该结点进行显性合并操作，因此被访问到的节点数不会超过较小的二叉树的节点数。
- 空间复杂度：$O(min(m,n))$，其中 m 和 n 分别是两个二叉树的节点个数。空间复杂度取决于递归调用的层数，递归调用的层数不会超过较小的最大高度，最坏情况下，二叉树的高度等于节点数。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function mergeTrees(root1: TreeNode | null, root2: TreeNode | null): TreeNode | null {
    if (root1 === null && root2 === null) return null;
  	if (root1 === null) return root2;
  	if (root2 === null) return root1;
    let root: TreeNode = new TreeNode(root1.val + root2.val);
    root.left = mergeTrees(root1.left, root2.left);
    root.right = mergeTrees(root1.right, root2.right);
    return root;
};
```

### BFS-迭代

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_13_iShot_2023-06-13_10.48.15.gif" alt="iShot_2023-06-13_10.48.15" style="zoom:67%;" />

- 时间复杂度：$O(min(m,n))$，其中 m 和 n 分别是两个二叉树的节点个数。对两个二叉树同时进行广度优先搜索，只有当两个二叉树的对应节点都不为空时才会访问到该节点，因此被访问到的节点数不会超过较小的二叉树的节点数。
- 空间复杂度：$O(min(m,n))$，其中 m 和 n 分别是两个二叉树的节点个数。空间复杂度取决于队列中元素个数，队列中的元素个数不会超过较小的二叉树的节点数。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function mergeTrees(root1: TreeNode | null, root2: TreeNode | null): TreeNode | null {
    if (root1 === null) return root2;
    if (root2 === null) return root1;
    const root = new TreeNode(root1.val + root2.val);
    const queue: TreeNode[] = [root];
    const queue1: TreeNode[] = [root1];
    const queue2: TreeNode[] = [root2];
    while (queue.length > 0) {
        const node = queue.shift();
        const node1 = queue1.shift();
        const node2 = queue2.shift();
        if (node1.left !== null && node2.left !== null) {
            const merge = new TreeNode(node1.left.val + node2.left.val);
            node.left = merge;
            queue.push(merge);
            queue1.push(node1.left);
            queue2.push(node2.left);
        } else if (node1.left === null) {
            node.left = node2.left;
        } else if (node2.left === null) {
            node.left = node1.left;
        }
        if (node1.right !== null && node2.right !== null) {
            const merge = new TreeNode(node1.right.val + node2.right.val);
            node.right = merge;
            queue.push(merge);
            queue1.push(node1.right);
            queue2.push(node2.right);
        }
        else if (node1.right === null) {
            node.right = node2.right;
        } else if (node2.right === null) {
            node.right = node1.right;
        }
    }
    return root;
};
```



## 700.二叉搜索树中的搜索

> 给定二叉搜索树（BST）的根节点 `root` 和一个整数值 `val`。
>
> 你需要在 BST 中找到节点值等于 `val` 的节点。 返回以该节点为根的子树。 如果节点不存在，则返回 `null` 。
>
> **示例 1:**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_13_tree1.jpg" alt="img" style="zoom:80%;float:left" />
>
> ```
> 输入：root = [4,2,7,1,3], val = 2
> 输出：[2,1,3]
> ```
>
> **示例 2:**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_13_tree2.jpg" alt="img" style="zoom:80%;float:left;" />
>
> ```
> 输入：root = [4,2,7,1,3], val = 5
> 输出：[]
> ```

### DFS-递归

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function searchBST(root: TreeNode | null, val: number): TreeNode | null {
    if (root === null) return null;
    if (root.val === val) return root;
    else if (root.val > val) return searchBST(root.left, val);
    else return searchBST(root.right, val);
};
```

### BFS-迭代

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function searchBST(root: TreeNode | null, val: number): TreeNode | null {
    const queue: TreeNode[] = [root];
    while (queue.length > 0) {
        const node = queue.shift();
        if (node === null) return null;
        if (node.val === val) return node;
        else if (node.val > val) queue.push(node.left);
        else queue.push(node.right);
    }
};
```



## 98.验证二叉搜索树

> 给你一个二叉树的根节点 `root` ，判断其是否是一个有效的二叉搜索树。
>
> **有效** 二叉搜索树定义如下：
>
> - 节点的左子树只包含 **小于** 当前节点的数。
> - 节点的右子树只包含 **大于** 当前节点的数。
> - 所有左子树和右子树自身必须也是二叉搜索树。
>
> **示例 1：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_13_tree1-20230613152354659.jpg" alt="img" style="zoom:80%;float:left;" />
>
> ```
> 输入：root = [2,1,3]
> 输出：true
> ```
>
> **示例 2：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_13_tree2-20230613152424111.jpg" alt="img" style="zoom:80%;float:left;" />
>
> ```
> 输入：root = [5,1,4,null,null,3,6]
> 输出：false
> 解释：根节点的值是 5 ，但是右子节点的值是 4 。
> ```

### 递归

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_13_iShot_2023-06-13_15.25.49.gif" alt="iShot_2023-06-13_15.25.49" style="zoom:89%;" />

- 时间复杂度：$O(n)$，其中 n 为二叉树的节点个数。在递归调用的时候二叉树的每个节点最多被访问一次，因此时间复杂度为 $O(n)$。
- 空间复杂度：$O(n)$，其中 n 为二叉树的节点个数。递归函数在递归过程中需要为每一层递归函数分配栈空间，所以这里需要额外的空间且该空间取决于递归的深度，即二叉树的深度。最坏情况下二叉树为一条链，树的高度为 n，递归最深达到 n 层，故最坏情况下空间复杂度为 $O(n)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function helper(root: TreeNode | null, low: number, upper: number) {
    if (root === null) return true;
    if (root.val <= low || root.val >= upper) {
        return false;
    }
    return helper(root.left, low, root.val) && helper(root.right, root.val, upper);
}

function isValidBST(root: TreeNode | null): boolean {
    return helper(root, -Infinity, Infinity);
};
```

### 中序遍历

思路：利用二叉搜索树中序遍历（递归）为递增序列的特点，如果不是递增序列则返回false，否则返回true。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_13_image-20230613164939938.png" alt="image-20230613164939938" style="zoom:33%;" />

- 时间复杂度：$O(n)$。
- 空间复杂度：$O(n)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function isValidBST(root: TreeNode | null): boolean {
    let pre = -Infinity;
    const helper = (root: TreeNode | null): boolean => {
        if (root === null) return true;
        if (!helper(root.left)) {
            return false;
        }
        if (root.val <= pre) {
            return false;
        }
        pre = root.val;
        return helper(root.right);
    }
    return helper(root);
};
```



## 530.二叉搜索树的最小绝对差

> 给你一个二叉搜索树的根节点 `root` ，返回 **树中任意两不同节点值之间的最小差值** 。
>
> 差值是一个正数，其数值等于两值之差的绝对值。
>
> **示例 1：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_14_bst1.jpg" alt="img" style="zoom:80%;" /> 
>
> ```
> 输入：root = [4,2,6,1,3]
> 输出：1
> ```
>
> **示例 2：**
>
> <img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_14_bst2.jpg" alt="img" style="zoom:80%;" /> 
>
> ```
> 输入：root = [1,0,48,null,null,12,49]
> 输出：1
> ```

### 中序遍历+递归

思路：通过中序遍历的方法，可以获得一个升序的节点值序列，这是因为二叉搜索树的性质是左子树的值 < 根节点的值 < 右子树的值。我们可以在遍历的过程中，比较相邻节点的差值，并记录下最小的差值。

- 时间复杂度：$O(n)$，其中 n 为二叉搜索树节点的个数。每个节点的中序遍历中都会被访问一次且只会被访问一次，因此总时间复杂度为 $O(n)$。
- 空间复杂度：$O(n)$。递归函数的空间复杂度取决于递归的栈深度，而栈深度在二叉搜索树为一条链的情况下会达到 $O(n)$级别。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function getMinimumDifference(root: TreeNode | null): number {
    let min = Infinity;
    let pre: number = null;
    const helper = (root: TreeNode | null) => {
        if (root === null) return;
        if (root.left) {
            helper(root.left);
        }
        if (pre !== null) {
            min = Math.min(Math.abs(pre - root.val), min);
        }
        pre = root.val;
        if (root.right) {
            helper(root.right);
        }
    }
    helper(root);
    return min;
};
```



## 501.二叉搜索树中的众数

> 给你一个含重复值的二叉搜索树（BST）的根节点 `root` ，找出并返回 BST 中的所有 [众数](https://baike.baidu.com/item/众数/44796)（即，出现频率最高的元素）。
>
> 如果树中有不止一个众数，可以按 **任意顺序** 返回。
>
> 假定 BST 满足如下定义：
>
> - 结点左子树中所含节点的值 **小于等于** 当前节点的值
> - 结点右子树中所含节点的值 **大于等于** 当前节点的值
> - 左子树和右子树都是二叉搜索树
>
> **示例 1：**
>
> ![img](https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_14_mode-tree.jpg) 
>
> ```
> 输入：root = [1,null,2,2]
> 输出：[2]
> ```
>
> **示例 2：**
>
> ```
> 输入：root = [0]
> 输出：[0]
> ```

### 中序遍历+递归

思路：对二叉搜索树进行中序遍历，这样可以得到一个**递增的序列**。然后，我们可以在遍历的过程中记录当前元素的出现次数和最大出现次数，并用一个列表保存出现次数最多的元素。如果当前元素的出现次数超过了之前的最大出现次数，就更新这个列表。这样，当遍历结束时，我们就可以得到出现次数最多的元素。

<img src="https://images-1256612942.cos.ap-guangzhou.myqcloud.com/2023_06_14_1600915764-mCBgBA-501.%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E4%B8%AD%E7%9A%84%E4%BC%97%E6%95%B01.png" alt="501.二叉搜索树中的众数1.png" style="zoom:33%;" />

- 时间复杂度：$O(n)$。
- 空间复杂度：$O(n)$。

```typescript
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function findMode(root: TreeNode | null): number[] {
    let arr: number[] = [];
    let count = 0;
    let maxCount = 0;
    let pre = root !== null ? root.val : null;
    const helper = (root: TreeNode | null) => {
        if (root === null) return;
        if (root.left) {
            helper(root.left);
        }
        if (pre === root.val) {
            count++;
        } else {
            count = 1;
        }
        if (count > maxCount) {
            arr = [];
            arr.push(root.val);
            maxCount = count;
        } else if (count === maxCount) {
            arr.push(root.val);
        }
        pre = root.val;
        if (root.right) {
            helper(root.right);
        }
    }
    helper(root);
    return arr;
};
```



## 236.二叉树的最近公共祖先

> 给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

# 回溯法









# 贪心算法















# 动态规划







