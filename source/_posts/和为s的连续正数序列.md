---
title: 剑指Offer:和为s的连续正数序列
date: 2020-03-02 20:23:43
tags: [剑指Offer,python,算法,滑动窗口]
categories: [剑指Offer]
---

<img src="http://lishengyu.xyz/pubgm/IMG_5372.JPG" >

## 剑指Offer 
### 面试题57 - II. 和为s的连续正数序列
输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

**Easy**
 

**示例 1：**

```
输入：target = 9
输出：[[2,3,4],[4,5]]
```

**示例 2：**

```
输入：target = 15
输出：[[1,2,3,4,5],[4,5,6],[7,8]]
```
 
**限制：**

- 1 <= target <= 10^5

### 思路
这道题说的是连续的数，就很简单了，如果不连续，就难了。这根题方法是[滑动窗口法](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/solution/shi-yao-shi-hua-dong-chuang-kou-yi-ji-ru-he-yong-h/):

![](http://lishengyu.xyz/leetcode/571.png)

![](http://lishengyu.xyz/leetcode/572.png)

![](http://lishengyu.xyz/leetcode/573.png)

```python
class Solution:
    def findContinuousSequence(self, target: int) -> List[List[int]]:
        r=[]
        for i in range(1,(target//2)+1):
            sum=i
            a=[i]
            for j in range(i+1,(target//2)+2):
                if sum<target:
                    sum=sum+j
                    a.append(j)
                if sum==target:
                    r.append(a)
                    break
                if sum>target:
                    break
        return r

```