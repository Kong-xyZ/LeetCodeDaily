# 剑指 Offer 09. 用两个栈实现队列

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 `appendTail` 和 `deleteHead` ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，`deleteHead` 操作返回 `-1` )

**示例1:**  
>**输入:**  
>["CQueue","appendTail","deleteHead","deleteHead"]  
>[[],[3],[],[]]  
>**输出:** [null,null,3,-1]  

**示例2:**  
>**输入:**  
>["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]  
>[[],[],[5],[2],[],[]]  
>**输出:** [null,-1,null,null,5,2]  

**提示:**

1. `1 <= values <= 10000`
2. 最多会对 `appendTail、deleteHead` 进行 `10000` 次调用

---
**解法一：**  
思路：  

* 加入队尾 `appendTail()` 函数： 将数字 `val` 加入栈 `A` 即可。
* 删除队首 `deleteHead()` 函数： 有以下三种情况。
    1. 当栈 `B` 不为空： `B` 中仍有已完成倒序的元素，因此直接返回 `B` 的栈顶元素。
    2. 否则，当 `A` 为空： 即两个栈都为空，无元素，因此返回 `-1` 。
    3. 否则：将栈 `A` 元素全部转移至栈 `B` 中，实现元素倒序，并返回栈 `B` 的栈顶元素。

```Java
class CQueue {

    private Stack<Integer> head;
    private Stack<Integer> foot;

    public CQueue() {
        head = new Stack<>();
        foot = new Stack<>();
    }

    public void appendTail(int value) {
        head.push(value);
    }

    public int deleteHead() {
        if (!foot.isEmpty()) {
            return foot.pop();
        } else {
            while (!head.isEmpty()) {
                foot.push(head.pop());
            }
            return foot.isEmpty() ? -1 : foot.pop();
        }
    }
}
```

**复杂度分析：**  

* 时间复杂度：$O(1)$，对于插入和删除操作，时间复杂度均为 $O(1)$。插入不多说，对于删除操作，虽然看起来是 $O(n)$ 的时间复杂度，但是仔细考虑下每个元素只会「至多被插入和弹出 `foot` 一次」，因此均摊下来每个元素被删除的时间复杂度仍为 $O(1)$。
* 空间复杂度：$O(n)$，需要使用两个栈存储已有的元素。
