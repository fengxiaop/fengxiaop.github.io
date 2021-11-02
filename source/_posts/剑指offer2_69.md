---
title: leetcode_剑指offer2 69
date: 2021-10-14 10:41:04
tags: leetcode
---

#### [剑指 Offer II 069. 山峰数组的顶部](https://leetcode-cn.com/problems/B1IidL/)

题目

```
符合下列属性的数组 arr 称为 山峰数组（山脉数组） ：

arr.length >= 3
存在 i（0 < i < arr.length - 1）使得：
arr[0] < arr[1] < ... arr[i-1] < arr[i]
arr[i] > arr[i+1] > ... > arr[arr.length - 1]
给定由整数组成的山峰数组 arr ，返回任何满足 arr[0] < arr[1] < ... arr[i - 1] < arr[i] > arr[i + 1] > ... > arr[arr.length - 1] 的下标 i ，即山峰顶部。

 

示例 1：

输入：arr = [0,1,0]
输出：1
示例 2：

输入：arr = [1,3,5,4,2]
输出：2
示例 3：

输入：arr = [0,10,5,2]
输出：1
示例 4：

输入：arr = [3,4,5,1]
输出：2
示例 5：

输入：arr = [24,69,100,99,79,78,67,36,26,19]
输出：2
 

提示：

3 <= arr.length <= 104
0 <= arr[i] <= 106
题目数据保证 arr 是一个山脉数组
 

进阶：很容易想到时间复杂度 O(n) 的解决方案，你可以设计一个 O(log(n)) 的解决方案吗？
```

我写的想法 第一次就想到for循环遍历  写出了O（n）的学法

```java
int peakIndexInMountainArray(int* arr, int arrSize){
    int temp=0;
    for(;temp<arrSize-1;temp++){
        if(arr[temp]>arr[temp+1])
        break;
    }
    return temp;
}
```

三叶姐姐的解法

二分
往常我们使用「二分」进行查值，需要确保序列本身满足「二段性」：当选定一个端点（基准值）后，结合「一段满足 & 另一段不满足」的特性来实现“折半”的查找效果。

但本题求的是峰顶索引值，如果我们选定数组头部或者尾部元素，其实无法根据大小关系“直接”将数组分成两段。

但可以利用题目发现如下性质：由于 arr 数值各不相同，因此峰顶元素左侧必然满足严格单调递增，峰顶元素右侧必然不满足。

因此 以峰顶元素为分割点的 arr 数组，根据与 前一元素/后一元素 的大小关系，具有二段性：

峰顶元素左侧满足 arr[i-1] < arr[i]arr[i−1]<arr[i] 性质，右侧不满足
峰顶元素右侧满足 arr[i] > arr[i+1]arr[i]>arr[i+1] 性质，左侧不满足
因此我们可以选择任意条件，写出若干「二分」版本。

代码：

```java
class Solution {
    // 根据 arr[i-1] < arr[i] 在 [1,n-1] 范围内找值
    // 峰顶元素为符合条件的最靠近中心的元素
    public int peakIndexInMountainArray(int[] arr) {
        int n = arr.length;
        int l = 1, r = n - 1;
        while (l < r) {
            int mid = l + r + 1 >> 1;
            if (arr[mid - 1] < arr[mid]) l = mid;
            else r = mid - 1;
        }
        return r;
    }
}
```

- 时间复杂度：O(\log{n})*O*(log*n*)

- 空间复杂度：O(1)*O*(1)

- 三分和k分

- ```java
  class Solution {
      public int peakIndexInMountainArray(int[] arr) {
          int n = arr.length;
          int l = 0, r = n - 1;
          while (l < r) {
              int m1 = l + (r - l) / 3;
              int m2 = r - (r - l) / 3;
              if (arr[m1] > arr[m2]) r = m2 - 1;
              else l = m1 + 1;
          }
          return r;
      }
  }
  
  作者：AC_OIer
  链接：https://leetcode-cn.com/problems/B1IidL/solution/gong-shui-san-xie-er-fen-san-fen-ji-zhi-lc8zl/
  来源：力扣（LeetCode）
  著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
  ```

  

