
---
title: 深度学习入门-基于python的理论与实现(3)
date: 2019-03-10  22:21:43
tags: [python,深度学习]
categories: [深度学习入门-基于python的理论与实现]
---
<p><img src="http://lishengyu.xyz/dl_from_scratch_front.png" width="200" height align="center"></p>
<h2 id="第三章：神经网络"><a href="#第三章：神经网络" class="headerlink" title="第三章：神经网络"></a>第三章：神经网络</h2><p>上一章学习了感知机。关于感知机，既有好消息，也有坏消息。好消息是，即便对于复杂的函数，感知机也隐含着能够表示它的可能性。即便是计算机进行的复杂处理，感知机（理论上）也可以将其表示出来。坏消息是，设定权重的工作，即确定合适的、能符合预期的输入与输出的权重，现在还是由人工进行的。</p>
<p>上一章中，我们结合与门、或门的真值表人工决定了合适的权重。神经网络的出现就是为了解决刚才的坏消息。具体地讲，<strong>神经网络的一个重要性质是它可以自动地从数据中学习到合适的权重参数</strong>。</p>
<h3 id="3-1-从感知器到神经网络"><a href="#3-1-从感知器到神经网络" class="headerlink" title="3.1 从感知器到神经网络"></a>3.1 从感知器到神经网络</h3><h4 id="3-1-1-神经网络的例子"><a href="#3-1-1-神经网络的例子" class="headerlink" title="3.1.1 神经网络的例子"></a>3.1.1 神经网络的例子</h4><p>如图是一个神经网络：</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_nn.png" width="350" height align="center"></p>
<p>如图所示。我们把最左边的一列称为<strong>输入层</strong>，最右边的一列称为<strong>输出层</strong>，中间的一列称为<strong>中间层</strong>。中间层有时也称为<strong>隐藏层</strong>。“隐藏”一词的意思是，隐藏层的神经元（和输入层、输出 层不同）肉眼看不见。</p>
<p>另外，这里把输入层到输出层依次称为第0层、第1层、第2层（层号之所以从0开始，是为了方便后面基于Python进行实现）。 图中，第0层对应输入层，第1层对应中间层，第2层对应输出层。</p>
<h4 id="3-1-2-复习感知器"><a href="#3-1-2-复习感知器" class="headerlink" title="3.1.2 复习感知器"></a>3.1.2 复习感知器</h4><p><img src="http://lishengyu.xyz/dl_from_scratch_perceptron.png" alt><br>

如图的感知器接受$x_1$和$x_2$两个输入信号你，输出$y$。其数学公式如下：</p>

$$y= \begin{cases}
0 & (b+w_1x_1+w_2x_2 \leq 0 )\\
1 & (b+w_1x_1+w_2x_2 > 0 )
\end{cases}$$

b是被称为偏置的参数，用于控制神经元被激活的容易程度；而$w_1$和$w_2$ 是表示各个信号的权重的参数，用于控制各个信号的重要性。 </p>
<p>在上图的网络中，偏置b并没有被画出来。如果要明确地表示出b，可以像下图这样做。</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_bias.png" alt></p>

图中添加了权重为b的输入信号1。这个感知机将$x_1$、$x_2$、1三个信号作为神经元的输入，将其和各自的权重相乘后，传送至下一个神经元。在下一个神经元中，计算这些加权信号的总和。如果这个总和超过0，则输出1，否则输出0。</p>
<p>另外，由于偏置的输入信号一直是1， 所以为了区别于其他神经元，我们在图中把这个神经元整个涂成灰色。 </p>
<p>现在将上式改写成更加简洁的形式。为了简化上式，我们用一个函数来表示这种分情况的动作（超过0则输出1，否则输出0）。引入新函数 h(x)，将上式改写成下面的式子：</p>

$$y=h(b+w_1x_1+w_2x_2)$$

$$h(x)= \begin{cases}
0 & (x \leq 0 )\\
1 & (x > 0 )
\end{cases}$$

第一个式中，输入信号的总和会被函数$h(x)$转换，转换后的值就是输出$y$。 然后第二个式所表示的函数$h(x)$，在输入超过0时返回1，否则返回0。因此， 第一个式子和第二个式子还有上面的式子做的是相同的事情。</p>
<h4 id="3-1-3-激活函数登场"><a href="#3-1-3-激活函数登场" class="headerlink" title="3.1.3 激活函数登场"></a>3.1.3 激活函数登场</h4>

刚才的$h(x)$函数会将输入信号的总和转换为输出信号，这种函数 一般称为激活函数（activation function）。如“激活”一词所示，激活函数的作用在于决定如何来激活输入信号的总和。 </p>
<h3 id="3-2-激活函数"><a href="#3-2-激活函数" class="headerlink" title="3.2 激活函数"></a>3.2 激活函数</h3><p>上一节表示的激活函数以阈值为界，一旦输入超过阈值，就切换输出。这样的函数称为“阶跃函数”。因此，可以说感知机中使用了阶跃函数作为 激活函数。也就是说，在激活函数的众多候选函数中，感知机使用了阶跃函数。 那么，如果感知机使用其他函数作为激活函数的话会怎么样呢？实际上，如果将激活函数从阶跃函数换成其他函数，就可以进入神经网络的世界了。下面就来介绍一下神经网络使用的激活函数。</p>
<h4 id="3-2-1-sigmoid函数"><a href="#3-2-1-sigmoid函数" class="headerlink" title="3.2.1 sigmoid函数"></a>3.2.1 sigmoid函数</h4><p>sigmoid函数：</p>

$$h(x)=\frac{1}{1+e^{-x}}$$

神经网络中用sigmoid函数作为激活函数，进行信号的转换，转换后的信号被传送给下一个神经元。</p>
<h4 id="3-2-2-阶跃函数的实现"><a href="#3-2-2-阶跃函数的实现" class="headerlink" title="3.2.2 阶跃函数的实现"></a>3.2.2 阶跃函数的实现</h4><p>阶跃函数如下式：</p>

$$h(x)= \begin{cases}
0 & (x \leq 0 )\\
1 & (x > 0 )
\end{cases}$$

当输入超过0时，输出1，否则输出0。可以像下面这样简单地实现阶跃函数。

```python
def step_function(x):
    if x>0:
        return 1
    else:
        return 0
```

这个实现简单、易于理解，但是参数x只能接受实数（浮点数）。也就是说，允许形如`step_function(3.0)`的调用，但不允许参数取NumPy数组，例如`step_function(np.array([1.0, 2.0]))`。为了便于后面的操作，我们把它修改为支持NumPy数组的实现。为此，可以考虑下述实现。

```python
def step_function(x):
    y=x>0
    return y.astype(np.int)
```

可以用<code>astype()</code>方法转换NumPy数组的类型。<code>astype()</code>方法通过参数指定期望的类型，这个例子中是<code>np.int</code>型。Python中将布尔型转换为int型后，True会转换为1,False会转换为0。</p>
<h4 id="3-2-3-阶跃函数的图形"><a href="#3-2-3-阶跃函数的图形" class="headerlink" title="3.2.3 阶跃函数的图形"></a>3.2.3 阶跃函数的图形</h4><p>下面用图来表示上面定义的阶跃函数，为此需要使用matplotlib库。</p>

```python
import numpy as np
import matplotlib.pylab as plt
def step_function(x):
    return np.array(x>0,dtype=np.int)
x=np.arange(-5.0,5.0,0.1)
y=step_function(x)
plt.plot(x,y)
plt.ylim(-0.1,1.1) #指定y轴的范围
plt.show()
```


函数<code>np.arange(-5.0, 5.0, 0.1)</code>在−5.0到5.0的范围内，以0.1为单位，生成 NumPy数组（[-5.0, -4.9, …, 4.9]）。 <code>step_function()</code>以该NumPy数组为参数，对数组的各个元素执行阶跃函数运算，并以数组形式返回运算结果。 对数组x、y进行绘图，结果如图所示。</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_jieyue.png" width="350" height align="center"></p>
<p>如图，阶跃函数以0为界，输出从0切换为1（或者从1切换为0）。 它的值呈阶梯式变化，所以称为阶跃函数。</p>
<h4 id="3-2-4-sigmoid函数的实现"><a href="#3-2-4-sigmoid函数的实现" class="headerlink" title="3.2.4 sigmoid函数的实现"></a>3.2.4 sigmoid函数的实现</h4>

```python
def sigmoid(x):
    return 1/(1+np.exp(-x))
```

绘制sigmoid函数的图像:

```python
x = np.arange(-5.0, 5.0, 0.1) 
y = sigmoid(x) 
plt.plot(x, y) 
plt.ylim(-0.1, 1.1) # 指定y轴的范围 
plt.show()
```

<p>这样就得到sigmoid函数的图像：</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_sigmoid.png" width="350" height align="center"></p>
<h4 id="3-2-5-sigmoid函数和阶跃函数的比较"><a href="#3-2-5-sigmoid函数和阶跃函数的比较" class="headerlink" title="3.2.5 sigmoid函数和阶跃函数的比较"></a>3.2.5 sigmoid函数和阶跃函数的比较</h4><p><img src="http://lishengyu.xyz/dl_from_scratch_sigmoid2.png" width="350" height align="center/"></p>
<p>如图是sigmoid函数和阶跃函数的对比。首先发现是“平滑性”的不同。sigmoid函数是一条平滑的曲线，输出随着输入发生连续性的变化。而阶跃函数以0为界，输出发 生急剧性的变化。sigmoid函数的平滑性对神经网络的学习具有重要意义。</p>
<p>另一个不同点是，相对于阶跃函数只能返回0或1，sigmoid函数可以返 回0.731 …、0.880 …等实数（这一点和刚才的平滑性有关）。也就是说，感知机中神经元之间流动的是0或1的二元信号，而神经网络中流动的是连续 的实数值信号。</p>
<p>阶跃函数和sigmoid函数虽然在平滑性上有差异，但是如果从宏观视角看图，可以发现它们具有相似的形状。实际上，两者的结构均是“输入小时，输出接近0（为0）； 随着输入增大，输出向1靠近（变成1）”。也就是说，当输入信号为重要信息时，阶跃函数和sigmoid函数都会输出较大的值；当输入信号为不重要的信息时， 两者都输出较小的值。还有一个共同点是，不管输入信号有多小，或者有多 大，输出信号的值都在0到1之间。</p>
<h4 id="3-2-6-非线性函数"><a href="#3-2-6-非线性函数" class="headerlink" title="3.2.6 非线性函数"></a>3.2.6 非线性函数</h4><p><strong>神经网络的激活函数必须使用非线性函数。</strong></p>
<p>线性函数的问题在于，不管如何加深层数，总是存在与之等效的“无隐藏层的神经网络”。使用线性函数时，无法发挥多层网络带来的优势。因此，为了发挥叠加层所带来的优势，激活函数必须使用非线性函数。</p>
<h4 id="3-2-7-ReLU函数"><a href="#3-2-7-ReLU函数" class="headerlink" title="3.2.7 ReLU函数"></a>3.2.7 ReLU函数</h4><p>在神经网络发展的历史上，sigmoid函数很早就开始被使用了，而最近则主要使用ReLu(Rectified Linear Unit)函数。</p>
<p>ReLU函数在输入大于0时，直接输出该值，输入小于等于0时，输出0。</p>
<p>函数表达式如下：</p>

$$h(x)= \begin{cases}
x & (x > 0 )\\
0 & (x \leq 0 )
\end{cases}$$

它的图像如下：</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_relu.png" width="350" height align="center"></p>
<p>ReLU的实现也很简单，可以写成如下的式子：

```python
def relu(x):
    return np.maximum(0,x)
```

代码里使用了NumPy的`maximum`函数。`maximum`函数会从输入的数值中选择较大的那个值进行输出。</p>
<h3 id="3-3-多维数组的运算"><a href="#3-3-多维数组的运算" class="headerlink" title="3.3 多维数组的运算"></a>3.3 多维数组的运算</h3><h4 id="3-3-1神经网络的内积"><a href="#3-3-1神经网络的内积" class="headerlink" title="3.3.1神经网络的内积"></a>3.3.1神经网络的内积</h4><p>下面用numpy矩阵来实现神经网络，这里以下图的简单神经网络为对象。这个神经网络省略了偏置与激活函数，只有权重。<br><img src="http://lishengyu.xyz/dl_from_scratch_numpy.png" alt></p>
<p><strong>实现神经网络时，要注意X、Y、W的形状，特别是X和W的对应维度的元素个数是否一致</strong>

```python
>>> X=np.array([1,2])
>>> X.shape
(2,)
>>> W=np.array([[1,3,5],[2,4,6]])
>>> print(W)
[[1 3 5]
 [2 4 6]]
```

如上所示，使用`np.dot`（多维数组的点积），可以一次性计算出Y的结果。 这意味着，即便Y的元素个数为100或1000，也可以通过一次运算就计算出结果！</p>
<h3 id="3-4-三层神经网络的实现"><a href="#3-4-三层神经网络的实现" class="headerlink" title="3.4 三层神经网络的实现"></a>3.4 三层神经网络的实现</h3><p>这里我们以下图的3层神经网络为对象，实现从输入到输出的(前向)处理。</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_nn1.png" width="350" height align="center"></p>
<h4 id="3-4-1-符号确认"><a href="#3-4-1-符号确认" class="headerlink" title="3.4.1 符号确认"></a>3.4.1 符号确认</h4><p>如图所示：</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_nn2.png" width="350" height align="center"></p>

图中只突出显示了从输入层神经元$x<em>2$到最后一层的神经元$a^{(1)}</em>{1}$的权重。</p>
<p>如图，权重和隐藏层的神经元的右上角有一个“(1)”，它表示权重和神经元的层号<br>（即第一层的权重，第一层的神经元）。</p>
<p>此外，权重的右下角有两个数字，它们是最后一层的神经元和前一层的神经元的索引号。</p>

例如，$w^{(1)}_{12}$表示表示前一层的第二个神经元$x_2$到后一层的第一个神经元$a_1^{(1)}$的权重。权重右下角按照“后一层的索引号，前一层的索引号”的顺序排列。</p>
<h4 id="3-4-2-各层间信号传递的实现"><a href="#3-4-2-各层间信号传递的实现" class="headerlink" title="3.4.2 各层间信号传递的实现"></a>3.4.2 各层间信号传递的实现</h4><p>现在来看从输入层到第一层的第一个神经元的信号传递过程，如图：</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_nn3.png" width="350" height align="center"></p>
<p>图中增加了表示偏置的神经元“1”。</p>

$a_1^{(1)}$通过加权信号和偏置的和按如下方式计算：</p>

$$a_1^{(1)}=w^{(1)}_{11}x_1+w^{(2)}_{12}x_2+b^{(1)}_1$$

<p>此外，如果使用矩阵的乘法运算，就可以将第一层的加权和表示成如下的式子：</p>

$$A^{(1)}=XW^{(1)}+B^{(1)}$$

其中，$A^{(1)}$、$X$、$W^{(1)}$如下所示：</p>

$$A^{(1)}=(a_1^{(1)},a_2^{(1)},a_3^{(1)})$$

$$X=(x_1,x_2)$$

$$B^{(1)}=(b_1^{(1)},b_2^{(1)},b_3^{(1)})$$

$$
W^{(1)}=\left[
 \begin{matrix}
   w_{11}^{(1)} & w_{21}^{(1)} & w_{31}^{(1)} \\
   w_{12}^{(1)} & w_{22}^{(1)} & w_{32}^{(1)}   
  \end{matrix} 
\right]$$

下面用numpy多维数组实现$A^{(1)}=XW^{(1)}+B^{(1)}$，为了方便，这里将输入信号、权重、偏置设置成任意值

```python
# (2,1)
X=np.array([1.0,0.5])
# (2,3)
W1=np.array([0.1,0.2,0.3],[0.3,0.4,0.5])
# (3,1)
B1=np.array([0.1,0.2,0.3])

A1=np.dot(X,W1)+B1
```

<p>接下来就是第一层中激活函数的计算过程，如图所示：</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_nn4.png" width="350" height align="center"></p>
<p>图中，隐藏层的加权和（加权信号和偏置的总和）用a表示，被激活函数转换后的信号用z表示，此外h(x)表示激活函数，这里使用sigmoid函数，代码如下：

```python
# (3,1)
Z1=sigmoid(A1)
```

<p>下面接着实现第一层到第二层的信号传递，如图：</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_nn5.png" width="350" height align="center"></p>

```python
# (3,2)
W2=np.array([[0.1,0.4],[0.2,0.5],[0.3,0.6]])
# (2,1)
B2=np.array([0.1,0.2])

A2=np.dot(Z1,W2)+B2
Z2=sigmoid(A2)
```

<p>最后是第二层到输出层的信号传递，如图：</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_nn6.png" width="350" height align="center"></p>
<p>代码如下：

```python
def identity_function(x):
    return x   

W3=np.array([0.1,0.3],[0.2,0.4])
B3=np.array([0.1,0.2])

A3=np.dot(Z3,W3)+B3
Y=identity_function(A3)
```

这里定义了<code>identity_function()</code>函数（也称为“恒等函数”），并将其作为输出层的激活函数。恒等函数会将输入按原样输出，因此，这个例子中没有必要特意定义<code>identity_function()</code>。这里这样实现只是为了和之前的流程保持统一。另外，图中，输出层的激活函数用σ()表示，不同于隐 藏层的激活函数h()（σ读作sigma）。</p>
<p><strong>注：输出层所用的激活函数，要根据求解问题的性质决定。一般地，回 归问题可以使用恒等函数，二元分类问题可以使用sigmoid函数， 多元分类问题可以使用softmax函数</strong></p>
<h4 id="3-4-3-代码实现小结"><a href="#3-4-3-代码实现小结" class="headerlink" title="3.4.3 代码实现小结"></a>3.4.3 代码实现小结</h4><p>之前已经实现了3层网络的设计，现在重新整理一下。按照神经网络的实现惯例，只把权重记为大写字母W1，其他都用小写字母表示。

```python
def init_network():
  network={}
  network['W1']=np,array([[0.1, 0.3, 0.5], [0.2, 0.4, 0.6]]) 
  network['b1'] = np.array([0.1, 0.2, 0.3])    
  network['W2'] = np.array([[0.1, 0.4], [0.2, 0.5], [0.3, 0.6]])    
  network['b2'] = np.array([0.1, 0.2])    
  network['W3'] = np.array([[0.1, 0.3], [0.2, 0.4]])
  network['b3'] = np.array([0.1, 0.2])
  return network



def forward(network,x):
  W1,W2,W3 = network['W1'], network['W2'], network['W3']
  b1,b2,b3=network['b1'], network['b2'], network['b3']
```

<h3 id="3-5-输出层的设计"><a href="#3-5-输出层的设计" class="headerlink" title="3.5 输出层的设计"></a>3.5 输出层的设计</h3><p>神经网络可以用在分类和回归上。一般，分类问题用softmax，回归问题用恒等函数。</p>
<h4 id="3-5-1-恒等函数与softmax函数"><a href="#3-5-1-恒等函数与softmax函数" class="headerlink" title="3.5.1 恒等函数与softmax函数"></a>3.5.1 恒等函数与softmax函数</h4><p>恒等函数将输入按原样输出。所以在输出层用恒等函数，输入信号会原封不动输出。将恒等函数处理过程用神经网络图表示如下：</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_softmax.png" alt></p>
<p>softmax函数表达式如下：</p>

$$y_k = \frac{exp(a_k)}{\sum^n_{i=1}exp(a_i)}$$

上式表示输出层一共有$n$个神经元，计算第$k$个神经元的输出$y_k$。softmax函数的分子是输入信号$a_k$的指数，分母是所有输入信号的指数之和。下面是softmax的示意图，可以看到函数的输出通过箭头与所有的输入信号相连。</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_softmax1.png" alt></p>
<p>下面是softmax的实现：</p>

```python
def softmax(a):
  exp_a=np.exp(a)
  sum_exp_a=np.sum(exp_a)
  y=exp_a / sum_exp_a
  return y
```

<p>上面的代码虽然实现了softmax，但是在计算机运算中可能会发生溢出。函数实现中要进行指数运算，但此时指数的值很容易变得非常大，如果在超大值之间进行除法运算，结果会出现“不确定”的情况。</p>
<p>因此，需要对softmax进行改进：</p>

$$y_k = \frac{exp(a_k)}{\sum^n_{i=1}exp(a_i)}= \frac{C \cdot \ exp(a_k)}{C \cdot \sum^n_{i=1}exp(a_i)}=\frac{exp(a_k)+\log C}{\sum^n_{i=1} exp(a_i+ \log C)} = \frac{exp(a_k+C_1)}{\sum^n_{i=1} exp(a_i+C_1)}$$

<p><strong>注：C是一个任意常数</strong></p>

通过上式能够说明，加上或减去某个常数并不会改变运算的结果，$C_1$可以用任何值，但为了防止溢出，一般使用输入信号中的最大值。</p>
<p>对上面的代码进行改进：</p>

```python
def softmax(a):
  c=np.max(a)
  exp_a=np.exp(a-c) #溢出对策
  sum_exp_a=np.sum(exp_a)
  y=exp_a / sum_exp_a
  return y
```
<h4 id="3-5-2-softmax函数的特征"><a href="#3-5-2-softmax函数的特征" class="headerlink" title="3.5.2 softmax函数的特征"></a>3.5.2 softmax函数的特征</h4><p>softmax输出的是0到1之间的实数，并且函数的输出值总和为1。因此，每一个输入对应的softmax输出就是它的概率。</p>
<h3 id="3-6-手写字体识别"><a href="#3-6-手写字体识别" class="headerlink" title="3.6 手写字体识别"></a>3.6 手写字体识别</h3><h4 id="3-6-1-MNIST数据集"><a href="#3-6-1-MNIST数据集" class="headerlink" title="3.6.1 MNIST数据集"></a>3.6.1 MNIST数据集</h4><p>MNIST数据集是由0到9的数字构成的，如下图所示：</p>
<p><img src="http://lishengyu.xyz/dl_from_scratch_MNIST.png" alt></p>
<p>训练图像有6万张，测试图像有1万张。MNIST的图像数据是28像素X28像素的灰度图像，各个像素的取值是在0到255之间，每一个图像数据都相应标有“1”，“2”等标签。</p>
<p>书中提供了一个能够将MNIST数据集转化成Numpy数组的脚本<code>mnist.py</code>。使用其中的<code>load_mnist()</code>函数，就可以读入MNIST数据：</p>

```python
import sys, os

from mnist import load_mnist

(x_train,t_train),(x_test) = load_mnist(flatten=True,normalize=False)

# 输出各个数据的形状
print(x_train.shape) # (60000,784)
print(t_train.shape) # (6000,)
print(x_test.shape) # (10000,784)
print(t_test.shape) # (10000,)
```

<code>load_data()</code>函数以“（训练图像，训练标签）”，“（测试图像，测试标签）”的形式返回读取的MNIST数据。<code>load_data()</code>有三参数：</p>
<ol>
<li>normalize设置是否将输入图片正规化为0.0~1.0的值。如果设置为False，输入图像的像素会保持原来的0~255。</li>
<li>flatt设置是否将图片展成一维，也就是784个元素构成的一维数组。如果设置为False，则输入图像是1<em>28</em>28的三维数组。</li>
<li>第三个参数one_hot_label是将标签设置为onehot表示。onehot表示仅将正确的标签标记为1，其余标记为0。  </li>
</ol>
<p>导入数据后，接下来显示MNIST的图像。图像的显示使用PIL模块。</p>

```python
import sys,os
sys.path.append(os.pardir)
import numpy as np
from dataset.mnist import load_mnist
from PIL import Image

def img_show(img):
  pil_img = Image.fromarray(np.uint8(img))
  pil_img.show()

(x_train,t_train),(x_test,t_test) = load_mnist(flatten=True,normalize=False)

img = x_train[0]
label = t_train[0]
print(label) # 5

print(img.shape) # (784,)
img = img.reshape(28,28) # 将图像的形状变成原来尺寸

img_show(img)
```

需要注意的是，<code>flatten=True</code> 时读入图像是以一维Numpy数组形式保存的。所以，显示图像时需要把它变成28像素*28像素的形状，可以通过<code>reshape()</code>方法的参数指定期望的形状。此外还需将Numpy数组转成PIL用的数据对象，此转换需要<code>Image.fromarray()</code>完成。</p>
<h4 id="3-6-2-神经网络的推理处理"><a href="#3-6-2-神经网络的推理处理" class="headerlink" title="3.6.2 神经网络的推理处理"></a>3.6.2 神经网络的推理处理</h4><p>神经网络的输入层有784（28*28）个神经元，输出层有10（数字0到9）个神经元。此外，这个神经网络有两个隐藏层。这两个隐藏层的神经元属于可以自己进行设置。这里设置第一个隐藏层有50个，第二个有100个。</p>
<p>下面定义<code>get_data()</code>、<code>init_network()</code>、<code>predict()</code>这三个函数：</p>

```python
def get_data():
  (x_train, t_train), (x_test, t_test) = load_mnist(normalize=True, flatten=True, one_hot_label=False)
  return x_test, t_test
```
```python
def init_network():
  with open("sample_weight.pkl",'rb') as f:
    network = pickle.load(f)
  return network
```

```python
def predict(network, x):
  W1, W2, W3 = network['W1'], network['W2'], network['W3']
  b1, b2, b3 = network['b1'], network['b2'], network['b3']
  a1= np.dot(x, W1)+ b1
  z1 = sigmoid(a1) 
  a2= np.dot(z1, W2)+ b2
  z2 = sigmoid(a2)
  a3= np.dot(z2, W3)+ b3
  y = softmax(a3)

  return y
```



</html>
