# 面试题29. 顺时针打印矩阵

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

**示例1:**  
>**输入：** matrix = [[1,2,3],[4,5,6],[7,8,9]]  
>**输出：** [1,2,3,6,9,8,7,4,5]  

**示例2:**  
>**输入：** matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]  
>**输出：** [1,2,3,4,8,12,11,10,9,5,6,7]

**进阶：**  

* `0 <= matrix.length <= 100`
* `0 <= matrix[i].length <= 100`

---
**解法一：**  
思路：  

* 从左到右遍历上侧元素，依次为 $(\textit{top}, \textit{left})$ 到 $(\textit{top}, \textit{right})$。

* 从上到下遍历右侧元素，依次为 $(\textit{top} + 1, \textit{right})$ 到 $(\textit{bottom}, \textit{right})$。

* 如果 $\textit{left} < \textit{right}$ 且 $\textit{top} < \textit{bottom}$，则从右到左遍历下侧元素，依次为 $(\textit{bottom}, \textit{right} - 1)$ 到 $(\textit{bottom}, \textit{left} + 1)$，以及从下到上遍历左侧元素，依次为 $(\textit{bottom}, \textit{left})$ 到 $(\textit{top} + 1, \textit{left})$。

```Java
class Solution {
    public int[] spiralOrder(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return new int[0];
        }
        int row = matrix.length;
        int col = matrix[0].length;
        int[] printArray = new int[row * col];
        int left = 0, right = col - 1, top = 0, bottom = row - 1, x = 0;
        while (true) {
            for (int i = left; i <= right; i++) {
                // left to right.
                printArray[x++] = matrix[top][i];
            }
            if (++top > bottom) {
                break;
            }
            for (int i = top; i <= bottom; i++) {
                // top to bottom.
                printArray[x++] = matrix[i][right];
            }
            if (left > --right) {
                break;
            }
            for (int i = right; i >= left; i--) {
                // right to left.
                printArray[x++] = matrix[bottom][i];
            }
            if (top > --bottom) {
                break;
            }
            for (int i = bottom; i >= top; i--) {
                // bottom to top.
                printArray[x++] = matrix[i][left];
            }
            if (++left > right) {
                break;
            }
        }
        return printArray;
    }
}
```

**复杂度分析：**  

* 时间复杂度：$O(MN)$，其中 $m$ 和 $n$ 分别是输入矩阵的行数和列数。矩阵中的每个元素都要被访问一次。
* 空间复杂度：$O(1)$，除了输出数组以外，空间复杂度是常数。
