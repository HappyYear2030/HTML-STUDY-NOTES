# HTML

## 标签

### [html](https://www.w3school.com.cn/tags/tag_html.asp)

```
<html>-</html>
```

此元素告知浏览器是一个HTML文档，标签之间限定了文档的开始点与结束点，在他们之间是文档的头部和主体。

### [head](https://www.w3school.com.cn/tags/tag_head.asp)

```
<head>-</head>
```

 此标签用于定义文档的头部，是所有头部元素的容器。

```
<base><link><meta><script><style><title>都可以用在head部分
其中<title>定义文档的标题，是head中唯一必须的元素。
```

#### 可选属性

##### profile

一个由空格分隔的URL列表，这些 URL 包含着**有关页面的元数据信息**。profile 属性提供了与当前文档相关联的配置文件的 URL。配置文件的格式以及浏览器使用它们的方式都还没有进行定义，这个属性主要是**为将来的开发而保留的占位符**。

### [base（空元素）](https://www.w3school.com.cn/tags/tag_base.asp)

```
<base/>
```

此标签为页面上的所有链接规定默认地址或默认目标。

通常情况下，浏览器会从当前文档的 URL 中提取相应的元素来填写相对 URL 中的空白。

#### 必需属性

##### href

```
<base href="     "/>
```

用于规定页面中所有相对链接的基准URL。

#### 可选的属性

##### target

```
<base target="    "/> 
```

用于规定在何处打开页面中所有的链接

###### 可选的属性值

```
_blank           
浏览器总在一个新打开、未命名的窗口中载入目标文档
_parent         
这个目标使得文档载入父窗口或者包含来超链接引用的框架的框架集。
_self   
这个目标的值对所有没有指定目标的 <a> 标签是默认目标，它使得目标文档载入并显示在相同的框架或者窗口中作为源文档。
_top
这个目标使得文档载入包含这个超链接的窗口，用 _top 目标将会清除所有被包含的框架并将文档载入整个浏览器窗口。
framename
```



### [link（空元素）](https://www.w3school.com.cn/tags/tag_link.asp)

```
<link/>
```

此标签定义文档与外部资源的关系，最常见的用途是链接样式表。

#### 可选的属性

##### charset（几乎没有主流的浏览器支持charset）

```
<link charset=""/>
```

用于规定被链接文档的字符编码方式。现代浏览器默认ISO-8859-1。

###### 可选的属性值

```
charater_set 

    UTF-8 - Unicode 字符编码
    ISO-8859-1 - 拉丁字母表的字符编码
    
在理论上，可以使用任何字符集，但并不是所有浏览器都能够理解它们。某种字符集使用的范围越广，浏览器就越有可能理解它。
```

##### herf

```
<link herf="    ">
```

用于规定被链接文档的位置

##### hreflang（几乎没有主流的浏览器支持hreflang）

```
<link hreflang="   ">
```

用于规定被链接文档的语言

###### 可选属性值

```
language_code
值为双字母的语言代码。
```

用于规定被链接文档的语言。

##### media

```
<link media="     ">
```

用于规定显示设备

###### 可选属性值

```
screen       计算机屏幕
tty          电传打字机以及类似的使用等宽字符网格的媒介
tv           电视机类型设备（低分辨率、有限的滚屏能力）。
projection   放映机
handheld     手持设备（小屏幕、有限带宽）
print        打印预览模式/打印页面
braille      盲人点字法反馈设备
aural        语音合成器
all 	     适用于所有设备
```

##### rel

```
<link rel="      ">
```

规定被链接的文档是一个样式表

###### 可选属性值

```
alternate    文档的替代版本（比如打印页、翻译或镜像）。
stylesheet   文档的外部样式表。
start 	     集合中的第一个文档。
next 	     集合中的下一个文档。
prev         集合中的上一个文档。
contents     文档的目录。
index        文档的索引。
glossary     在文档中使用的词汇的术语表（解释）。
copyright    包含版权信息的文档。
chapter      文档的章。
section      文档的节。
subsection   文档的小节。
appendix     文档的附录。
help         帮助文档。
bookmark     相关文档。
```

##### rev（几乎没有主流的浏览器支持hreflang）

```
<link rev="     ">
```

规定被链接文档与当前文档的关系。

###### 可选属性值

```
alternate 	文档的替代版本（比如打印页、翻译或镜像）。
stylesheet 	文档的外部样式表。
start 	    集合中的第一个文档。
next 	    集合中的下一个文档。
prev 	    集合中的上一个文档。
contents 	文档的目录。
index    	文档的索引。
glossary 	在文档中使用的词汇的术语表（解释）。
copyright 	包含版权信息的文档。
chapter 	文档的章。
section 	文档的节。
subsection 	文档的小节。
appendix 	文档的附录。
help 	    帮助文档。
bookmark 	相关文档。
```

##### size

```
<link sizes="    ">
```

此属性规定被链接的尺寸，只有当被链接资源是图标时 (rel="icon")，才能使用该属性。该属性可接受多个值。值由空格分隔。

###### 可选属性值

```
heightxwidth 
为被链接的图标规定一个或多个以像素计的高度/宽度值对。
高度与宽度之间由 "x" 或 "X" 分隔。
any 	
规定图标是可伸缩的（比如 SVG 图像）。
```

##### target（几乎没有主流的浏览器支持hreflang）

```
<link target="    ">
```

此属性规定在哪个窗口或框架中加载被链接文档。

###### 可选属性值

```
_blank      在新窗口中打开被链接文档。
_self       默认。在相同的框架中打开被链接文档。
_parent     在父框架集中打开被链接文档。
_top        在整个窗口中打开被链接文档。
framename	在指定的框架中打开被链接文档。
```

##### type

```
<link type="    ">
```

该属性规定被链接文档的MIME类型

###### 可选属性值

```
MIME_type  
```

表示被链接的文档类型

### [meta（空元素）](https://www.w3school.com.cn/tags/tag_meta.asp)

```
<meta/>
```

meta元素提供有关界面的元信息，比如针对搜索引擎和更新频度的描述和关键词，其标签的属性定义了与文档相关联的名称/值对。

### [script](https://www.w3school.com.cn/tags/tag_script.asp)

```
<script>-<script>
```

此元素可以在HTML中插入一段JavaScript

### [style](https://www.w3school.com.cn/tags/tag_style.asp)

```
<style>-</style>
```

此标签用于为HTML文档定义样式信息，在style中，可以规定在浏览器中如何呈现HTML文档。type属性是必须的，定义style元素的内容，唯一可能的值是“text/css”。

### [title](https://www.w3school.com.cn/tags/tag_title.asp)

```
<title>-</title>
```

该元素可定义文档的标题。浏览器会以特殊的方式来使用标题，并且通常把它放置在浏览器窗口的标题栏或状态栏上。同样，当把文档加入用户的链接列表或者收藏夹或书签列表时，标题将成为该文档链接的默认名称。

### [body](https://www.w3school.com.cn/tags/tag_body.asp)

```
<body>-</body>
```

body 元素定义文档的主体。

body 元素包含文档的所有内容（比如文本、超链接、图像、表格和列表等等。）

### [form](https://www.w3school.com.cn/tags/tag_form.asp)

```
<form>-</form>
```

该标签用于为用户输入创建 HTML 表单。

表单能够包含 [input 元素](https://www.w3school.com.cn/tags/tag_input.asp)，比如文本字段、复选框、单选框、提交按钮等等。

表单还可以包含 [menus](https://www.w3school.com.cn/tags/tag_menu.asp)、[textarea](https://www.w3school.com.cn/tags/tag_textarea.asp)、[fieldset](https://www.w3school.com.cn/tags/tag_fieldset.asp)、[legend](https://www.w3school.com.cn/tags/tag_legend.asp) 和 [label 元素](https://www.w3school.com.cn/tags/tag_label.asp)。

表单用于向服务器传输数据。

### [input（空元素）](https://www.w3school.com.cn/tags/tag_input.asp)

```
<input/>
```

该标签用于搜集用户信息。

根据不同的 type 属性值，输入字段拥有很多种形式。输入字段可以是文本字段、复选框、掩码后的文本控件、单选按钮、按钮等等。

## [textarea](https://www.w3school.com.cn/tags/tag_textarea.asp)

```
<textarea>-</textarea>
```

标签定义多行的文本输入控件。

文本区中可容纳无限数量的文本，其中的文本的默认字体是等宽字体（通常是 Courier）。

可以通过 cols 和 rows 属性来规定 textarea 的尺寸，不过更好的办法是使用 CSS 的 height 和 width 属性。

注释：在文本输入区内的文本行间，用 "%OD%OA" （回车/换行）进行分隔。

提示：可以通过 textarea标签的 wrap 属性设置文本输入区内的换行模式