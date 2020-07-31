# 面试题 08.03. 魔术索引

魔术索引。 在数组 `A[0...n-1]` 中，有所谓的魔术索引，满足条件 `A[i] = i`。给定一个有序整数数组，编写一种方法找出魔术索引，若有的话，在数组 `A` 中找出一个魔术索引，如果没有，则返回 `-1`。若有多个魔术索引，返回索引值最小的一个。

**示例1:**  
>**输入：** nums = [0, 2, 3, 4, 5]  
>**输出：** 0  
>**解释：** 0 下标的元素为 0

**示例2:**  
>**输入：** nums = [1, 1, 1]  
>**输出：** 1  

**提示:**

1. `nums` 长度在 `[1, 1000000]` 之间

---
**解法一：**  
思路：  

准备一个函数 `helper(nums,left,right)`,这个函数求 `nums[left...right]`区间范围内第一个符合条件的值（值与索引相等时返回），没有符合的值时，返回 $-1$,

**一个前提：** 数组是有序的，从左到右是上升的

* 每次优先搜索 `[left...mid-1]` 部分，如果这部分的返回值不为 $−1$,返回这个值即可（注意 `helper` 函数的定义），如果这个值为 $-1$，说明 `[left...mid-1]` 部分没有符合条件的值，判断下 `nums[mid]` 与 `mid` 的值是否相等，相等则返回，不相等则进入下一步
* 搜索 `[mid+1...right]` ,逻辑和搜索左半部分的逻辑相同，在这个大区间上分出左右部分

```Java
class Solution {
    public int findMagicIndex(int[] nums) {
        return getAnswer(nums, 0, nums.length - 1);
    }

    public int getAnswer(int[] nums, int left, int right) {
        if (left > right) {
            return -1;
        }
        int mid = (right - left) / 2 + left;
        int leftAnswer = getAnswer(nums, left, mid - 1);
        if (leftAnswer != -1) {}
            return leftAnswer;
        } else if (nums[mid] == mid) {}
            return mid;
        }
        return getAnswer(nums, mid + 1, right);
    }
}
```

**复杂度分析：**  

* 时间复杂度：$O(n)$，最坏情况下会达到 $O(n)$ 的时间复杂度，其中 $n$ 为数组的长度。。
* 空间复杂度：$O(n)$，递归函数的空间取决于调用的栈深度，而最坏情况下我们会递归 $n$ 层，即栈深度为 $O(n)$，因此空间复杂度最坏情况下为 $O(n)$。
