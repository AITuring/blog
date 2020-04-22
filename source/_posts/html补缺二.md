---
title: HTML补缺二
date: 2020-03-03 15:43:12
tags: [HTML,前端]
categories: [HTML]
---
<img src="http://lishengyu.xyz/pubgm/IMG_5512.JPG" >


## HTML补缺二
### HTML5新增元素
- `<article>` 标签定义外部的内容（结构元素） 
- `<aside>`定义页面内容之外的内容。aside的内容与article的内容相关。（结构元素） 
- `<figure>`定义一组媒介内容的分组，以及它们的标题。（结构元素） 
- `<section>`标签定义文档中的节（section，区段）。比如章节，页眉，页脚或文档中的其他部分（结构元素） 
- `<meter>`定义预定义范围内的度量。仅用于已知最大和最小值的度量（内联元素） 
- `<progress>`定义任何类型的任务的进度。可以使用`<progress>`标签来显示javascript中耗费时间的函数的进度（内联元素）
- `<time>`定义一个日期/时间 （内联元素） 
- `<audio>`定义声音内容。(内嵌元素) audio 元素允许多个 source 元素。source 元素可以链接不同的音频文件。浏览器将使用第一个可识别的格式 
- `<video>`定义视频。(内嵌元素) Ogg支持firefox3.5，opera10.5，chrome3.0 Mpeg 4 支持chrome3.0，safsri3.0 Video也支持多个source元素，链接到不同的视频文件，浏览器将使用第一个可识别的格式 属性值： autoplay=”autoplay”就绪后马上播放 loop=“loop”播放完再次播放 
- `<command>`定义命令按钮 （交互元素） 
- `<datalist>`定义下拉列表,与input元素配合使用该元素，定义input可能出现的值，datalist的选项不会被显示出来，它仅仅是合法的输入值列表（交互元素） 
- `<details>`定义元素的细节 （交互元素） 
- `<canvas>`定义图形,绘制路径，矩形，圆形，字符以及添加图像的方法 Canvas元素本身没有绘图能力，所有的绘制工作必须在javascript内部完成 
- `<dialog>`定义对话（会话）dialog元素表示几个人之间的对话。HTML5dt元素可以表示讲话者，HTML5dd元素可以表示讲话内容。（结构元素） 
- `<embed>`定义外部交互内容或插件 
- `<event-source>`为服务器发送的事件定义目标 
- `<footer>`定义 section 或 page 的页脚 
- `<figcaption>` 标签定义 figure 元素的标题。
- `<hgroup>` 标签用于对网页或区段（section）的标题进行组合。 对网页或区段的标题进行组合 
- `<keygen>`标签提供一种验证用户的可靠方法。keygen 元素是密钥对生成器（key-pair generator）。当提交表单时，会生成两个键，一个是私钥，一个公钥。私钥（private key）存储于客户端，公钥（public key）则被发送到服务器。公钥可用于之后验证用户的客户端证书（client certificate）。 
- `<header>`定义 section 或 page 的页眉（介绍信息）
-   `<mark>` 标签定义带有记号的文本。请在需要突出显示文本时使用。 
-  `<nav>`定义导航链接。 
-  `<output>`定义输出的一些类型。 
-  `<source>`定义媒体资源 Ogg支持firefox3.5，opera10.5，chrome3.0 Mpeg 4 支持chrome3.0，safari3.0 Video也支持多个source元素，链接到不同的视频文件，浏览器将使用第一个可识别的格式 属性值： autoplay=”autoplay”就绪后马上播放 loop=“loop”播放完再次播放 
-  `<ruby>` 标签定义 ruby 注释（中文注音或字符）在东亚使用

### HTML中的嵌套关系
#### 1. 块级元素可以包含行内元素

```html
<body>
    <div><a href="#">div & a</a></div>
</body>
```
<body>
    <div><a href="#">div & a</a></div>
</body>


#### 2. 块级元素不一定能包含块级元素

例如`<p>`中不能包含`<div>`

#### 3.行内元素一般不能包含块级元素

比如`<a>`可以包含块级元素`<div>`

```html
<body>
    <a href="#"><div>div & a</div></a>
</body>
```

<body>
    <a href="#"><div>div & a</div></a>
</body>

### HTML的默认样式

HTML中部分标签都有自己的样式。有时候我们并不想要这些默认样式，就可以使用CSS reset。将HTML所有标签的样式设为0.

```html
<style>
    *{
        margin:0;
        padding:0;
    }
</style>

```
然后就可以按照自己的想法去编写样式。

### HTML面试真题

#### 1.dectype的意义

1. 让浏览器以标准模式渲染
2. 让浏览器知道元素的合法性

#### 2.HTML XHTML HTML5关系

1. HTML属于SGML(标准通用标记语言（Standard Generalized Markup Language，SGML）是现时常用的超文本格式的最高层次标准，是可以定义标记语言的元语言，甚至可以定义不必采用< >的常规方式。 由于它的复杂，因而难以普及。)
2. XHTML属于XML，是HTML进行XML严格化的结果
3. HTML5不属于XML或SGML，比XHTML宽松

#### 3.HTML5有什么变化

1. 新的语义化的元素
2. 表单增强
3. 新的API（离线、音视频、图像、实时通信、本地存储、设备能力）
4. 分类和嵌套变更

#### 4. em和i有什么区别
1. em是语义化标签。表示强调
2. i是纯样式标签，表示斜体
3. HTML5中i不推荐使用，一般用作图标
   
#### 5.语义化的意义是什么

1. 开发者容易理解
2. 机器容易理解结构（搜索、读屏软件）
3. 有助于SEO
4. semantic microdata（）

#### 6.哪些元素可以自闭合

1. 表单input
2. 图片img
3. br hr
4. meta link
   
#### 7.HTML和DOM关系

1. HTML是“死的”
2. DOM是HTML解析来的，活的
3. js可以维护DOM

#### 8.property和attribute的区别

1. property是活的
2. attribute是死的

#### 9.form的作用

1. 直接提交表单
2. 使用submit/reset按钮
3. 便于浏览器保存表单
4. 第三方库可以整体提取值
5. 第三方库可以进行表单验证