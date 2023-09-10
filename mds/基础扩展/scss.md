> 创建日期：2023-7-10
>
> 修改日期：2023-7-10

#
# 一、什么是Sass

Sass 是采用 Ruby 语言编写的一款 CSS 预处理语言，它诞生于2007年，是最大的成熟的 CSS 预处理语言。最初它是为了配合 HAML（一种缩进式 HTML 预编译器）而设计的，因此有着和 HTML 一样的缩进式风格。

[scss中文网](https://www.sass.hk/)

[scss转css](https://www.sassmeister.com/)

# 二、SASS 和 SCSS 的区别

Sass 和 SCSS 其实是同一种东西，我们平时都称之为 Sass，两者之间不同之处有以下两点：

（1）文件扩展名不同。
Sass 是以“.sass”后缀为扩展名，而 SCSS 是以“.scss”后缀为扩展名。
（2）语法书写方式不同。
Sass 是以严格的缩进式语法规则来书写，不带大括号( { } )和分号( ; )，而 SCSS 的语法书写和我们的 CSS 语法书写方式非常类似。

示例：

```scss
$font-stac: Helvetica, sans-serif  //定义变量
$primary-color: #333 //定义变量
body 
  font: 100% $font-stack;
  color: $primary-color; // 没有 {} 和 ;


// Scss语法
$font-stack: Helvetica, sans-serif;
$primary-color: #333;
body {
  font: 100% $font-stack;
  color: $primary-color;
}

// 编译出来的css
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```



# 三、Scss的基本语法



## 1、声明变量 $

声明变量的符号 $

下面这张图左半部分是scss的语法，右半部分是编译后的css。（整篇文章皆是如此）

## 2、默认变量 !default

sass 的默认变量仅需要在值后面加上 !default 即可。


如果分配给变量的值后面添加了 !default 标志 ，这意味着该变量如果已经赋值，那么它不会被重新赋值，但是，如果它尚未赋值，那么它会被赋予新的给定值。

上述例子因为变量$color已经被赋值为$666，所以后来再给它赋默认值时不会影响它原来的值，$color的值仍然是$666。

## 3、变量调用

直接调用即可。变量声明时也可直接调用已声明的变量

## 4、局部变量和全局变量

在元素内部定义的变量不会影响其他元素

## 5、嵌套

**5.1、选择器嵌套**
Sass 中还提供了选择器嵌套功能，但这也并不意味着你在 Sass 中的嵌套是无节制的，因为你嵌套的层级越深，编译出来的 CSS 代码的选择器层级将越深，这往往是大家不愿意看到的一点

假如有这么一个结构：

```html
<header>
	<nav>
    <a href=“##”>Home</a>
    <a href=“##”>About</a>
    <a href=“##”>Blog</a>
	</nav>
<header>
```


想选中 header 中的 a 标签，在写 CSS 会这样写：

```css
nav a {
  color:red;
}

header nav a {
  color:green;
}
```

那么在 Scss 中，就可以使用选择器的嵌套来实现：

```scss
nav {
  a {
    color: red;
	header & {
  		color:green;
	}
  }  
}
```



**5.2、属性嵌套**
Sass 中还提供属性嵌套，CSS 有一些属性前缀相同，只是后缀不一样，比如：border-top/border-right，与这个类似的还有 margin、padding、font 等属性。假设你的样式中用到了：

```scss
.box {
    border-top: 1px solid red;
    border-bottom: 1px solid green;
}
```


在 Sass 中我们可以这样写：

```scss
.box {
  border: {
   top: 1px solid red;
   bottom: 1px solid green;
  }
}
```

5.3、伪类嵌套
借助 &

```scss
span{
    color: red;
    &:hover{
        color: #ccc;
    }
}
```



## 6、混合宏

如果你的整个网站中有几处小样式类似，比如颜色，字体等，在 Sass 可以使用变量来统一处理，那么这种选择还是不错的。但当你的样式变得越来越复杂，需要重复使用大段的样式时，使用变量就无法达到我们目了。这个时候 Sass 中的混合宏就会变得非常有意义。



**6.1、声明**



6.1.1、不带参数混合宏
在 Sass 中，使用“ @mixin ”来声明一个混合宏。如：

```scss
@mixin border-radius{
    -webkit-border-radius: 5px;
    border-radius: 5px;
}
```

其中 @mixin 是用来声明混合宏的关键词，有点类似 CSS 中的 @media、@font-face 一样。border-radius 是混合宏的名称。大括号里面是复用的样式代码。



6.1.2、带参数混合宏
除了声明一个不带参数的混合宏之外，还可以在定义混合宏时带有参数，如：

```scss
@mixin border-radius($radius:5px){
    -webkit-border-radius: $radius;
    border-radius: $radius;
}
```


**6.2、调用**
在 Sass 中通过 @mixin 关键词声明了一个混合宏，那么在实际调用中，其匹配了一个关键词“ @include ”来调用声明好的混合宏。例如在你的样式中定义了一个圆角的混合宏“border-radius”:

```scss
@mixin border-radius{
    -webkit-border-radius: 3px;
    border-radius: 3px;
}
```

在一个按钮中要调用定义好的混合宏“border-radius”，可以这样使用：

```scss
button {
    @include border-radius;
}
```

这个时候编译出来的 CSS:

```css
button {
  -webkit-border-radius: 3px;
  border-radius: 3px;
}
```

**6.3、混合宏的参数**
Sass 的混合宏有一个强大的功能，可以传参，那么在 Sass 中传参主要有以下几种情形：



6.3.1、 传一个不带值的参数
在混合宏中，可以传一个不带任何值的参数，比如：

```scss
@mixin border-radius($radius){
  -webkit-border-radius: $radius;
  border-radius: $radius;
}
```


在混合宏“border-radius”中定义了一个不带任何值的参数“$radius”。

在调用的时候可以给这个混合宏传一个参数值：

```scss
.box {
  @include border-radius(3px);
}
```

这里表示给混合宏传递了一个“border-radius”的值为“3px”。

编译出来的 CSS:

```scss
.box {
  -webkit-border-radius: 3px;
  border-radius: 3px;
}
```


6.3.2、传一个带值的参数
在 Sass 的混合宏中，还可以给混合宏的参数传一个默认值，例如：

```scss
@mixin border-radius($radius:3px){
  -webkit-border-radius: $radius;
  border-radius: $radius;
}
```

在混合宏“border-radius”传了一个参数“$radius”，而且给这个参数赋予了一个默认值“3px”。

在调用类似这样的混合宏时，会多有一个机会，假设你的页面中的圆角很多地方都是“3px”的圆角，那么这个时候只需要调用默认的混合宏“border-radius”:

```scss
.btn {
  @include border-radius;
}
```


编译出来的 CSS:

```scss
.btn {
  -webkit-border-radius: 3px;
  border-radius: 3px;
}
```

但有的时候，页面中有些元素的圆角值不一样，那么可以随机给混合宏传值，如：

```scss
.box {
  @include border-radius(50%);
}
```

编译出来的 CSS:

```scss
.box {
  -webkit-border-radius: 50%;
  border-radius: 50%;
}
```


**6.4、混合宏的不足**
混合宏在实际编码中给我们带来很多方便之处，特别是对于复用重复代码块。但其最大的不足之处是会生成冗余的代码块。比如在不同的地方调用一个相同的混合宏时。如：

```scss
@mixin border-radius{
  -webkit-border-radius: 3px;
  border-radius: 3px;
}

.box {
  @include border-radius;
  margin-bottom: 5px;
}

.btn {
  @include border-radius;
}
```

示例在“.box”和“.btn”中都调用了定义好的“border-radius”混合宏。先来看编译出来的 CSS：

```scss
.box {
  -webkit-border-radius: 3px;
  border-radius: 3px;
  margin-bottom: 5px;
}

.btn {
  -webkit-border-radius: 3px;
  border-radius: 3px;
}
```

上例明显可以看出，Sass 在调用相同的混合宏时，并不能智能的将相同的样式代码块合并在一起。这也是 Sass 的混合宏最不足之处。



## 7、扩展/继承

在 Sass 中是通过关键词 “@extend”来继承已存在的类样式块，从而实现代码的继承。如下所示：

```scss
.btn {
  border: 1px solid #ccc;
  padding: 6px 10px;
  font-size: 14px;
}

.btn-primary {
  background-color: #f36;
  color: #fff;
  @extend .btn;
}

.btn-second {
  background-color: orange;
  color: #fff;
  @extend .btn;
}
```

编译出来之后：

// CSS

```css
.btn, .btn-primary, .btn-second {
  border: 1px solid #ccc;
  padding: 6px 10px;
  font-size: 14px;
} // 合并到了一起

.btn-primary {
  background-color: #f36;
  color: #fff;
}

.btn-second {
  background-clor: orange;
  color: #fff;
}
```

从示例代码可以看出，在 Sass 中的继承，可以继承类样式块中所有样式代码，而且编译出来的 CSS 会将选择器合并在一起，形成组合选择器。



## 8、占位符 % placeholder

它可以取代以前 CSS 中的基类造成的代码冗余的情形。因为 %placeholder 声明的代码，如果不被 @extend 调用的话，不会产生任何代码。来看一个演示：

```scss
%mt5 {
  margin-top: 5px;
}
%pt5{
  padding-top: 5px;
}
```

这段代码没有被 @extend 调用，他并没有产生任何代码块，只是静静的躺在你的某个 SCSS 文件中。只有通过 @extend 调用才会产生代码：

```scss
// SCSS
%mt5 {
  margin-top: 5px;
}
%pt5{
  padding-top: 5px;
}

.btn {
  @extend %mt5;
  @extend %pt5;
}

.block {
  @extend %mt5;

  span {
    @extend %pt5;
  }
}
```

编译出来的CSS

```scss
// CSS
.btn, .block {
  margin-top: 5px;
}

.btn, .block span {
  padding-top: 5px;
}
```

版权声明：本文为CSDN博主「平平无奇小码农qwq」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_42667613/article/details/113176294