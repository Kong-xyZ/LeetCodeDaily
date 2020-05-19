# 冒泡排序

> 基本思想: 冒泡排序，类似于水中冒泡，较大的数沉下去，较小的数慢慢冒起来，假设从小到大，即为较大的数慢慢往后排，较小的数慢慢往前排。

**算法原理:**

1. 比较相邻的元素。如果第一个比第二个大，就交换他们两个。  
2. 对每一对相邻元素做同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数。  
3. 针对所有的元素重复以上的步骤，除了最后一个。  
4. 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。  

**代码实现:**

```Java  
    public class BubbleSort {
        public static void main(String[] args) {
            int[] nums = {8, 55, 325, 2, 132, 95, 11, 66, 0};
            bubbleSort(nums);
            System.out.println(Arrays.toString(nums));
        }

        public static void bubbleSort(int[] nums) {
            int len = nums.length - 1;
            for (int i = 0; i < len; i++) {
                for (int j = 0; j < len - i; j++) {
                    if (nums[j] > nums[j + 1]) {
                        int temp = nums[j];
                        nums[j] = nums[j + 1];
                        nums[j + 1] = temp;
                    }
                }
            }
        }
    }
```

**性能分析：**  

 | 算法  | 最好时间 | 最坏时间 | 平均时间 | 额外空间 | 稳定性 |
 | :---: | :------: | :------: | :------: | :------: | :----: |
 | 冒泡  |  $O(n)$  | $O(n^2)$ | $O(n^2)$ |   $1$    |  稳定  |
