---
title: leetcode_453
date: 2021-10-20 15:50:11
tags: [数组]

---

#### [453. 最小操作次数使数组元素相等](https://leetcode-cn.com/problems/minimum-moves-to-equal-array-elements/)

给你一个长度为 `n` 的整数数组，每次操作将会使 `n - 1` 个元素增加 `1` 。返回让数组所有元素相等的最小操作次数。

**示例 1：**

```
输入：nums = [1,2,3]
输出：3
解释：
只需要3次操作（注意每次操作会增加两个元素的值）：
[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]

```

**示例 2：**

```
输入：nums = [1,1,1]
输出：0
```

```

```

解析

每一步除了最大的那个数不加1  相等于最大的数减1 参考相对运动理解

每一次操作总和都会-1

那么最后的结果肯定是n个最小数

那么

```
return sum - min * n;
```

即可得到结果

利用for each语句遍历数组

找出数组里面最小的数和总和sum

```java
for (int i : nums) {
            min = Math.min(min, i);
            sum += i;
        }
```

题解

```java
class Solution {
    public int minMoves(int[] nums) {
        int n = nums.length;
        int min = nums[0], sum = 0;
        for (int i : nums) {
            min = Math.min(min, i);
            sum += i;
        }
        return sum - min * n;
    }
}
```

