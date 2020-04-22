---
title: HTML基础
date: 2020-02-21 17:47:12
tags: [HTML,前端]
categories: [HTML]
---
<img src="http://lishengyu.xyz/1573191879821.jpeg" alt>

## HTML
### HTML常见元素
#### head区的元素
在head中，不会在页面上留下内容
- `meta`
- `title`
- `style`
- `link`
- `script`
- `base`

#### body区内容
在body中，会出现在页面上
- `div`/`section`/`article`/`aside`/`header`/`footer`
- `p`
- `span`/`em`(斜体)/`strong`(粗体)
- `table`/`tbody`/`tr`(行)/`td`(数据格)/`th`(表头)/`caption`(标题)

table有一系列属性：
border是表格的边框粗细，cellspacing是单元格之间的空隙
，cellpadding是单元格与内容的距离，align是对齐方式，默认为左，width是整个表格的宽度，每一列平分 

```html
<table border="1">
    <tr>
        <th>Header 1</th>
        <th>Header 2</th>
    </tr>
    <tr>
        <td>row 1, cell 1</td>
        <td>row 1, cell 2</td>
    </tr>
    <tr>
        <td>row 2, cell 1</td>
        <td>row 2, cell 2</td>
    </tr>
</table>


```
![](https://www.runoob.com/wp-content/uploads/2013/07/CB476DA7-7279-4892-A424-657772E385BA.jpg)

- `ul`(无序列表)/`ol`(有序列表)/`li`(列表项)/`dl`(定义列表)/`dt`(定义列表项目)/`dd`(自定义列表项目的描述)

`ul`有属性`type`,默认是实心圆点，square是小方块，cicle是空心圆
```html
<!-- 无序列表 -->
<ul>
    <li>milk</li>
</ul>
<!-- 有序列表 -->
<ol>
    <li>milk</li>
    <li>coffee</li>
</ol>
<!-- 自定义列表 -->
<!-- 自定义列表以 <dl> 标签开始。每个自定义列表项以 <dt> 开始。每个自定义列表项的定义以 <dd> 开始。 -->
<dl>
    <dt>coffee</dt>
    <dd>- black hot drink</dd>
    <dt>milk</dt>
    <dd>- white cold drink</dd>

</dl>

浏览器显示如下：
Coffee
- black hot drink
Milk
- white cold drink
```
- `a`
- `form`/`input`(输入框)/`select`(下拉框)/`textarea`(文本输入区)/`button`

#### 一些常用元素
1. `<meta charset="utf-8">`

表示页面使用了`utf-8`字符集

2. `<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=no">`

视口(页面的尺寸)宽度等于设备宽度，初始化缩放和最大缩放为1，用户不能缩放。**给页面适配移动端的第一步就是加上viewpoint**。

3.`<base href="/">`

指定基础路径，所有链接都以此路径为基础计算

#### HTML重要属性
- a[href,target]
`href`指链接地址，`target`指在哪里打开链接，默认是`self`，在当前窗口打开，可以设置为`blank`在新页面打开

```html
<body>
    <section>
        <h3>链接</h3>
        <a href="https://www.github.com/">github</a>
        <a href="https://www.google.com" target="_blank">google</a>
    </section>
</body>
```
<body>
    <section>
        <h3>链接</h3>
        <a href="https://www.github.com/">github</a>
        <a href="https://www.google.com" target="_blank">google</a>
    </section>
</body>

- img[src,alt,title]
`src`是图片地址，`alt`是图片链接不可用时，解释图片的文字，`title`是鼠标滑到图片上的提示

- table td[colspan,rowspan]
`colspan`和`rowspan`按照行，列合并单元格

```html
<table align="center" border="1" width="300" >
        <!-- 标题-->
        <caption>测试</caption>
        <tr>
            <!-- 表头 -->
            <th>这是表头1</th>
            <th>这是表头2</th>
            <th>这是表头3</th>
        </tr>
        <tr>
            <td align="center" colspan="3">列合并</td>
            <!-- <td>2</td>
            <td>3</td> -->
        </tr>
        <tr>
            <!-- 第一列写了合并之后，后面几行的对应列就应该删除 -->
            <td rowspan="2">1</td>
            <td>2</td>
            <td>3</td>
        </tr>
        <tr>
            <!-- <td>4</td> -->
            <td>5</td>
            <td>6</td>
        </tr>
</table>
```
![](http://lishengyu.xyz/htmltable.png)

- form[action,method,enctype]
`action`指表单提交的地方。`method`指表单提交的方式，有GET(获取内容)和POST(提交内容),`enctype`是post用什么编码

- input[type,value]
输入框
- select>option[value]
下拉框

```html
<body>
    <section>
        <h3>表单</h3>
        <form method="GET" action="https://www.qq.com">
        <p>
            <select name="select1">
                <option value="1">一</option>
                <option 
                value="2" selected>二</option>
                <!-- 当option中有selected，它默认是被选中的 -->
            </select>
        </p>
    </section>
</body>
```
<body>
    <section>
        <h3>表单</h3>
        <form method="GET" action="https://www.qq.com">
        <p>
            <select name="select1">
                <option value="1">一</option>
                <option 
                value="2" selected>二</option>
                <!-- 当option中有selected，它默认是被选中的 -->
            </select>
        </p>
    </section>
</body>

- `<label for="">`
如果有`<label for>`属性，点击文字就能进行选择，如果没有，就必须点击文字前面的空心圆才行。

**注意：HTML中id是不能重复的**

```html
<form>
    <input type="radio" name="radio1" id="radio1-1"/>
    <label for="radio1-1">选项一</label>
    <input type="radio" name="radio1" id="radio1-2"/>
    <label ">选项二</label>

</form>
```

<form>
    <input type="radio" name="radio1" id="radio1-1"/>
    <label for="radio1-1">选项一</label>
    <input type="radio" name="radio1" id="radio1-2"/>
    <label ">选项二</label>

</form>










  