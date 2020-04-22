---
title: python中的str与repr
date: 2020-01-11 10:14:12
tags: [python]
categories: [python]
---
<img src="http://lishengyu.xyz/sr712.jpg" alt></p>
<h3 id="二者的区别"><a href="#二者的区别" class="headerlink" title="二者的区别"></a>二者的区别</h3><p>在 Python 中要将某一类型的变量或者常量转换为字符串对象通常有两种方法，即 <code>str()</code> 或者 <code>repr()</code> 。<br>一般来说，无论是在类中实现，还是单独使用。<code>str()</code> 的输出追求可读性，输出格式要<strong>便于理解</strong>，适合用于输出内容到用户终端。<br><code>repr()</code> 的输出<strong>追求明确性</strong>，除了对象内容，还需要展示出对象的数据类型信息，适合开发和调试阶段使用。</p>
<p>下面是一个例子：

```python
>>> from datetime import datetime
>>> now=datetime.now()
>>> print(str(now))
2019-10-25 17:37:32.125564
>>> print(repr(now))
datetime.datetime(2019, 10, 25, 17, 37, 32, 125564)
```

<p>通过 <code>str()</code> 的输出结果我们能很好地知道 <code>now</code> 实例的内容，但是却丢失了 <code>now</code> 实例的数据类型信息。而通过 <code>repr()</code> 的输出结果我们不仅能获得 <code>now</code> 实例的内容，还能知道 <code>now</code> 是 <code>datetime.datetime</code> 对象的实例。</p>
<h4 id="Python-中一切皆对象"><a href="#Python-中一切皆对象" class="headerlink" title="Python 中一切皆对象"></a>Python 中一切皆对象</h4><p><code>Python Data Model</code> 中指出，Python 中的所有数据都是“对象”(Object)。Python 中几乎所有（不确定有没有反例）的操作都可以对应到对象的某个特殊方法。因此可以通过手工实现它们来覆盖默认的逻辑。</p>
<p>比如说迭代器(<code>iterator</code>)取长度操作 <code>len(iter)</code> 对应 <code>obj.__len__</code>；加法操作 <code>a + b</code> 对应<code>a.__add__(b)</code>；函数调用 <code>func(...)</code> 对应 <code>func.__cal__(...)</code>。</p>
<p>同样的，<code>str()</code>内置函数使用 <code>__str__</code> 显示对象的字符串表示形式，而 <code>repr()</code>内置函数使用 <code>__repr__</code>显示对象。</p>
<h4 id="str-和-repr"><a href="#str-和-repr" class="headerlink" title="__str__和__repr__"></a><code>__str__</code>和<code>__repr__</code></h4><p>python 默认有对<code>__repr__</code> 和 <code>__str__</code> 的实现方法,当两者均使用缺省定义的情况下 <code>__repr__</code>是等同于<code>__str__</code>的。</p>
<p><code>__str__</code> 的默认实现是直接调用了 <code>__repr__</code>方法。所以仅定义 <code>__repr__</code> 的时候， <code>__repr__ == __str__</code>，因此如果覆盖了 <code>__repr__</code>方法，<code>__str__</code> 的结果也会随之改变。 但是仅定义 <code>__str__</code> 的情况下，两者不相等。如果两者都定义了，结果也是不相等的。</p>
<p>例如：

```python
# __str__ 和 __repr__都没有定义
class Test:
    pass

print(str(Test()))
print(repr(Test()))
print(str(Test()) == repr(Test()))
```

<p>输出结果:

```python
>>> print(str(Test))
<class '__main__.Test'>
>>> print(repr(Test))
<class '__main__.Test'>
>>> print(repr(Test) == str(Test))
True
```

```python
# 只定义 __str__
class Test1:
    def __str__(self):
        return "Test1.__str__"

print(str(Test1()))
print(repr(Test1()))
print(str(Test1()) == repr(Test1()))
```

<p>输出结果如下:

```python
>>> print(str(Test1()))
Test1.__str__
>>> print(repr(Test1()))
<__main__.Test1 object at 0x000001F9B3DCD518>
>>> print(str(Test1()) == repr(Test1()))
False
```

```python
# 只定义 __repr__
class Test2:
    def __repr__(self):
        return "Test1.__str__"

print(str(Test2()))
print(repr(Test2()))
print(str(Test2()) == repr(Test2()))
```

<p>输出结果如下:</p>

```python
>>> print(str(Test2()))
Test2.__repr__
>>> print(repr(Test2()))
Test2.__repr__
>>> print(str(Test2()) == repr(Test2()))
True
```


```python
# 两者均定义
class Test3:
    def __repr__(self):
        return "Test3.__repr__"
    def __str__(self):
        return "Test3.__str__"


print(str(Test3()))
print(repr(Test3()))
print(str(Test3()) == repr(Test3()))
```
<p>输出的结果如下:

```python
>>> print(str(Test3()))
Test3.__str__
>>> print(repr(Test3()))
Test3.__repr__
>>> print(str(Test3()) == repr(Test3()))
False
```
<p>如果要自己实现，一般实现<code>__str__</code>就行。</p>

     
