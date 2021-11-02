---
title: ArrayList与Hashset的区别.md
date: 2021-11-01 22:53:09
tags: leetcode
---

<h1>ArrayList与Hashset



Hashset 具有去重的功能 利用size()方法可以得到里面元素的种类

ArrayList是有序的  元素可以重复

HashSet是无序不重复的

#### [575. 分糖果](https://leetcode-cn.com/problems/distribute-candies/)

```java
class Solution {
    public int distributeCandies(int[] candyType) {
        Set<Integer> set = new HashSet<>();
        for (int i : candyType) set.add(i);
        return Math.min(candyType.length / 2, set.size());
    }
}
```

利用set去重,再用set.size()得到糖果的种类

创建ArrayList表

`ArrayList<E> arraylist = new ArrayList();`

利用add方法可以给ArrayList增加元素

数组排序方法

`Arrays.sort(arr)`

arr代表着数组

若s是字符串 则用s.length()获取字符串长度。

若s是数组 则用s.length获取数组的长度。

