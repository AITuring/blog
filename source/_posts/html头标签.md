---
title: HTML头标签
date: 2020-03-27 11:53:12
tags: [HTML,前端]
categories: [HTML]
---
<img src="http://lishengyu.xyz/pubgm/2020-03-13 170130.jpg" >

## HTML头标签
### 1. !DOCTYPE
`DocType Declaration`，简称DTD。此标签可告知浏览器文档使用哪种 HTML 或 XHTML 规范。
`<!DOCTYPE>` 声明必须是 HTML 文档的第一行，位于标签之前。
<!DOCTYPE html>

HTML 5：`<!DOCTYPE html>`


### 2.头标签

下面是一个html5的骨架：
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
	<meta name="Author" content="">
    <meta name="Keywords" content="牛逼，很牛逼，特别牛逼" />
    <meta name="Description" content="网易是中国领先的互联网技术公司，为用户提供免费邮箱、游戏、搜索引擎服务，开设新闻、娱乐、体育等30多个内容频道，及博客、视频、论坛等互动交流，网聚人的力量。" />
    <title>Document</title>
</head>
<body>

</body>
</html>
```
头标签都放在头部分之间。包括：`<title>`、`<base>`、`<meta>`、`<link>`

- `<title>`：指定整个网页的标题，在浏览器最上方显示。
- `<base>`：为页面上的所有链接规定默认地址或默认目标。
- `<meta>`：提供有关页面的基本信息
- `<link>`：定义文档与外部资源的关系。

#### 2.1 meta 标签

常见的几种 meta 标签如下：

##### 2.1.1 字符集 charset

```html
<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
```
字符集用meta标签中的charset定义，meta表示“元”。“元”配置，就是表示基本的配置项目。

charset就是charactor set（即“字符集”）。

浏览器就是通过meta来看网页是什么字符集的。比如你保存的时候，meta写的和声明的不匹配，那么浏览器就是乱码。

##### 2.1.2 视口 viewport

浏览器的 viewport 是可以看到Web内容的窗口区域，通常与渲染出的页面的大小不同，这种情况下，浏览器会提供滚动条以滚动访问所有内容。

窄屏幕设备（如移动设备）在一个虚拟窗口或视口中渲染页面，这个窗口或视口通常比屏幕宽；然后缩小渲染的结果，以便在一屏内显示所有内容。然后用户可以移动、缩放以查看页面的不同区域。例如，如果移动屏幕的宽度为640px，则可能会用980px的虚拟视口渲染页面，然后缩小页面以适应640px的窗口大小。

这样做是因为许多页面没有做移动端优化，在小窗口渲染时会乱掉（或看起来乱）。所以，这种虚拟视口是一种让未做移动端优化的网站在窄屏设备上看起来更好的办法。

一个典型的针对移动端优化的站点包含类似下面的内容：
```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
```
`width`属性控制视口的宽度。可以像`width=600`这样设为确切的像素数，或者设为 `device-width` 特殊值，代表缩放为 100% 时以 CSS 像素计量的屏幕宽度。（相应的也有`height`及`device-height`属性，可能对包含基于视口高度调整大小及位置的元素的页面有用。）

`initial-scale` 属性控制页面最初加载时的缩放等级。`maximum-scale`、`minimum-scale`及`user-scalable`属性控制允许用户以怎样的方式放大或缩小页面。

##### 2.1.3 内容 content

1.定义“关键词”：

举例如下：
```html
<meta name="Keywords" content="网易,邮箱,游戏,新闻,体育,娱乐,女性,亚运,论坛,短信" />
```
这些关键词，就是告诉搜索引擎，这个网页是干嘛的，能够提高搜索命中率。让别人能够找到你，搜索到你。

   定义“页面描述”：

meta除了可以设置字符集，还可以设置关键字和页面描述。

只要设置Description页面描述，那么百度搜索结果，就能够显示这些语句，这个技术叫做SEO（search engine optimization，搜索引擎优化）。

设置页面描述的举例：
```html
<meta name="Description" content="网易是中国领先的互联网技术公司，为用户提供免费邮箱、游戏、搜索引擎服务，开设新闻、娱乐、体育等30多个内容频道，及博客、视频、论坛等互动交流，网聚人的力量。" />
```
```html
<meta http-equiv="refresh" content="3;http://www.baidu.com">
```
上面这个标签的意思是说，3秒之后，自动跳转到百度页面。





#### 2.2 base标签
```html
<base href="/">
```
base 标签用于指定基础的路径。指定之后，所有的 a 链接都是以这个路径为基准。