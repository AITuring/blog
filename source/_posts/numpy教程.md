---
title: numpy教程
date: 2019-12-20 14:24:12
tags: [numpy,python]
categories: [numpy]
---
<img src="https://extraimage.net/images/2019/09/23/5ac6e9d90002903efacacdcb8182b8ed.png" width="200" height align="middle"></p>

<h2 id="1-什么是Nmupy"><a href="#1-什么是Nmupy" class="headerlink" title="1.什么是Nmupy"></a>1.什么是Nmupy</h2><p>NumPy是Python中科学计算的基础包。它是一个Python库，提供多维数组对象，各种派生对象（如掩码数组和矩阵），以及用于数组快速操作的各种API，有包括数学、逻辑、形状操作、排序、选择、输入输出、离散傅立叶变换、基本线性代数，基本统计运算和随机模拟等等。</p>
<p>NumPy包的核心是ndarray 对象。它封装了python原生的同数据类型的n维数组，为了保证其性能优良，其中有许多操作都是代码在本地进行编译后执行的。</p>
<h3 id="Numpy数组和原生Python-数组之间的区别"><a href="#Numpy数组和原生Python-数组之间的区别" class="headerlink" title="Numpy数组和原生Python 数组之间的区别"></a>Numpy数组和原生Python 数组之间的区别</h3><ul>
<li>NumPy 数组在创建时具有固定的大小，与Python的原生数组对象（可以动态增长）不同。更改ndarray的大小将创建一个新数组并删除原来的数组。</li>
<li>NumPy 数组中的元素都需要具有相同的数据类型，因此在内存中的大小相同。 例外情况：Python的原生数组里包含了NumPy的对象的时候，这种情况下就允许不同大小元素的数组。</li>
<li>NumPy 数组有助于对大量数据进行高级数学和其他类型的操作。通常，这些操作的执行效率更高，比使用Python原生数组的代码更少。</li>
<li>越来越多的基于Python的科学和数学软件包使用NumPy数组; 虽然这些工具通常都支持Python的原生数组作为参数，但它们在处理之前会还是会将输入的数组转换为NumPy的数组，而且也通常输出为NumPy数组。</li>
</ul>
<p>下面是一个具体的例子：</p>
<p>将1维数组中的每个元素与相同长度的另一个序列中的相应元素相乘的情况。一般情况下，如果数据存储在两个Python 列表<code>a</code> 和 <code>b</code> 中，我们可以迭代每个元素，如下所示：

```python
c = []
for i in range(len(a)):
    c.append(a[i]*b[i])
```





<p>正常这样写，完全没有问题。但是如果<code>a</code>和<code>b</code>的长度都是几百万的话，这样的效率就比较低了，我们可以通过在C中写入以下代码，更快地完成相同的任务：</p>

```C
for (i = 0; i < rows; i++): {
  c[i] = a[i]*b[i];
}
```

<p>这节省了解释Python代码和操作Python对象所涉及的所有开销，但牺牲了用Python编写代码所带来的好处。此外，编码工作需要增加的维度，我们的数据。例如，对于二维数组，C代码(如前所述)会扩展为这样：

```C
for (i = 0; i < rows; i++): {
  for (j = 0; j < columns; j++): {
    c[i][j] = a[i][j]*b[i][j];
  }
}
```
<p>NumPy 为我们提供了两全其美的解决方案：当涉及到 <code>ndarray</code> 时，逐个元素的操作是“默认模式”，但逐个元素的操作由预编译的C代码快速执行。在NumPy中：

```python
c = a * b
```
<p>以近C的速度执行前面的示例所做的事情！</p>
<h2 id="2-numpy基础属性"><a href="#2-numpy基础属性" class="headerlink" title="2. numpy基础属性"></a>2. numpy基础属性</h2><p><code>NmuPy</code>主要处理的是同构多维数组。它是一个所有类型都相同的元素表（通常是数字）。数组中的元素由非负整数元组索引。在NumPy维度中称为<strong>轴</strong>。</p>
<p>例如，3D空间中的点的坐标<code>[1, 2, 1]</code>具有一个轴。该轴有3个元素，所以我们说它的长度为3.在下面的例子中，数组有2个轴。第一轴的长度为2，第二轴的长度为3。

```
[[ 1., 0., 0.],
 [ 0., 1., 2.]]
```
<p>NumPy的数组类被调用<code>ndarray</code>。它也被别名所知 <code>array</code>。请注意，<code>numpy.array</code>这与标准Python库类不同<code>array.array</code>，后者只处理一维数组并提供较少的功能。<code>ndarray</code>对象更重要的属性是：</p>
<ul>
<li><code>ndarray.ndim</code> - 数组的轴（维度）的个数。在Python世界中，维度的数量被称为<code>rank</code>。</li>
<li><code>ndarray.shape</code> - 数组的维度。这是一个整数的元组，表示每个维度中数组的大小。对于有 n 行和 m 列的矩阵，shape 将是 (n,m)。因此，shape 元组的长度就是rank或维度的个数 ndim。</li>
<li><code>ndarray.size</code> - 数组元素的总数。这等于 shape 的元素的乘积。</li>
<li><code>ndarray.dtype</code> - 一个描述数组中元素类型的对象。可以使用标准的Python类型创建或指定dtype。另外NumPy提供它自己的类型。例如<code>numpy.int32</code>、<code>numpy.int16</code>和<code>numpy.float64</code>。</li>
<li><code>ndarray.itemsize</code> - 数组中每个元素的字节大小。例如，元素为 <code>float64</code> 类型的数组的 <code>itemsize</code> 为8（=64/8），而 <code>complex32</code> 类型的数组的 <code>itemsize</code> 为4（=32/8）。它等于 <code>ndarray.dtype.itemsize</code> 。</li>
<li><code>ndarray.data</code> - 该缓冲区包含数组的实际元素。通常，我们不需要使用此属性，因为我们将使用索引访问数组中的元素。</li>
</ul>
<p>下面是一些使用<code>numpy</code>的例子：

```python
>>> import numpy as np
>>> a=np.arange(15).reshape(3,5)
>>> a
array([[ 0,  1,  2,  3,  4], 
       [ 5,  6,  7,  8,  9], 
       [10, 11, 12, 13, 14]])
>>> a.shape
(3, 5)
>>> a.ndim
2   
>>> a.dtype.name
'int32'
>>> a.itemsize
4   
>>> a.size
15
>>> type(a)
<class 'numpy.ndarray'>
```

<h2 id="3-特定array的创建"><a href="#3-特定array的创建" class="headerlink" title="3. 特定array的创建"></a>3. 特定array的创建</h2><p>在实际上的项目工程中，我们常常会需要一些特定的数据，NumPy中提供了这么一些辅助函数:</p>
<ul>
<li><code>zeros</code>：用来创建元素全部是0的数组</li>
<li><code>ones</code>：用来创建元素全部是1的数组</li>
<li><code>empty</code>：用来创建未初始化的数据，因此是内容是不确定的</li>
<li><code>arange</code>：通过指定范围和步长来创建数组</li>
<li><code>linespace</code>：通过指定范围和元素数量来创建数组</li>
<li><code>random</code>：用来生成随机数</li>
</ul>

```python
# create_specific_array.py

import numpy as np

a = np.zeros((2,3))
print('np.zeros((2,3)= \n{}\n'.format(a))

b = np.ones((2,3))
print('np.ones((2,3))= \n{}\n'.format(b))

c = np.empty((2,3))
print('np.empty((2,3))= \n{}\n'.format(c))

d = np.arange(1, 2, 0.3)
print('np.arange(1, 2, 0.3)= \n{}\n'.format(d))

e = np.linspace(1, 2, 7)
print('np.linspace(1, 2, 7)= \n{}\n'.format(e))

f = np.random.random((2,3))
print('np.random.random((2,3))= \n{}\n'.format(f))
```

<p>这段代码的输出如下</p>

```python
np.zeros((2,3)= 
[[ 0.  0.  0.]
 [ 0.  0.  0.]]

np.ones((2,3))= 
[[ 1.  1.  1.]
 [ 1.  1.  1.]]

np.empty((2,3))= 
[[ 1.  1.  1.]
 [ 1.  1.  1.]]

np.arange(1, 2, 0.3)= 
[ 1.   1.3  1.6  1.9]

np.linspace(1, 2, 7)= 
[ 1.          1.16666667  1.33333333  1.5         1.66666667  1.83333333
  2.        ]

np.random.random((2,3))= 
[[ 0.5744616   0.58700653  0.59609648]
 [ 0.0417809   0.23810732  0.38372978]]
```

<h2 id="4-Shape与操作"><a href="#4-Shape与操作" class="headerlink" title="4.Shape与操作"></a>4.Shape与操作</h2><p>除了生成数组之外，当我们已经持有某个数据之后，我们可能会需要根据已有数组来产生一些新的数据结构，这时候我们可以使用下面这些函数：</p>
<ul>
<li><code>reshape</code>：根据已有数组和指定的shape，生成一个新的数组</li>
<li><code>vstack</code>：用来将多个数组在垂直（v代表vertical）方向拼接（数组的维度必须匹配）</li>
<li><code>hstack</code>：用来将多个数组在水平（h代表horizontal）方向拼接（数组的维度必须匹配）</li>
<li><code>hsplit</code>：用来将数组在水平方向拆分</li>
<li><code>vsplit</code>：用来将数组在垂直方向拆分<br>下面我们通过一些例子来进行说明。</li>
</ul>
<p>为了便于测试，我们先创建几个数据。这里我们创建了：</p>
<p><code>zero_line</code>：一行包含3个0的数组<br><code>one_column</code>：一列包含3个1的数组<br><code>a</code>：一个2行3列的矩阵<br><code>b</code>：[11, 20)区间的整数数组</p>

```python
# shape_manipulation.py

zero_line = np.zeros((1,3))
one_column = np.ones((3,1))
print("zero_line = \n{}\n".format(zero_line))
print("one_column = \n{}\n".format(one_column))

a = np.array([(1,2,3), (4,5,6)])
b = np.arange(11, 20)
print("a = \n{}\n".format(a))
print("b = \n{}\n".format(b))
```

<p>通过输出我们可以看到它们的结构：

```python
zero_line = 
[[ 0.  0.  0.]]

one_column = 
[[ 1.]
 [ 1.]
 [ 1.]]

a = 
[[1 2 3]
 [4 5 6]]

b = 
[11 12 13 14 15 16 17 18 19]
```
<p>数组b原先是一个一维数组，现在我们通过reshape方法将其调整成为一个3行3列的矩阵：

```python
# shape_manipulation.py

b = b.reshape(3, -1)
print("b.reshape(3, -1) = \n{}\n".format(b))
```
<p>这里的第二参数设为-1，表示根据实际情况自动决定。由于原先是9个元素的数组，因此调整后刚好是3X3的矩阵。这段代码输出如下：

```python
b.reshape(3, -1) = 
[[11 12 13]
 [14 15 16]
 [17 18 19]]
```
<p>接着，我们通过vstack函数，将三个数组在垂直方向拼接：

```python
# shape_manipulation.py

c = np.vstack((a, b, zero_line))
print("c = np.vstack((a,b, zero_line)) = \n{}\n".format(c))
```
<p>这段代码输出如下，仔细观察拼接前后的数据结构：

```python
c = np.vstack((a,b, zero_line)) = 
[[  1.   2.   3.]
 [  4.   5.   6.]
 [ 11.  12.  13.]
 [ 14.  15.  16.]
 [ 17.  18.  19.]
 [  0.   0.   0.]]
```
<p>同样的，我们也可以通过hstack进行水平方向的拼接。为了可以拼接我们需要先将数组a调整一下结构：

```python
# shape_manipulation.py

a = a.reshape(3, 2)
print("a.reshape(3, 2) = \n{}\n".format(a))

d = np.hstack((a, b, one_column))
print("d = np.hstack((a,b, one_column)) = \n{}\n".format(d))
```
<p>这段代码输出如下，再仔细观察拼接前后的数据结构：

```python
a.reshape(3, 2) = 
[[1 2]
 [3 4]
 [5 6]]

d = np.hstack((a,b, one_column)) = 
[[  1.   2.  11.  12.  13.   1.]
 [  3.   4.  14.  15.  16.   1.]
 [  5.   6.  17.  18.  19.   1.]]
```
<p>注意，如果两个数组的结构是不兼容的，拼接将无法完成。例如下面这行代码，它将无法执行：

```python
# shape_manipulation.py

# np.vstack((a,b)) # ValueError: dimensions not match
```
<p>这是因为数组a具有两列，而数组b具有3列，所以它们无法拼接。</p>
<p>接下来我们再看一下拆分。首先，我们将数组d在水平方向拆分成3个数组。然后我们将中间一个（下标是1）数组打印出来：

```python
# shape_manipulation.py

e = np.hsplit(d, 3) # Split a into 3
print("e = np.hsplit(d, 3) = \n{}\n".format(e))
print("e[1] = \n{}\n".format(e[1]))
```
<p>这段代码输出如下：

```python
e = np.hsplit(d, 3) = 
[array([[ 1.,  2.],
       [ 3.,  4.],
       [ 5.,  6.]]), array([[ 11.,  12.],
       [ 14.,  15.],
       [ 17.,  18.]]), array([[ 13.,   1.],
       [ 16.,   1.],
       [ 19.,   1.]])]

e[1] = 
[[ 11.  12.]
 [ 14.  15.]
 [ 17.  18.]]
```
<p>另外，假设设置的拆分数量使得原先的数组无法平均拆分，则操作会失败：

```python
# np.hsplit(d, 4) # ValueError: array split does not result in an equal division
```
<p>除了指定数量平均拆分，我们也可以指定列数进行拆分。下面是将数组d从第1列和第3列两个地方进行拆分：

```python
# shape_manipulation.py

f = np.hsplit(d, (1, 3)) # # Split a after the 1st and the 3rd column
print("f = np.hsplit(d, (1, 3)) = \n{}\n".format(f))
```
<p>这段代码输出如下。数组d被拆分成了分别包含1，2，3列的三个数组：

```python
f = np.hsplit(d, (1, 3)) = 
[array([[ 1.],
       [ 3.],
       [ 5.]]), array([[  2.,  11.],
       [  4.,  14.],
       [  6.,  17.]]), array([[ 12.,  13.,   1.],
       [ 15.,  16.,   1.],
       [ 18.,  19.,   1.]])]
```
<p>最后再将数组d在垂直方向进行拆分。同样的，如果指定的拆分数无法平均拆分则会失败：

```python
# shape_manipulation.py

g = np.vsplit(d, 3)
print("np.hsplit(d, 2) = \n{}\n".format(g))

# np.vsplit(d, 2) # ValueError: array split does not result in an equal division
np.vsplit(d, 3)将产生三个一维数组：

np.vsplit(d, 3) = 
[array([[  1.,   2.,  11.,  12.,  13.,   1.]]), array([[  3.,   4.,  14.,  15.,  16.,   1.]]), array([[  5.,   6.,  17.,  18.,  19.,   1.]])]
```
<h2 id="5-索引"><a href="#5-索引" class="headerlink" title="5.索引"></a>5.索引</h2><p>接下来我们看看如何访问NumPy数组中的数据。</p>
<p>同样的，为了测试方便，我们先创建一个一维数组。它的内容是 [100，200）区间的整数。</p>
<p>最基本的，可以通过array[index]的方式指定下标来访问数组的元素，这一点对于有一点编程经验的人来说应该都是很熟悉的。

```python
# array_index.py

import numpy as np

base_data = np.arange(100, 200)
print("base_data\n={}\n".format(base_data))

print("base_data[10] = {}\n".format(base_data[10]))
```
<p>上面这段代码输出如下：

```python
base_data
=[100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117
 118 119 120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135
 136 137 138 139 140 141 142 143 144 145 146 147 148 149 150 151 152 153
 154 155 156 157 158 159 160 161 162 163 164 165 166 167 168 169 170 171
 172 173 174 175 176 177 178 179 180 181 182 183 184 185 186 187 188 189
 190 191 192 193 194 195 196 197 198 199]

base_data[10] = 110
```
<p>在NumPy中，我们可以创建一个包含了若干个下标的数组来获取目标数组中的元素。如下所示：

```python
# array_index.py
every_five = np.arange(0, 100, 5)
print("base_data[every_five] = \n{}\n".format(
    base_data[every_five]))
```
<p><code>every_five</code>是包含了我们要获取的下标的数组，它的内容大家应该很容易理解。我们可以直接通过方括号的形式来获取到所有我们指定了下标的元素，它们如下：

```python
base_data[every_five] = 
[100 105 110 115 120 125 130 135 140 145 150 155 160 165 170 175 180 185
 190 195]
```
<p>下标数组可以是一维的，当然也可以是多维的。假设我们要获取一个2X2的矩阵，这个矩阵的内容来自于目标数组中1，2，10，20这四个下标的元素，则可以这样写：

```python
# array_index.py
a = np.array([(1,2), (10,20)])
print("a = \n{}\n".format(a))
print("base_data[a] = \n{}\n".format(base_data[a]))
```
<p>这段代码输出如下：

```python
a = 
[[ 1  2]
 [10 20]]
 
base_data[a] = 
[[101 102]
 [110 120]]
```
<p>上面我们看到的是目标数组是一维的情况，下面我们把这个数组转换成一个10X10的二维数组。

```python
# array_index.py
base_data2 = base_data.reshape(10, -1)
print("base_data2 = np.reshape(base_data, (10, -1)) = \n{}\n".format(base_data2))
```
<p><code>reshape</code>函数前面已经介绍过,应该能够想到它的结果：

```
base_data2 = np.reshape(base_data, (10, -1)) = 
[[100 101 102 103 104 105 106 107 108 109]
 [110 111 112 113 114 115 116 117 118 119]
 [120 121 122 123 124 125 126 127 128 129]
 [130 131 132 133 134 135 136 137 138 139]
 [140 141 142 143 144 145 146 147 148 149]
 [150 151 152 153 154 155 156 157 158 159]
 [160 161 162 163 164 165 166 167 168 169]
 [170 171 172 173 174 175 176 177 178 179]
 [180 181 182 183 184 185 186 187 188 189]
 [190 191 192 193 194 195 196 197 198 199]]
```
<p>对于二维数组来说：</p>
<p>假设我们只指定了一个下标，则访问的结果仍然是一个数组。<br>假设我们指定了两个下标，则访问得到的是其中的元素<br>我们也可以通过”-1”来指定“最后一个”的元素

```python
# array_index.py
print("base_data2[2] = \n{}\n".format(base_data2[2]))
print("base_data2[2, 3] = \n{}\n".format(base_data2[2, 3]))
print("base_data2[-1, -1] = \n{}\n".format(base_data2[-1, -1]))
```
<p>这段代码输出如下。</p>

```python
base_data2[2] = 
[120 121 122 123 124 125 126 127 128 129]

base_data2[2, 3] = 
123

base_data2[-1, -1] = 
199
```
<p>对于更高维的数组，原理是一样的。</p>
<p>除此之外，我们还可以通过”:“的形式来指定范围，例如：2:5 这样。只写”:“则表示全部范围。</p>
<p>看下面这段代码：

```python
# array_index.py
print("base_data2[2, :]] = \n{}\n".format(base_data2[2, :]))
print("base_data2[:, 3]] = \n{}\n".format(base_data2[:, 3]))
print("base_data2[2:5, 2:4]] = \n{}\n".format(base_data2[2:5, 2:4]))
```
<p>它的含义是：</p>
<p>获取下标为2的行的所有元素<br>获取下标为3的列的所有元素<br>获取下标为[2,5)行，下标为[2,4)列的所有元素。

## 6.数学运算

</span></span><br><span class="line"></span><br><span class="line"></span><br><span class="line">NumPy中自然也少不了大量的数学运算函数，下面是一些例子，更多的函数请参见这里`NumPy manual contents`：</span><br><span class="line">

```python
# operation.py

import numpy as np

base_data = (np.random.random((5, 5)) - 0.5) * 100
print("base_data = \n{}\n".format(base_data))

print("np.amin(base_data) = {}".format(np.amin(base_data)))
print("np.amax(base_data) = {}".format(np.amax(base_data)))
print("np.average(base_data) = {}".format(np.average(base_data)))
print("np.sum(base_data) = {}".format(np.sum(base_data)))
print("np.sin(base_data) = \n{}".format(np.sin(base_data)))
```
<p>这段代码输出如下：

```python
base_data = 
[[ -9.63895991   6.9292461   -2.35654712 -48.45969283  13.56031937]
 [-39.75875796 -43.21031705 -49.27708561   6.80357128  33.71975059]
 [ 36.32228175  30.92546582 -41.63728955  28.68799187   6.44818484]
 [  7.71568596  43.24884701 -14.90716555  -9.24092252   3.69738718]
 [-31.90994273  34.06067289  18.47830413 -16.02495202 -44.84625246]]

np.amin(base_data) = -49.277085606595726
np.amax(base_data) = 43.24884701268845
np.average(base_data) = -3.22680706079886
np.sum(base_data) = -80.6701765199715
np.sin(base_data) = 
[[ 0.21254814  0.60204578 -0.70685739  0.9725159   0.8381861 ]
 [-0.88287359  0.69755541  0.83514527  0.49721505  0.74315189]
 [-0.98124746 -0.47103234  0.7149727  -0.40196147  0.16425187]
 [ 0.99045239 -0.66943662 -0.71791164 -0.18282139 -0.5276184 ]
 [-0.4741657   0.47665553 -0.36278223  0.31170676 -0.76041722]]

```


## 7.矩阵

</span></span><br><span class="line">接下来我们看一下以矩阵的方式使用NumPy。</span><br><span class="line"></span><br><span class="line">首先，我们创建一个<span class="number">5</span>X5的随机数整数矩阵。有两种方式可以获得矩阵的转置：通过.T或者transpose函数。另外，通过dot函数可以进行矩阵的乘法，示例代码如下：

```python
# matrix.py

import numpy as np

base_data = np.floor((np.random.random((5, 5)) - 0.5) * 100)
print("base_data = \n{}\n".format(base_data))

print("base_data.T = \n{}\n".format(base_data.T))
print("base_data.transpose() = \n{}\n".format(base_data.transpose()))

matrix_one = np.ones((5, 5))
print("matrix_one = \n{}\n".format(matrix_one))

minus_one = np.dot(matrix_one, -1)
print("minus_one = \n{}\n".format(minus_one))

print("np.dot(base_data, minus_one) = \n{}\n".format(
np.dot(base_data, minus_one)))
```
<p>这段代码输出如下：

```
base_data = 
[[-49.  -5.  11. -13. -41.]
 [ -6. -33. -33. -47.  -4.]
 [-38.  26.  28. -18.  18.]
 [ -3. -19. -15. -39.  45.]
 [-43.   6.  18. -15. -21.]]

base_data.T = 
[[-49.  -6. -38.  -3. -43.]
 [ -5. -33.  26. -19.   6.]
 [ 11. -33.  28. -15.  18.]
 [-13. -47. -18. -39. -15.]
 [-41.  -4.  18.  45. -21.]]

base_data.transpose() = 
[[-49.  -6. -38.  -3. -43.]
 [ -5. -33.  26. -19.   6.]
 [ 11. -33.  28. -15.  18.]
 [-13. -47. -18. -39. -15.]
 [-41.  -4.  18.  45. -21.]]

matrix_one = 
[[ 1.  1.  1.  1.  1.]
 [ 1.  1.  1.  1.  1.]
 [ 1.  1.  1.  1.  1.]
 [ 1.  1.  1.  1.  1.]
 [ 1.  1.  1.  1.  1.]]

minus_one = 
[[-1. -1. -1. -1. -1.]
 [-1. -1. -1. -1. -1.]
 [-1. -1. -1. -1. -1.]
 [-1. -1. -1. -1. -1.]
 [-1. -1. -1. -1. -1.]]

np.dot(base_data, minus_one) = 
[[  97.   97.   97.   97.   97.]
 [ 123.  123.  123.  123.  123.]
 [ -16.  -16.  -16.  -16.  -16.]
 [  31.   31.   31.   31.   31.]
 [  55.   55.   55.   55.   55.]]
```


## 8.随机数

</span></span><br><span class="line"></span><br><span class="line"></span><br><span class="line">随机数是我们在编程过程中非常频繁用到的一个功能。例如：生成演示数据，或者将已有的数据顺序随机打乱以便分割出建模数据和验证数据。</span><br><span class="line"></span><br><span class="line">`numpy.random` 包中包含了很多中随机数的算法。下面我们列举四种最常见的用法：

```python
# rand.py

import numpy as np

print("random: {}\n".format(np.random.random(20)));

print("rand: {}\n".format(np.random.rand(3, 4)));

print("randint: {}\n".format(np.random.randint(0, 100, 20)));

print("permutation: {}\n".format(np.random.permutation(np.arange(20))));
```
<p>在四种用法分别是：</p>
<p>生成20个随机数，它们每一个都是[0.0, 1.0)之间<br>根据指定的shape生成随机数<br>生成指定范围内（[0, 100)）的指定数量（20）的随机整数<br>对已有的数据（[0, 1, 2, …, 19]）的顺序随机打乱顺序<br>这段代码的输出如下所示：

```
random: [0.62956026 0.56816277 0.30903156 0.50427765 0.92117724 0.43044905
 0.54591323 0.47286235 0.93241333 0.32636472 0.14692983 0.02163887
 0.85014782 0.20164791 0.76556972 0.15137427 0.14626625 0.60972522
 0.2995841  0.27569573]

rand: [[0.38629927 0.43779617 0.96276889 0.80018417]
 [0.67656892 0.97189483 0.13323458 0.90663724]
 [0.99440473 0.85197677 0.9420241  0.79598706]]

randint: [74 65 51 34 22 69 81 36 73 35 98 26 41 84  0 93 41  6 51 55]

permutation: [15  3  8 18 14 19 16  1  0  4 10 17  5  2  6 12  9 11 13  7]
```
<pre><code>                                    🎓🎓🎓
</code></pre><p><img src="http://lishengyu.xyz/gif/mmexport1571402223200.gif" width="400" height align="middle"></p>


