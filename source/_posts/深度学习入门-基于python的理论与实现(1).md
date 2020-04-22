---
title: 深度学习入门-基于python的理论与实现(1)
date: 2019-03-07  12:00:43
tags: [python,深度学习]
categories: [深度学习入门-基于python的理论与实现]
---

<p><img src="http://lishengyu.xyz/dl_from_scratch_front.png" width="200" height align="center"></p>
    

            
<h2 id="第一章：python入门"><a href="#第一章：python入门" class="headerlink" title="第一章：python入门"></a>第一章：python入门</h2><h3 id="1-5-NumPy"><a href="#1-5-NumPy" class="headerlink" title="1.5 NumPy"></a>1.5 NumPy</h3><h4 id="1-5-2-生成NumPy数组"><a href="#1-5-2-生成NumPy数组" class="headerlink" title="1.5.2 生成NumPy数组"></a>1.5.2 生成NumPy数组</h4><p>生成NumPy数组,需要<code>np.array()</code>方法，<code>np.array()</code>接受Python列表作为参数，生成NumPy数组(<code>np.ndarray</code>)。

```python
>>> x=np.array([1.0,2.0,3.0])
>>> print(x)
[1. 2. 3.]
>>>type(x)
<class 'numpy.ndarray'>
```

<h4 id="1-5-5-广播"><a href="#1-5-5-广播" class="headerlink" title="1.5.5 广播"></a>1.5.5 广播</h4><p>NumPy中,形状不同的数组之间也可以进行运算。如图：<br><img src="http://lishengyu.xyz/dl_from_scratch_broadcast1.png" alt></p>
<p>另外一个例子：

```python
>>> X=np.array([[1,2],[3,4]])
>>> Y=np.array([10,20])
>>> X*Y
array([[10,40],
       [30,40])
```

<p>在上面的例子中，如下图所示你，一维数组Y变成了和二维数组相同的形状你，然后再以对应原始的方式进行运算。<br><img src="http://lishengyu.xyz/dl_from_scratch_broadcast2.png" alt></p>
<h3 id="1-6-Matplotlib"><a href="#1-6-Matplotlib" class="headerlink" title="1.6 Matplotlib"></a>1.6 Matplotlib</h3><h4 id="1-6-1-绘制简单图形"><a href="#1-6-1-绘制简单图形" class="headerlink" title="1.6.1 绘制简单图形"></a>1.6.1 绘制简单图形</h4><p>下面是一个使用matplotlib的pyplot模块绘制sin函数的例子

```python
import numpy as np
import matplotlib.pyplot as plt
# 生成数据
# 以0.1为单位，生成0到6的数据
x=np.arange(0,6,0.1) 
y=np.sin(x)
# 绘制图形
plt.plot(x,y)
plt.show()
```


<p>这里用NumPy的arange方法生成了[0,0.1,0.2,…,5.8n,5.9]的数据，设为x。对x的各个元素，应用NumPy的sin函数np.sin(),将x,y的数据传递给plt.plot方法你，然后绘制图形。最后通过plt.show()显示图形，运行上述代码后，图形如下：</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_sin.png" width="350" height align="center"></p>
<h4 id="1-6-2-pyplot的功能"><a href="#1-6-2-pyplot的功能" class="headerlink" title="1.6.2 pyplot的功能"></a>1.6.2 pyplot的功能</h4><p>在上面sin函数中，增加一些代码：

```python
import numpy as np
import matplotlib.pyplot as plt
# 生成数据
# 以0.1为单位，生成0到6的数据
x=np.arange(0,6,0.1) 
y1=np.sin(x)
y2=np.cos(x)
# 绘制图形
plt.plot(x,y1,label="sin")
# 用虚线绘制
plt.plot(x,y2n,linestyle="--"n,label="cos")
# x轴标签
plt.xlabel("x")
# y轴标签
plt.ylabel("y") 
# 标题
plt.title('sin & cos')
plt.legend()
plt.show()
```


<p>结果如图：<br><img src="http://lishengyu.xyz/dl_from_scratch_sincos.png" width="350" height align="center"></p>
<h4 id="1-6-3-显示图像"><a href="#1-6-3-显示图像" class="headerlink" title="1.6.3 显示图像"></a>1.6.3 显示图像</h4><p>pyplot中<code>imshow()</code>方法用来显示图形你，<code>imread()</code>用来读入图像。</p>

