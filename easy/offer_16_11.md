# 面试题 16.11. 跳水板

你正在使用一堆木板建造跳水板。有两种类型的木板，其中长度较短的木板长度为 `shorter`，长度较长的木板长度为 `longer`。你必须正好使用k块木板。编写一个方法，生成跳水板所有可能的长度。

返回的长度需要从小到大排列。

**说明：** m 和 n 的值均不超过 100。

**示例1:**  
>**输入:**  
>shorter = 1  
>longer = 2  
>k = 3  
>**输出:** {3,4,5,6}  

**提示:**  

* `0 < shorter <= longer`
* `0 <= k <= 100000`

---
**解法一：数学**  
思路：  

由于三个变量的取值范围，考虑到两种特殊情况

1. 当 $k$ 为 $0$ 时，返回一个空数组；
2. 当 `shorter` 和 `longer` 相等时，返回 $\text{shorter}*k$ 即可；
3. 最后就是通常情况了，根据数学归纳法，$2$ 种长度板子，必须用 $k$ 块，不同的情况共 $k+1$ 中，公式为 $(k - i)*\text{shorter}+i*\text{longer}$

```Java
class Solution {
    public int[] divingBoard(int shorter, int longer, int k) {
        if (k == 0) {
            return new int[0];
        }
        if (shorter == longer) {
            return new int[]{shorter * k};
        }
        int[] lengths = new int[k + 1];
        for (int i = 0; i <= k; i++) {
            lengths[i] = shorter * (k - i) + longer * i;
        }
        return lengths;
    }
}
```

**复杂度分析：**  

* 时间复杂度：$O(k)$，其中 $k$ 是木板数量。短木板和长木板一共使用 $k$ 块，一共有 $k+1$ 种组合，对于每种组合都要计算跳水板的长度。
* 空间复杂度：$O(1)$，除了返回值以外，额外使用的空间复杂度为常数。
