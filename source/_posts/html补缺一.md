---
title: HTML补缺一
date: 2020-02-23 17:48:12
tags: [HTML,前端]
categories: [HTML]
---
<img src="http://lishengyu.xyz/340954867.gif" >
## HTML补缺一

### HTML默认样式分类
#### 块级 block
独占一行
`div`,`p`,`section`,`arctle`,`aside`,`h1(2,3,4,5,6)`,`ol`,`ul`,`dl`,`table`,`address`,`blockquote`,`form`

#### 行内 inline
一行之内，和文本相关
`span`,`em`,`strong`,`a`,`br`,`i`,`label`,`q`,`var`,`cite`,`code`

#### inline-block
对内像block，对外像inline。表单元素
`select`,`img`,`input`

### 空元素

一个空元素（empty element）可能是 `HTML`，`SVG`，或者 `MathML`里不具有任何子节点（即嵌套元素或文本节点）的元素.

在 HTML 中，在空元素上使用结束标签通常是无效的。例如，`<input type="text"></input>` 是无效的 HTML。

在 HTML 中有以下这些空元素：

1. `<area>`
2. `<base>`
3. `<br>`
4. `<col>`
5. `<colgroup>` when the span is present
6. `<command>`
7. `<embed>`
8. `<hr>`
9. `<img>`
10. `<input>`
11. `<keygen>`：该标签规定用于表单的密钥对生成器字段。当提交表单时，私钥存储在本地，公钥发送到服务器。
12. `<link>`
13. `<meta>`:提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。

`<meta>` 标签位于文档的头部，不包含任何内容。`<meta>` 标签的属性定义了与文档相关联的名称/值对。

14. `<param>`:允许用户为插入 XHTML 文档的对象规定 run-time 设置，也就是说，此标签可为包含它的 `<object>` 或者 `<applet>` 标签提供参数。

15. `<source>`:为媒介元素（比如 `<video>` 和 `<audio>`）定义媒介资源。

16. `<source>` 标签允许您规定可替换的视频/音频文件供浏览器根据它对媒体类型或者编解码器的支持进行选择。

17. `<track>`:为诸如 video 元素之类的媒介规定外部文本轨道。
用于规定字幕文件或其他包含文本的文件，当媒介播放时，这些文件是可见的。

18. `<wbr>`:Word Break Opportunity (<wbr>) 规定在文本中的何处适合添加换行符。
提示：如果单词太长，或者您担心浏览器会在错误的位置换行，那么您可以使用 <wbr> 元素来添加 Word Break Opportunity（单词换行时机）。

### Ajax和Flash
1.Ajax的优势：1.可搜索性 2.开放性 3.费用 4.易用性 5.易于开发。
2.Flash的优势：1.多媒体处理 2.兼容性 3.矢量图形 4.客户端资源调度
3.Ajax的劣势：1.它可能破坏浏览器的后退功能   2.使用动态页面更新使得用户难于将某个特定的状态保存到收藏夹中 ，不过这些都有相关方法解决。
4.Flash的劣势：1.二进制格式 2.格式私有 3.flash 文件经常会很大，用户第一次使用的时候需要忍耐较长的等待时间  4.性能问题

### 强调标签辨析
- `<mark>` 标签定义带有记号的文本。在需要突出显示文本时使用 `<mark>` 标签。例如：一个搜索结果展示页面，需要把搜索关键词高亮显示,这时候可以使用`<mark>`。

- `<em>` 把文本定义为强调的内容。 
- `<strong>` 把文本定义为语气更强的强调的内容。 
- HTML中没有`<highlight>`标签，但是CSS中有highlight 属性用来高亮显示指定的代码行

### 一些不常用标签
`<dfn>` 定义一个定义项目。 
`<code>` 定义计算机代码文本。 
`<samp>` 定义样本文本。 
`<kbd>` 定义键盘文本。它表示文本是从键盘上键入的。它经常用在与计算机相关的文档或手册中。 
`<var>` 定义变量。可以将此标签与 `<pre>` 及 `<code>` 标签配合使用。 
`<cite>` 定义引用。可使用该标签对参考文献的引用进行定义，比如书籍或杂志的标题。 

### html `video`

`<video>` 标签定义视频，比如电影片段或其他视频流。目前，`<video>` 元素支持三种视频格式：MP4、WebM、Ogg。例如：

```html
<video width="320" height="240" controls>
    <source src="movie.mp4" type="video/mp4">
    <source src="movie.ogg" type="video/ogg">
    您的浏览器不支持 video 标签。
</video>

`<video>`可以在开始标签和结束标签之间放置文本内容，这样老的浏览器就可以显示出不支持该标签的信息。

```
`video`标签有以下属性：

| 属性 | 值 | 描述 | 
| :-----:| :----: | :----: |
| autoplay | autoplay | 如果出现该属性，则视频在就绪后马上播放 |
| controls | controls | 如果出现该属性，则向用户显示控件，比如播放按钮。|
| height | pixels | 设置视频播放器的高度。|
| width | pixels | 设置视频播放器的宽度。|
| loop | loop | 如果出现该属性，则当视频文件完成播放后再次开始播放。|
| muted | muted | 如果出现该属性，视频的音频输出为静音。|
| poster | URL | 规定视频正在下载时显示的图像，直到用户点击播放按钮。|
| preload | auto,metadata,none | 如果出现该属性，则视频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。|
| src | URL | 要播放视频的URL。|

### HTML `<audio>`

和`video`标签类似，`<audio>` 标签定义声音，比如音乐或其他音频流。例如：

```html
<audio controls>
  <source src="horse.ogg" type="audio/ogg">
  <source src="horse.mp3" type="audio/mpeg">
  您的浏览器不支持 audio 元素。
</audio>
```

`<audio>`可以在开始标签和结束标签之间放置文本内容，这样老的浏览器就可以显示出不支持该标签的信息。

`audio`标签有以下属性：

| 属性 | 值 | 描述 | 
| :-----:| :----: | :----: |
| autoplay | autoplay | 如果出现该属性，则音频在就绪后马上播放 |
| controls | controls | 如果出现该属性，则向用户显示控件，比如播放按钮。|
| loop | loop | 如果出现该属性，则当音频文件完成播放后再次开始播放。|
| muted | muted | 如果出现该属性，视频的音频输出为静音。|
| preload | auto,metadata,none | 如果出现该属性，则音频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。|
| src | URL | 要播放音频的URL。|

### HTML `datalist`

类似于下拉框`select`,`<datalist>` 标签定义选项列表。与input 元素配合使用该元素，来定义 input 可能的值。datalist 及其选项不会被显示出来，它仅仅是合法的输入值列表。

```html
<input id="myCar" list="cars" />
<datalist id="cars">
  <option value="BMW">
  <option value="Ford">
  <option value="Volvo">
</datalist>
```
<input id="myCar" list="cars" />
<datalist id="cars">
  <option value="BMW">
  <option value="Ford">
  <option value="Volvo">
</datalist>

### HTML `<progress>`

`<progress>` 标签一般与 JavaScript 一同使用，来显示任务的进度。
但是`<progress>` 标签不适合用来表示度量衡（例如，磁盘空间使用情况或查询结果）。如需表示度量衡，请使用 `<meter>` 标签代替。

`<progress>`有两个参数，max规定任务一共需要多少工作。number规定已经完成多少任务。`<progress>`标签不填写max和value会自动滑动。如下：

<progress>




