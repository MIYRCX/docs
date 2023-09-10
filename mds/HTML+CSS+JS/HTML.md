> 创建日期：2020
>
> 修改日期：2023-3-11

# 一. 主体标签

```html
<html>
	<head><title>网页标题</title><head>
	<body>大部分内容</body>
</html>
```

# 二. 文本标签

```html
加粗：b <b>内容</b>; strong <strong>内容</strong> 倾斜：i <i>内容</i>; em
<em>内容</em> 变大：big <big>内容</big>； 变小：small <small>内容</small>;
上标：sup <sup>内容</sup> 下标：sub <sub>内容</sub> 删除线：del <del>内容</del>;
s <s>内容</s>text-decoration: line-through; 下划线：u <u>内容</u>; ins
<ins>内容</ins> 字体：font <font>内容</font> 属性（color颜色 size大小 face样式
排版标签： 换行 br <br />
横线 hr
<hr />
属性：width宽度 size粗细 color颜色 align对齐 noshade无阴影 段落 p
<p></p>
属性：align (left,center,right)
```

**标签嵌套：**必须有层次的嵌套，不可交叉嵌套

# 三. 标题标签

h1~h6 ，h1 最大,h2 最小 属性：align

```html
div和span div:
<div></div>
块标签 Span:<span></span>行内标签 注意：块可以设置长宽高
```

# 四. 列表标签

## 1. 有序标签

```html
<ol>
  <li>内容1</li>
  <li>内容2</li>
  <li></li>
</ol>
```

属性：type:1,a,A,i,I,none. start:起始位置

## 2. 无序标签

```html
<ul>
  <li>内容1</li>
</ul>
```

**去除小圆点：list-style:none;**

## 3. 自定义标签

```html
<dl>
  <dt>名词1</dt>
  <dt>名词</dt>
  <dd>名词解释1</dd>
  <dd>名词解释2</dd>
</dl>
```

# 五. 表单标签

```html
语法：
<form></form>
```

**含义：**会把它范围内的表单元素信息提交给服务器

| 属性   | 属性值   | 作用                                               |
| ------ | -------- | -------------------------------------------------- |
| action | url 地址 | 用于指定接收并处理表单的服务器程序的 url 地址      |
| method | get/post | 用于设置表单数据的提交方式，其取值为 get 或 post   |
| name   | 名称     | 用于指定表单的名称，以区分同一个页面中的多个表单域 |

## 1. 表单元素

```html
Input标签：文本输入 <input type="“属性值”" />
```

| 属性值   | 描述                                                                             |
| -------- | -------------------------------------------------------------------------------- |
| button   | 定义可点击按钮(多数情况下，用于通过 JavaScript 启动脚本)                         |
| checkbox | 定义复选框。                                                                     |
| file     | 定义输入字段和“浏览"按钮，供文件上传。                                           |
| hidden   | 定义隐藏的输入字段。value 用来放一些不希望被用户看见但是需要被提交到服务器的数据 |
| image    | 定义图像形式的提交按钮。                                                         |
| password | 定义密码字段。该字段中的字符被掩码。                                             |
| radio    | 定义单选按钮。                                                                   |
| reset    | 定义重置按钮。重置按钮会清除表单中的所有数据。                                   |
| submit   | 定义提交按钮。提交按钮会把表单数据发送到服务器。                                 |
| text     | 定义单行的输入字段，用户可在其中输入文本。默认宽度为 20 个字符。                 |

**checked = true 为选中状态** autofocus="autofocus"

focus 获取焦点

radio 单选和 checkbox 复选 必须有相同的 name 名字,才能实现多选一

| 属性      | 属性值       | 描述                                    |
| --------- | ------------ | --------------------------------------- |
| name      | 由用户自定义 | 定义 input 元素的名称。                 |
| value     | 由用户自定义 | 规定 input 元素的值。                   |
| checked   | checked      | 规定此 input 元素首次加载时应当被选中。 |
| maxlength | 正整数       | 规定输入字段中的字符的最大长度。        |

## 2. lable 标签

作用：使文字可被点击从而选中按钮

```html
<input type="radio" name="sex" id="nan" /><label for="nan">男</label>
<input type="radio" name="sex" id="nv" /><label for="nv">女</label>
```

## 3. select 下拉标签

**含义：**定义一个下拉列表

```html
<select>
  <option></option>
  <option></option>
</select>
```

**注意：**select 中至少包含一对 option

​ 在标签中定义 selected=“selected”,即为当前项为默认选中项

**textarea 标签：**

```html
<textarea cols="30" rows="10">这个是用来做留言反馈的</textarea>
```

# 六. 图片标签

```html
<img src="“url”width" ="“”" />
```

# 七. 地址路径

绝对路径：http://

相对路径：相对于某个文件来找的路径

目录：

1.  当前目录：【./】【当前目录./可以不写】
2.  上级目录：【../】
3.  下级目录：【文件夹/】

# 八. 链接标签

```html
<a href=”http://...”></a>
```

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310154900626.png" alt="image-20230310154900626" style="zoom: 67%;" />

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310154938900.png" alt="image-20230310154938900" style="zoom: 50%;" />

# 九. 表格标签

## 1. 表格的基本语法

含义：表格不是用来布局页面的，而是用来展示数据的

```html
<table>
  <tr>
    <td></td>
  </tr>
</table>
tr表示行 td表示列
```

## 2. 表头单元格标签

表头单元格常用于表格第一行，表头单元格的内容会加粗居中显示

```html
<table>
  <tr>
    <th></th>
  </tr>
</table>
```

## 3. 表格的基本属性

| 属性名      | 展性值               | 描述                                              |
| ----------- | -------------------- | ------------------------------------------------- |
| align       | left、center、 right | 规定表格相对周围元素的对齐方式。                  |
| border      | 1 或"“               | 规定表格单元是否拥有边框，默认为""， 表示没有边框 |
| cellpadding | 像素值               | 规定单元边沿与其内容之间的空白，默认 1 像素。     |
| cellspacing | 像素值               | 规定单元格之间的空白，默认 2 像素。               |
| width       | 像素值或百分比       | 规定表格的宽度。                                  |

border-spacing: 0; 单元格与单元格的距离

border-collapse: collapse; 合并边框模型

```html
<caption></caption>
标签为表格标题，在表格中上方生成标题
```

## 4. 表格结构标签

thead 用于定义表格头部`<thead>`内部必须要有`<tr>`标签，一般位于第一行

tbody 用于定义表格的主体，主要用于放数据本体

以上标签都是放在 table 标签中

## 5. 合并单元格

跨行合并：rowspan:“合并单元格个数”

跨列合并：colspan:“合并单元格个数”

目标单元格：（写代码合并代码）

跨行：最上侧目标单元格为目标单元格，写合并代码

跨列：最左侧目标单元格为目标单元格，写合并代码

合并单元格三部曲：

1. 先确定是跨行还是跨列
2. 找到目标单元格，写上合并方式=合并单元格数量，如`<td colspan="2"></td>`
3. 删除多余单元格

## 十. html 通用样式

Name:名称。`<div name="a1">123</div> `首位不能为数字可以为“A1“”不能为“1A”

Class:类

Id：唯一标识

Title:标题

Style:样式

# 十一. 标签关系

后代关系：包含关系父子关系

兄弟关系：同级关系，必须属于同父级关系
