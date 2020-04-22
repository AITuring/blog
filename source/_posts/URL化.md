---
title: 程序员面试金典面试题:URL化
date: 2020-03-06 18:27:41
tags: [程序员面试金典面试题,python,算法]
categories: [程序员面试金典面试题]
---

<img src="http://lishengyu.xyz/pubgm/2020-02-26 133606(17).jpg" >

## 程序员面试金典面试题 
### 01.03. URL化

**Easy**

URL化。编写一种方法，将字符串中的空格全部替换为%20。假定该字符串尾部有足够的空间存放新增字符，并且知道字符串的“真实”长度。（注：用Java实现的话，请使用字符数组实现，以便直接在数组上操作。）

**示例1:**

```
 输入："Mr John Smith    ", 13
 输出："Mr%20John%20Smith"
```

**示例2:**

```
 输入："               ", 5
 输出："%20%20%20%20%20"


```
**提示：**
- 字符串长度在[0, 500000]范围内。

### 思路([leetcode题解](https://leetcode-cn.com/problems/string-to-url-lcci/solution/zong-he-ti-jie-by-flypython-2/))

常见的做法是从字符串尾部开始编辑，从后往前反向操作。因为字符串尾部有额外的缓冲，可以直接修改，不必担心会覆写原有数据

这题可以先对空格进行计数，然后从应该的末尾开始挪字符到应该的位置，见到空格就替换，到头部字符为止。

不过这题用Python来做，可以不用这样。比如，可以转为list，遍历一次，直接替换。


```pyhon
class Solution:
    def replaceSpaces(self, S: str, length: int) -> str:
        l = list(S)
        for p in range(length):
            if l[p] == ' ': 
                l[p] = '%20'
        
        return ''.join(l[:length])

```

既然都转成了list，那split是否更好一点？

```python
class Solution:
    def replaceSpaces(self, S: str, length: int) -> str:
        return "%20".join(S[:length].split(" "))
```

split都用了，那replace岂不是更好，非常清晰。

```python
class Solution:
    def replaceSpaces(self, S: str, length: int) -> str:
        return S[0:length].replace(" ", "%20")
```
