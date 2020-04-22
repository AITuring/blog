---
title: leetcode 121 Best Time to Buy and Sell Stock
date: 2019-10-09 23:57:43
tags: [leetcode,C++,算法]
categories: [leetcode]
---

![](http://lishengyu.xyz/j20.jpg)
## leetcode 121 Best Time to Buy and Sell Stock
### easy

####  题意
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

Example 1:
```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```
Example 2:
```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

#### 分析
其实就是问数组里面哪两个元素的差最大，但是前提是大的数字必须在小的数字的前面。

目前有两种思路：第一种就是两重循环，计算差值，然后将这个差值记录，再与之前的差值比较，直到最后选出最大的差值。这样的话，时间复杂度是$O(n^2)$。代码如下：
```C++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int profit=0;
        for(int i=0;i<prices.size();i++)
        {
            for(int j=i+1;j<prices.size();j++)
            {
                int temp=prices[j]-prices[i];
                if(temp>profit)
                    profit=temp;
                
            }
        }
        return profit;
    }
};
```
另外一种做法是做两个标记，然后进行循环，如果这个数比buy小，就将这个数赋值给buy，此时sale也应该等于这个数，这是因为sale必须在buy的前面，这一点一定要注意。然后如果另一个数比sale大，就把这个数赋值给sale，最后输出sale与buy的差就行，这样做时间复杂度只有$O(n)$。



```c++
 int maxProfit(vector<int>& prices) {
        if(prices.size()<=0)
            return 0;
        int profit=0;
        
        int buy=prices[0];
        int sale=prices[0];
        for(int i=1;i<prices.size();i++)
        {
            if(prices[i]<buy)
            {
                buy=prices[i];
                sale=prices[i];
            }
            if(prices[i]>sale)
            {
                sale=prices[i];
                if(sale-buy>profit)
                    profit=sale-buy;
            }
        }
        return profit;
    }

```
除此之外，要注意，测试样例里面可能有数组长度不符合要求的例子，这时就需要对数组长度进行判断再去操作。否则提交之后会发生runtime error的错误，不会AC。