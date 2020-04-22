---
title: HTML表单
date: 2020-02-21 11:44:12
tags: [HTML,前端]
categories: [HTML]
---
<img src="http://lishengyu.xyz/mmexport1571830223208.jpg" alt>

## HTML表单
HTML表单用于收集用户输入，表单使用`<form>`元素表示。

### `<input>`
`<input>`根据不同的type类型有不同形态。

| 类型 | 描述 | 
| :-----:| :----: | 
| text | 常规文本输入 | 
| radio | 单选按钮 | 
| submit | 提交表单 | 

#### `<input type="text">`

```html
<!DOCTYPE html>
<html>
<body>

<form>
First name:<br>
<input type="text" name="firstname">
<br>
Last name:<br>
<input type="text" name="lastname">
</form>

<p>请注意表单本身是不可见的。</p>

<p>同时请注意文本字段的默认宽度是 20 个字符。</p>

</body>
</html>
```
浏览器中看起来如下图：

![](http://lishengyu.xyz/formtext.png)

#### `<input type="radio">`

同一组单选框的name属性要一致
```html
<form>
<input type="radio" name="sex" value="male" checked>Male
<br>
<input type="radio" name="sex" value="female">Female
</form> 

```

浏览器中看起来如下图：

![](http://lishengyu.xyz/formradio.png)

当name不一致时，他们就不属于一组了，也就不是单选了：

```html
<form>
<input type="radio" name="sex1" value="male" checked>Male
<br>
<input type="radio" name="sex" value="female">Female
</form> 
```

<form>
<input type="radio" name="sex1" value="male" checked>Male
<br>
<input type="radio" name="sex" value="female">Female
</form> 

#### `<label for="">`
如果有`<label for>`属性，点击文字就能进行选择，如果没有，就必须点击文字前面的空心圆才行。

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


#### `<input type="submit">`

```html
<form action="action_page.php">
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit">
</form> 
```
浏览器中看起来如下图：

![](http://lishengyu.xyz/formsubmit.png)

### `action`

`action`定义提交表单时执行的动作。在上面例子中，指定了某个服务器脚本来处理被提交的表单：

```html
<form action="action_page.php" >
```
如果省略`action`属性，则`action`会被设置为当前页面。

### `method`

`method`规定了表单提交时所用的HTTP方法，一般为`GET`或`POST`。

#### GET(默认)
- 如果表单提交是被动的（比如搜索引擎查询），并且没有敏感信息使用GET。

- 使用 GET 时，表单数据在页面地址栏中是可见的：
    ```html
    action_page.php?firstname=Mickey&lastname=Mouse
    ```
- 少量数据的提交时用GET。浏览器会设定容量限制。

#### POST
如果表单正在更新数据，或者包含敏感信息（例如密码）使用POST。相比于GET，POST 更加安全，因为在页面地址栏中被提交的数据是不可见的。

### name

如果要正确地被提交，每个输入字段必须设置一个 name 属性。

本例只会提交 "Last name" 输入字段：

```html
<form action="action_page.php">
First name:<br>
<input type="text" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit">
</form> 
```
<form action="action_page.php">
First name:<br>
<input type="text" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit">
</form> 

### `<fieldset>` 
`<fieldset>` 元素组合表单中的相关数据

`<legend>` 元素为 `<fieldset>` 元素定义标题。

实例:
```html
<form action="action_page.php">
<fieldset>
<legend>Personal information:</legend>
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit"></fieldset>
</form> 
```
<form action="action_page.php">
<fieldset>
<legend>Personal information:</legend>
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit"></fieldset>
</form> 



