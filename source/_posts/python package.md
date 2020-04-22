---
title: python package
date: 2019-12-31 14:24:12
tags: [python]
categories: [python]
---
<img src="http://lishengyu.xyz/tu106.jpg" alt></p>
<h3 id="package与module间的关系"><a href="#package与module间的关系" class="headerlink" title="package与module间的关系"></a>package与module间的关系</h3><p><code>Python</code>是通过<code>module</code>来组织代码的，一个<code>module</code>就是一个<code>.py</code>文件，<code>module</code>又是通过 <code>package</code>来组织的，<code>package</code> 是一个包含 <code>__init__.py</code>的文件夹。</p>
<p>代码，<code>module</code>，<code>package</code>它们三者的关系就是：<code>module</code> 包含代码，<code>package</code> 至少包含一个为 <code>__init__.py</code> 的 <code>module</code>。</p>
<p><img src="http://lishengyu.xyz/package.png" alt><br>例如：

```
package
├── __init__.py
├── submodule.py
└── subpackage
    └── __init__.py
```

<p><code>Python</code> 的 <code>package</code> 以及 <code>package</code> 中的<code>__init__.py</code> 共同决定了 <code>package</code> 中的 <code>module</code> 是如何被外界访问的。</p>
<h3 id="空的-init-py文件"><a href="#空的-init-py文件" class="headerlink" title="空的 __init__.py文件"></a>空的 <code>__init__.py</code>文件</h3><p>不包含任何代码的 <code>__init__.py</code> 只用来标识一个文件夹是一个 <code>package</code>，而 <code>package</code> 是可以被导出的。</p>

```python
from package import item
```

<p>此处的 <code>item</code> 可以是 <code>package</code> 中包含的 <code>submodule</code> 或 <code>subpackage</code>。</p>

```python
>>> from package import submodule
>>> from package import subpackage
```

<h4 id="如果-init-py-不为空"><a href="#如果-init-py-不为空" class="headerlink" title="如果__init__.py 不为空"></a>如果<code>__init__.py</code> 不为空</h4><p>如果<code>__init__.py</code> 不为空,其中包含的任何变量，包括 <code>function</code>、<code>class</code>、<code>variable</code> 以及 任何被导入的 <code>module</code> 都可以通过 <code>package</code> 导出。

```python
from package import item
```

<p>此处的 <code>item</code> 可以是 <code>__init__.py</code> 中的任何变量。</p>
<h3 id="package-的初始化工作"><a href="#package-的初始化工作" class="headerlink" title="package 的初始化工作"></a><code>package</code> 的初始化工作</h3><p>一个 <code>package</code> 被导入，不管在什么时候 <code>__init__.py</code> 中的代码只执行一次。</p>

```python
>>> import package
hello world
>>> import package
>>> import package
```

<p>由于<code>package</code>被导入时<code>__init__.py</code>中的可执行代码会被执行，所以小心在<code>package</code> 中放置你的代码，尽可能消除它们产生的副作用，比如把代码尽可能的进行封装成函数或类。</p>
<h3 id="从-package-中导入变量的顺序"><a href="#从-package-中导入变量的顺序" class="headerlink" title="从 package 中导入变量的顺序"></a>从 package 中导入变量的顺序</h3>

```python
from package import item
```

<p><code>import</code> 语句首先检查 <code>item</code> 是否是 <code>__init__.py</code> 中定义的变量，然后检查其是不是一个 <code>subpackage</code>，如果不是再去检查其是不是一个 <code>module</code>，都不是将抛出 <code>ImportError</code>。</p>
<p>在 <code>import item.subitem.subsubitem</code> 语句时，除了最后一个 <code>subsubitem</code> 之外其他 <code>item</code> 都必须是 <code>package</code>，而最后一个 <code>subsubitem</code> 必须是一个 <code>package</code> 或者 <code>module</code>，不能是他前一个 <code>item</code> 定义的 <code>function、class、variable</code>。</p>
<h4 id="使用-导入"><a href="#使用-导入" class="headerlink" title="使用 * 导入"></a>使用 * 导入</h4><p>在 <code>from package import *</code> 语句中，如果 <code>__init__.py</code> 中定义了 <code>__all__</code> 变量，一个 <code>list</code>，仅仅只有这个 <code>list</code> 中定义的 <code>submodule</code>或者变量将会被导出。</p>
<p>如果 <code>__init__.py</code> 中没有<code>__all__</code> 变量，导出将按照以下规则执行：</p>
<ol>
<li>此 <code>package</code> 被导入，并且执行 </li>
<li><code>__init__.py</code> 中可被执行的代码</li>
<li><code>__init__.py</code> 中定义的 <code>variable</code> 被导入</li>
<li><code>__init__.py</code> 中被显式导入的 <code>module</code> 被导入</li>
</ol>

 