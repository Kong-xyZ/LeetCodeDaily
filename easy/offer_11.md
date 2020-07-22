# 167. 两数之和 II - 输入有序数组

给定一个已按照 **升序排列** 的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 `index1` 和 `index2`，其中 `index1` 必须小于 `index2`。

**说明：**  

* 返回的下标值（`index1` 和 `index2`）不是从零开始的。
* 你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

**示例:**  
>**输入:** numbers = [2, 7, 11, 15], target = 9  
>**输出:** [1,2]  
>**解释:** 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。  

---
**解法一：二分查找**  
思路：  

1. 初始化左和右；
2. 如果左小于右则循环：
3. 中间等于左和右的平均索引：
4. 如果中间和右边的值一样：移动左；
5. 如果中间大于右：左等于中间的下一个；
6. 如果右大于中间：右等于中间的下一个。
7. 最后返回左对应的值。

```Java
class Solution {
    public int minArray(int[] numbers) {
        int len = numbers.length;
        // 首先判断旋转数组是否本身有序
        if (numbers[0] < numbers[len - 1]) return numbers[0];  // 本身有序
        // 如果真的发生了旋转
        int left = 0;
        int right = len - 1;
        while (left < right) {
            int mid = left + (right - left) / 2;
            // 如果找到最小值，则返回
            // 最小值的特点为，它比前一个数要小
            if (mid > 0 && numbers[mid] < numbers[mid - 1]) return numbers[mid];
            // 此时有下面几种情况：
            // 1. 3 4 5 6 7 8 9 1 2 在前半部分，特点为 mid 处元素 > 最后一个元素
            // 2. 8 9 1 2 3 4 5 6 7 在后半部分，特点为 mid 处元素 < 最后一个元素
            // 当mid 处元素 == 最后一个元素时，无法确定最小值在哪一边，例如：
            // 3, 3, 3, 1, 3 和 3, 1, 3, 3, 3 此时right-1，缩小范围直到可以确定
            // 以上面的特点为切入点，进行二分查找
            if (numbers[mid] < numbers[right]) {
                right = mid;
            } else if (numbers[mid] > numbers[right]) {
                left = mid + 1;
            } else {
                right -= 1;
            }
        }
        return numbers[left];
    }
}
```

**复杂度分析：**  

* 时间复杂度：$O(\log n)$，其中 $n$ 是数组 $\it numbers$ 的长度。如果数组是随机生成的，那么数组中包含相同元素的概率很低，在二分查找的过程中，大部分情况都会忽略一半的区间。而在最坏情况下，如果数组中的元素完全相同，那么 `while` 循环就需要执行 $n$ 次，每次忽略区间的右端点，时间复杂度为 $O(n)$。
* 空间复杂度：$O(1)$，我们只需要常数空间存放若干变量。
