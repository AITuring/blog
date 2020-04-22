---
title: leetcode 908 Smallest Range I
date: 2019-09-04 23:59:43
tags: [leetcode,java,python,算法]
categories: [leetcode]
---

![](http://lishengyu.xyz/j201.jpg)
## leetcode 908 Smallest Range I
### Easy
### 题目：
Given an array A of integers, for each integer A[i] we may choose any x with `-K <= x <= K`, and add x to A[i].

After this process, we have some array B.

Return the smallest possible difference between the maximum value of B and the minimum value of B.

 
```
Example 1:

Input: A = [1], K = 0
Output: 0
Explanation: B = [1]
```
```
Example 2:

Input: A = [0,10], K = 2
Output: 6
Explanation: B = [2,8]
```
```
Example 3:

Input: A = [1,3,6], K = 3
Output: 0
Explanation: B = [3,3,3] or B = [4,4,4]
``` 

Note:
```
1 <= A.length <= 10000
0 <= A[i] <= 10000
0 <= K <= 10000
```
### 思路
思路很简单，就是先找到数组中的最大值与最小值，然后最小值加K，最大值减k，如果现在最大值还比最小值大，那最小差就是它俩差。如果最小值等于或者大于最大值，那他们最小差就是0.
下面是代码：
```java
class Solution {
    public int smallestRangeI(int[] A, int K) {
        
        int min=A[0];
        int max=A[0];
        for(int i=0;i<A.length;++i)
        {
            if(A[i]>=max)
                max=A[i];
            if(A[i]<=min)
                min=A[i];
        }
        min=min+K;
        max=max-K;
        if(max>min)
            return max-min;
        else
            return 0;
        
        
    }
}

```

```python
class Solution:
    def smallestRangeI(self, A: List[int], K: int) -> int:
        return max(0,max(A)-min(A)-2*K)
        
```