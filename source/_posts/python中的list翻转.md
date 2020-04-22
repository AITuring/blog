---
title: python中的list翻转
date: 2019-10-07 16:00:43
tags: python
categories: python
---

![](http://lishengyu.xyz/j202.jpg)
## 1.list翻转
`list.reverse()`改变原list，没有返回值.`reversed(list)`不改变原list，有返回值。

### `reverse()`：
是python中列表的一个内置方法（也就是说，在字典，字符串或者元组中，是没有这个内置方法的），用于列表中数据的反转
```python
lista = [1, 2, 3, 4]
lista.reverse()
print(lista)
>>>[4, 3, 2, 1]
```
<!-- more --> 

lista.reverse() 这一步操作的返回值是一个None，其作用的结果，需要通过打印被作用的列表才可以查看出具体的效果。

### `reversed()`：
reversed()是python自带的一个方法，准确说，应该是一个类；
关于reversed()官方解释：

reverse（sequence） - >反转迭代器的序列值,然后返回反向迭代器

也就是说，在经过reversed()的作用之后，返回的是一个把序列值经过反转之后的迭代器，所以，需要通过遍历，或者List,或者next()等方法，获取作用后的值；
```python
bb = [1,3,5,7]
print(list(reversed(bb)))
>>>[7,5,3,1]
```