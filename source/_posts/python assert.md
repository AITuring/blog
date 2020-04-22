---
title: python assert
date: 2020-01-20 00:14:12
tags: [python]
categories: [python]
---
<img src="http://lishengyu.xyz/gif/0aca6554c60c28e3287a831b4be07b7b.gif" alt><br>在开发一个程序时候，与其让它运行时崩溃，不如在它出现错误条件时就崩溃（返回错误）。这时候断言<code>assert</code>就显得非常有用。</p>
<p><code>python assert</code>断言是声明布尔值必须为真的判定，如果发生异常就说明表达式为假。<br>可以理解<code>assert</code>断言语句为<code>raise-if-not</code>，用来测试表示式，其返回值为假，就会触发异常。</p>
<p><code>assert</code>的语法格式：

```python
assert expression
```

<p>它的等价语句为：

```python
if not expression:
  raise AssertionError
```

<p>下面这段代码用来检测数据类型的断言，因为<code>a_str</code> 是 <code>str</code> 类型，所以认为它是 <code>int</code> 类型肯定会引发错误。

```python
>>> a_str = 'this is a string'
>>> type(a_str)
<type 'str'>
>>> assert type(a_str)== str
>>> assert type(a_str)== int
 
Traceback (most recent call last):
 File "<pyshell#41>", line 1, in <module>
  assert type(a_str)== int
AssertionError
```

  