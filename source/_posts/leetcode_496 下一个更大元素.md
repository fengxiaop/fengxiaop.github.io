---
layout: leetcode_496
title: 下一个更大元素
date: 2021-10-26 22:02:43
tags: leetcode
---

#### [496. 下一个更大元素 I](https://leetcode-cn.com/problems/next-greater-element-i/)

难度 :简单

```
给你两个 没有重复元素 的数组 nums1 和 nums2 ，其中nums1 是 nums2 的子集。

请你找出 nums1 中每个元素在 nums2 中的下一个比其大的值。

nums1 中数字 x 的下一个更大元素是指 x 在 nums2 中对应位置的右边的第一个比 x 大的元素。如果不存在，对应位置输出 -1 。
```

**示例 1:**

```
输入: nums1 = [4,1,2], nums2 = [1,3,4,2].
输出: [-1,3,-1]
解释:
    对于 num1 中的数字 4 ，你无法在第二个数组中找到下一个更大的数字，因此输出 -1 。
    对于 num1 中的数字 1 ，第二个数组中数字1右边的下一个较大数字是 3 。
    对于 num1 中的数字 2 ，第二个数组中没有下一个更大的数字，因此输出 -1 。
```

**示例 2:**

```
输入: nums1 = [2,4], nums2 = [1,2,3,4].
输出: [3,-1]
解释:
    对于 num1 中的数字 2 ，第二个数组中的下一个较大数字是 3 。
    对于 num1 中的数字 4 ，第二个数组中没有下一个更大的数字，因此输出 -1 。

```

提示：

```
1 <= nums1.length <= nums2.length <= 1000
0 <= nums1[i], nums2[i] <= 104
nums1和nums2中所有整数 互不相同
nums1 中的所有整数同样出现在 nums2 中
```

看到题目第一时间就想的遍历然后匹配  虽然写的很垃圾  但是是自己独立debug写出来的还是很高兴

#### **方法一 ：暴力**

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        int n = nums1.length;
        int nums3[] = new int[n];
        for(int i = 0 ; i < n ; i++ )
            for(int j = 0 ; j < nums2.length ; j++ )
                if(nums1[i] == nums2[j])
                    for(int k = j;k<nums2.length;k++)
                        if( nums2[k] > nums1[i])
                          {
                          nums3[i] = nums2[k];
                          break;
                          }
                        else
                          nums3[i] = -1;
    return nums3;
    }
}
```

有几个地方需要注意  就是当遇见一个数比他大的时候 需要赋值后立即跳出 

官方题解

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        int m = nums1.length, n = nums2.length;
        int[] res = new int[m];
        for (int i = 0; i < m; ++i) {
            int j = 0;
            while (j < n && nums2[j] != nums1[i]) {
                ++j;
            }
            int k = j + 1;
            while (k < n && nums2[k] < nums2[j]) {
                ++k;
            }
            res[i] = k < n ? nums2[k] : -1;
        }
        return res;
    }
}
```

不得不感叹一下 同样是暴力遍历 官方写的比我写的好得多

#### 方法二：单调栈 + 哈希表

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        Deque<Integer> stack = new ArrayDeque<Integer>();
        for (int i = nums2.length - 1; i >= 0; --i) {
            int num = nums2[i];
            while (!stack.isEmpty() && num >= stack.peek()) {
                stack.pop();
            }
            map.put(num, stack.isEmpty() ? -1 : stack.peek());
            stack.push(num);
        }
        int[] res = new int[nums1.length];
        for (int i = 0; i < nums1.length; ++i) {
            res[i] = map.get(nums1[i]);
        }
        return res;
    }
}
```

三叶姐题解

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        int n = nums1.length, m = nums2.length;
        Deque<Integer> d = new ArrayDeque<>();
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = m - 1; i >= 0; i--) {
            int x = nums2[i];
            while (!d.isEmpty() && d.peekLast() <= x) d.pollLast();
            map.put(x, d.isEmpty() ? -1 : d.peekLast());
            d.addLast(x);
        }
        int[] ans = new int[n];
        for (int i = 0; i < n; i++) ans[i] = map.get(nums1[i]);
        return ans;
    }
}
```

