> 创建日期：2020
>
> 修改日期：2023-3-11

#

**语法规则**

- 格式声明语句，要用{ }括起来，里面放各种声明语句
- 一条格式的声明语句 是由 属性：属性值；构成
- 属性就是 css 的各种属性，已经定义好
- 在属性的后面用；结束
- Css 样式必须写单位
- Css 样式的数值单位用 px（像素），0 可以不写

# 一.引入

1.行内引入

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160342292.png" alt="image-20230310160342292" style="zoom:50%;" />

2.内嵌引入

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160358973.png" alt="image-20230310160358973" style="zoom:50%;" />

3.外部引入

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160408197.png" alt="image-20230310160408197" style="zoom:50%;" />

# 二.选择器

## 1.通用选择器

**符号**：\*{属性}

含义：所有的元素都选择

```css
* {
}
```

## 2.标签选择器

**语法**：标签名{属性}

含义：选择指定标签的元素

```css
div {
}
```

## 3.类选择器

**语法**：.class 名{属性；}

**含义**：指定的 class 名的元素

```css
.a {
}
/*多类名使用：
	优点：少写css代码
	语法：<div class=“a1 a2”>内容<div>*/
```

## 4.id 选择器

**语法**：id 名{属性；}

**含义**：选择器指定 id 的元素

**注意：要加#号**

```css
#a {
}
```

## 5.伪类选择器

a:link 未访问的选择器
a:visited 访问过的
a:hover 鼠标放上
a:active 鼠标点击
注意：以上顺序最好不要打乱

```css
a:hover {
}
```

**focus 伪类选择器**：此选择器一般针对表单来说

```css
input:focus {
  background-color: red;
}
```

## 6.分组选择器

语法：选择器 1，选择器 2{属性；}

含义：选择选择器 1 的元素和选择器 2 的元素，一起设置一样的格式

```css
.a,
#a {
}
```

## 7.后代选择器

语法：选择器 1 选择器 2{属性；}

含义：选择选择器 1 的后代选择器 2 的元素

```css
.box a {
}
```

## 8.子代选择器

语法：选择器 1>选择器 2{属性；}

含义：选择选择器 1 的子元素选择器 2 的元素

```css
.box > a {
}
```

## 9.并集选择器（重要）

语法：元素 1,元素 2{样式声明} 英文逗号连接

```css
span,
ul a {
}
```

## 10.选择器优先级

Id 选择器（100）>类选择器（10）>标签选择器（1）>通用选择器

把权重相加：得到的数值越大优先级越高

如果优先级相同，后面的覆盖前面的

# 三.属性

元素转换：

```css
display: block块元素 inline行元素 inline-block行内块 （默认内容宽度）none不显示;
```

字体：

```css
font-size: 大小 font-weigth：400（取消加粗）加粗（bold加粗） font-style：倾斜
  （italic倾斜 normal正常） font-family：字体 '宋体';
```

文本：

```css
text-indent：2em 首行缩进
text-align:对齐（left） {text-align}（可用于上下对齐）
text-decoration：文本线（underline下划线 line-through中划线 over-line上划线 none不显示）
letter-spacing：字间距
word-spacing：词间距
white-space: nowrap; /* 文字强制一行显示 */
```

# 四.背景

| 属性/值                                                        | 含义                                                                                        |
| -------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| background-color:red                                           | 背景颜色 默认为透明的                                                                       |
| background-image: url ( );                                     | 背景图片会压住背景颜色                                                                      |
| background-position：x y 代表 x 轴和 y 轴                      | 背景图片位置 可只用方位名词和精确坐标                                                       |
| background-repeat：repeat \| no-repeat \| repeat-x \| repeat-y | 含义：常见于 logo、装饰图片、超大的背景图片，优点是易控制                                   |
| background-attachment：scroll(滚动) fixed(固定)                | 背景图像是否固定或者随着页面其余部分滚动                                                    |
| background：rgba（0,0,0,0.3）；                                | 背景半透明 最后一个参数是透明度，取值范围在 0~1 之间 此处为盒子背景半透明，盒子内容不受影响 |

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160423665.png" alt="image-20230310160423665" style="zoom:50%;" />

**背景复合写法：**background：背景颜色 背景图片地址 背景平铺 背景图像滚动 背景图片位置；

实际开发中更提倡此写法

# 五.盒子模型

## 1.边框

border 可以设置元素的边框。边框又三部分组成：边框宽度（粗细）、边框样式、边框颜色 D:\华为云盘\数据备份\资料\md 笔记

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160434294.png" alt="image-20230310160434294" style="zoom:50%;" />

```css
/*边框简写：边框会影响盒子实际大小*/
border: 12px solid red;
```

## 2.内边距

padding 属性用于设置内边距，既边框与内容的距离

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160446344.png" alt="image-20230310160446344" style="zoom:50%;" />

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160512677.png" alt="image-20230310160512677" style="zoom:50%;" />

## 3.外边距

margin 用于设置盒子与盒子之间的距离

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160524160.png" alt="image-20230310160524160" style="zoom:50%;" />

margin 的简写方式和 padding 完全一致

**块级盒子设置居中显示：**

盒子必须设置了 width 宽度

盒子左右外边距设置为 auto

以上元素是让块元素水平居中，行内元素和行内块元素水平居中可以在其父元素添加 text-align：center 即可

**相邻垂直外边距合并**

​ 当上下两个盒子设置了上下外边距的时候，取最大值。而不是两个边距相加

解决方案：尽量只给一个盒子设置外边距

**嵌套块元素垂直外边距塌陷**

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160535566.png" alt="image-20230310160535566" style="zoom:50%;" />

## 4.圆角边框

border-radius 属性用于设置元素的外边框圆角

```css
border-radius：20px;
```

```css
border-radius:50%; 设置为一个圆
border-radius:?px;（高度的一半）设置为圆角矩形
```

该属性是一个简写属性，可以跟四个值，分别代表左上角，右上角，右下角，左下角

## 5.盒子阴影

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160545643.png" alt="image-20230310160545643" style="zoom:50%;" />

## 6.文字阴影

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160553062.png" alt="image-20230310160553062" style="zoom:50%;" />

# 六.浮动

**网页布局第一准则：多个块级元素纵向排列找标准流，多个块级元素横向排列找浮动**

## 1.浮动语法

```css
float: left;
```

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160604720.png" alt="image-20230310160604720" style="zoom:50%;" />

设置了浮动（float）的元素最重要特性：

- 脱离标准普通流的控制（浮）移动到指定位置（动），（俗称脱标）
- 浮动的盒子**不再保留原先的位置**
- 多个盒子都设置了浮动，则它们会按照属性值一行内显示并且顶部对齐排列
- 浮动元素会具有行内块元素的特性

## 2.常见网页布局

**浮动元素和标准流父级搭配使用**

先用标准流的父元素排列上下位置，之后内部子元素采取浮动排列左右位置，符合网页布局第一准则。

**一个元素浮动了，理论上其余的兄弟元素也要浮动**

浮动的盒子只会影响浮动盒子后面的标准流，不会影响前面的标准流。

## 3.清楚浮动

由于父级盒子很多情况下不方便给高度，但是子盒子浮动又不占有位置，最后父级盒子高度为 0 时，就会影响下面的标准流盒子

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160613249.png" alt="image-20230310160613249" style="zoom:50%;" />

由于浮动元素补在占用原文档的位置，所以它会对后面的元素排版产生影响

**语法：选择器 { clear : 属性值};**

实际开发中几乎只用 { clear : both };

含义：清除浮动造成的影响

**清除浮动——额外标签法**

额外标签法也称隔墙法，是 w3c 推荐的做法。实际工作中不推荐

额外标签法会在浮动元素末尾添加一个空的标签。例如`<div style=" clear:both></div>`，或者其他标签（如）等。

- 优点：通俗易懂，书写方便
- 缺点：添加许多无意义的标签，结构化较差

**注意：**要求这个新的空标签必须是**块级**元素。

**清除浮动——父级添加 overflow**

可以给**父级**添加 overflow 属性，将其属性值设置为 hidden、auto、或 scroll。

- 优点：代码简洁
- 缺点：无法显示溢出的部分

**清除浮动——：after 伪元素法**

:after 方式是额外标签法的升级版。也是给父元素添加

- 优点：没有增加标签，结构简单
- 缺点：需要照顾低版本浏览器

代表网站：百度、淘宝网、网易等

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160629935.png" alt="image-20230310160629935" style="zoom:50%;" />

**清除浮动——双伪元素清除浮动**

也是给父元素添加

- 优点：代码更简洁
- 缺点：需照顾低版本浏览器

代表网站：小米、腾讯等

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160638766.png" alt="image-20230310160638766" style="zoom:50%;" />

# 七.css 书写顺序

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160645901.png" alt="image-20230310160645901" style="zoom:50%;" />

# 八. 定位

定位：将盒子定在某一个位置，所以定位也是在摆放盒子，按照定位的方式移动盒子。

定位=定位模式+边偏移。

定位模式用于指定一个元素在文档中的定位方式，边偏移则决定了该元素最终位置

## 1.定位模式

定位模式决定元素的定位方式，它通过 css 的 position 属性来设置，其值可以分为：

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160654400.png" alt="image-20230310160654400" style="zoom:50%;" />

## 2.边偏移

边偏移就是定位的盒子移动到最终位置。有四个属性。

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160702851.png" alt="image-20230310160702851" style="zoom:50%;" />

## 3.静态定位（了解）

静态定位是元素的默认定位方式，无定位的意思

**语法：** 选择器 { position : static ; }

- 静态定位按照标准流特性摆放位置，它没有边偏移
- 静态定位在布局时很少用到

## 4.相对定位（重要）

**相对定位**是元素在移动位置的时候，相对于它**原来的位置**来说的（自恋型）

**语法：**

```css
选择器 {
  position: relative;
}
```

**相对定位的特点：**务必记住

- 它是相对于自己原来的位置来移动的（移动位置的时候参照点是自己原来的位置）
- 原来在标准流的位置继续占有，后面的盒子仍以标准流的方式对待它。（不脱标，继续保留原来的位置）。它最典型的运用是给绝对定位当爹的。

## 5.绝对定位

**绝对定位**是元素在移动位置的时候，相对于它**祖先元素**来说的（拼爹型）。

**语法：**

```css
选择器 {
  position: absolute;
}
```

绝对定位的特点：（务必记住）

- 如果没有**祖先元素**或者**祖先元素没有定位**，则以浏览器为准定位
- 如果祖先元素有定位（相对、绝对、固定定位），则以最近一级的有定位祖先元素为参考点移动位置。

## 6.定位叠放次序 z-index

在使用定位布局时，可能出现盒子重叠的情况。此时，可以使用 z-index 来控制盒子的前后次序（z 轴）

**语法:**

```css
选择器 {
  z-index: 1;
}
```

- 数值可以是正整数、负整数或 0，默认是 auto，数值越大，盒子越靠上
- 如果属性值相同，则按照书写顺序，后来居上
- 数字后面不能加单位
- 只有定位的盒子才有 z-index 属性

## 7.设置绝对定位的盒子居中

加了绝对定位的盒子不能通过 margin:0 auto 水平居中，但是可以通过以下计算方法实现水平和垂直居中

- Left : 50%；：让盒子的左侧移动到父级元素的水平中心位置。
- margin-left：-100px；：让盒子向左移动自身宽度的一半。

## 8.定位的特性

绝对定位和固定定位也和浮动类似

- 行内元素添加绝对或者固定定位，可以直接设置高度和宽度
- 块级元素添加绝对或者固定定位，可以不给宽度或者高度，默认大小是类容大小

**浮动不会压住文字**：因为浮动本身是用来做文字环绕效果的

# 九.元素的显示与隐藏

网页的广告，当我们点击就不见了，但是我们重新刷新页面，会重新出现！

本质：**让一个元素在页面中隐藏或者显示出来。**

## 1.display 属性

display 属性设置一个元素应如何显示

```css
display: none; /*隐藏对象*/
display: block; /*除了转换块级元素之外，同时还有显示元素的意思*/
```

**display 隐藏元素后，不再占有原来的位置**

## 2.visibility 可见性

visibility 属性用于指定一个元素应可见还是隐藏

```css
visibility:visible;元素可视
visibility:hidden;元素隐藏
```

**visibility 隐藏元素后，继续占有原来的位置**

- 如果隐藏元素**想要**原来的位置，就用 visibility:hidden;

- 如果隐藏元素**不想**要原来的位置，就用 display:none（用处更多 重点）

## 3.overflow 溢出

属性指定了如果内容**溢出**一个元素的框（超过其指定高度及宽度）时，会发生什么。

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160713706.png" alt="image-20230310160713706" style="zoom:50%;" />

一般情况下，我们都不想让溢出的内容显示出来，因为溢出的部分会影响布局

但是如果有定位的盒子，请慎用 overflow:hidden 因为它会隐藏多余的部分

# 十.css 高级技巧

## 1.精灵图

精灵技术的目的：**为了有效地减少服务器接收和发送请求的次数，提高页面的加载速度**

使用精灵图核心**总结**：

- 精灵图主要针对于小的背景图片使用
- 主要借助于背景位置来实现——background-position
- 一般情况下精灵图都是负值

## 2.字体图标

字体图标的优点:

- 轻量级：一个图标字体要比一系列的图像要小。一旦字体加载了，图标就会马上渲染出来，减少了服务器的请求
- 灵活性：本质就是文字，可以很随意的改变颜色、产生阴影、透明效果、旋转等
- 兼容性：几乎支持所有的浏览器、可以放心的使用

简单的用字体图标，复杂的用精灵图

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160724707.png" alt="image-20230310160724707" style="zoom:50%;" />

```css
@font-face {
  font-family: 'icomoon';
  src: url('fonts/icomoon.eot?897qlt');
  src: url('fonts/icomoon.eot?897qlt#iefix') format('embedded-opentype'), url('fonts/icomoon.ttf?897qlt')
      format('truetype'), url('fonts/icomoon.woff?897qlt') format('woff'), url('fonts/icomoon.svg?897qlt#icomoon')
      format('svg');
  font-weight: normal;
  font-style: normal;
  font-display: block;
}
```

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160735803.png" alt="image-20230310160735803" style="zoom:50%;" />

## 3.css 三角

网页中常见的一些三角形，可以直接画出来，不用做成图片和字体图标

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160746414.png" alt="image-20230310160746414" style="zoom:50%;" />

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160757083.png" alt="image-20230310160757083" style="zoom:50%;" />

## 4.用户界面样式

## 4.1.鼠标样式

鼠标样式 cursor

```css
li { cursor：pointer；}
```

设置或检索在对象上移动的鼠标指针采用何种系统预定义的光标形状

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160807165.png" alt="image-20230310160807165" style="zoom:50%;" />

## 4.2.表单轮廓线

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160817130.png" alt="image-20230310160817130" style="zoom:50%;" />

## 4.3.防止拖拽文本域

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160823567.png" alt="image-20230310160823567" style="zoom:50%;" />

## 5.vertical-align 属性

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160832817.png" alt="image-20230310160832817" style="zoom:50%;" />

**图片底侧空白缝隙解决方案：**

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160840478.png" alt="image-20230310160840478" style="zoom:50%;" />

## 6.溢出文字省略号显示

## 6.1 单行显示

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160849521.png" alt="image-20230310160849521" style="zoom:50%;" />

## 6.2 多行显示

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160857011.png" alt="image-20230310160857011" style="zoom:50%;" />

# 十一.常见布局技巧

## 1.margin 负值运用

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160908213.png" alt="image-20230310160908213" style="zoom:50%;" />

## 2.文字围绕浮动元素

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160914410.png" alt="image-20230310160914410" style="zoom:50%;" />

# 十二. HTML5 新特性

## 1.新增语义化标签

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160921231.png" alt="image-20230310160921231" style="zoom:50%;" />

## 2.多媒体标签

## 2.1 视频 video

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161028414.png" alt="image-20230310161028414" style="zoom:50%;" />

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310160929253.png" alt="image-20230310160929253" style="zoom:50%;" />

考虑兼容性写法：

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161037748.png" alt="image-20230310161037748" style="zoom:50%;" />

## 2.2 音频 audio

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161049901.png" alt="image-20230310161049901" style="zoom:50%;" />

## 3.新增的 input 类型

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161111452.png" alt="image-20230310161111452" style="zoom:50%;" />

## 4. 新增的表单属性

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161118621.png" alt="image-20230310161118621" style="zoom:50%;" />

## 5.网站 TDK 优化

**1、title 网站标题**

title 具有不可替代性，是我们内页的第一个重要标签，是搜索引擎了解网页的入口和对网页主题归属的最佳判断点

建议：网站名（产品名）-网站的介绍（尽量不要超过 30 个汉字）

**2、description 网站说明**

简要说明我们的网站主要做什么

**3、keywords 关键字**

Keywords 最好限制为 6~8 个关键词，关键词之间用英文逗号隔开，采用关键词 1、关键词 2 的形式

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161127605.png" alt="image-20230310161127605" style="zoom:50%;" />

# 十三.css3 新特性

## 1.新增选择器

## 1.1 属性选择器

属性选择器可以根据元素特定的属性来选择元素，这样就可以不用借助于类 id 选择器

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161134195.png" alt="image-20230310161134195" style="zoom:50%;" />

## 1.2 结构伪类选择器

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161152978.png" alt="image-20230310161152978" style="zoom:50%;" />

## 1.3 伪元素选择器

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161205780.png" alt="image-20230310161205780" style="zoom:50%;" />

**清除浮动**

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161212541.png" alt="image-20230310161212541" style="zoom:50%;" />

## 2.2d 转换

## 2.1 二维坐标系

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161220801.png" alt="image-20230310161220801" style="zoom:50%;" />

## 2.2 移动 translate

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161231577.png" alt="image-20230310161231577" style="zoom:50%;" />

## 2.3 旋转

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161242765.png" alt="image-20230310161242765" style="zoom: 50%;" />

## 2.4 转换中心点 origin

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161257502.png" alt="image-20230310161257502" style="zoom:50%;" />

## 2.5 缩放 scale

## 2. 6 综合写法

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161309076.png" alt="image-20230310161309076" style="zoom:50%;" />

## 3. 动画

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161344344.png" alt="image-20230310161344344" style="zoom:50%;" />

## 3.1 定义动画

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161354786.png" alt="image-20230310161354786" style="zoom:50%;" />

## 3.2 使用动画

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161407264.png" alt="image-20230310161407264" style="zoom:50%;" />

## 3.3 动画常见属性

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161415880.png" alt="image-20230310161415880" style="zoom:50%;" />

**Linear：匀速播放**

## 3.4 动画简写

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161425660.png" alt="image-20230310161425660" style="zoom:50%;" />

## 4. 3d 转换

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161435572.png" alt="image-20230310161435572" style="zoom:50%;" />

## 4.1 3d 移动 translate3d

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161444832.png" alt="image-20230310161444832" style="zoom:50%;" />

## 4.2 透视 perspective

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161454169.png" alt="image-20230310161454169" style="zoom:50%;" />

## 4.3 3d 旋转 rotate3d

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161500522.png" alt="image-20230310161500522" style="zoom:50%;" />

## 4.4 3d 呈现 transfrom-style

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161507801.png" alt="image-20230310161507801" style="zoom:50%;" />

## 5. 浏览器私有前缀

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161515687.png" alt="image-20230310161515687" style="zoom:50%;" />

## 6.C3 盒子模型

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161522669.png" alt="image-20230310161522669" style="zoom:50%;" />

## 7.图片模糊处理

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161529923.png" alt="image-20230310161529923" style="zoom:50%;" />

## 8. 宽度函数 calc

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161538003.png" alt="image-20230310161538003" style="zoom:50%;" />

计算符号左右有空格

子盒子比父盒子小 80px

## 9.过渡

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161556800.png" alt="image-20230310161556800" style="zoom:50%;" />

# 十四. 补充

## 1.**display:block;**

div 下 a 标签用 padding 撑开，用此方法可以使整个盒子都可点击

**案例：**js（5.2）拖动登录框

## 2.**生成随机数**

var sum =Math.floor(Math.random()\*12+1) ; //创造一个随机 1~12 的随机数

## 3.**背景线性渐变**

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161605452.png" alt="image-20230310161605452" style="zoom:50%;" />

## 4.html 实体

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310161616517.png" alt="image-20230310161616517" style="zoom:50%;" />
