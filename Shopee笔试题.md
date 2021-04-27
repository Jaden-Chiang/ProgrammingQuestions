

# Shopee笔试题&JZ13

## Question

==i)==. 输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分。

------

## Solution

We could use two pointers `p1` and `p2`. `p1` traverses the array from front to back, and `p2` traverses the array from back to front. During the traversing, if the `p1` points to an odd, then points to next number until it points to an even. `p2` is opposite to `p1`, it move forward until points to an odd. When `p1` points to an even and `p2` points to an odd, change their value until `p1` meets `p2`.

#### Own Code

```java
    public static int[] AdjustOrder(int[] arr) {
        int p1 = 0;// p1指针从前向后遍历
        int p2 = arr.length - 1;// p2指针从后向前遍历
        while (p1 < p2) {

            // 如果p1指针指向的数是奇数，则继续向后移动
            while (p1 < p2 && arr[p1] % 2 == 1) {
                p1++;
            }
            // 如果p2指针指向的数是偶数，则继续向前移动
            while (p1 < p2 && arr[p2] % 2 == 0) {
                p2--;
            }

            // 如果p1指向偶数，p2指向奇数，交换两者的值
            if (p1 < p2) {
                int temp = arr[p1];
                arr[p1] = arr[p2];
                arr[p2] = temp;
            }
        }
        return arr;
    }
```



------

==ii)==. 与上方要求相同，但是增加一条要求：不能更改奇数和偶数的位置

------

## Solution

In this time, we couldn't use two pointers again. We need to record the order of odd and even numbers. In this question, I create a new array `res` with the same length of the array given to store result and an arraylist to record even numbers. Traverse the array from head to tail. If there is an odd number, store it to `res` directly, and if traverse to an even number, store it to arraylist. At last, copy all the elements of arraylist to tail of `res`, and we can get answer.

#### Own Code

```java
import java.util.*;

public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param array int整型一维数组 
     * @return int整型一维数组
     */
    public int[] reOrderArray (int[] array) {
        int len = array.length;
        int[] res = new int[len];
        int pos = 0; // 记录res中的元素位置
        List<Integer> list = new ArrayList<>();
        
        for (int i = 0; i < len; i++) {
            // 如果是奇数，则直接存入数组
            if (array[i] % 2 == 1) {
                res[pos] = array[i];
                pos++;
            }else {
                list.add(array[i]);
            }
        }
        
        for (int i = 0; i < list.size(); i++) {
            res[pos] = list.get(i);
            pos++;
        }
        
        return res;
    }
}
```

