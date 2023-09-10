> 创建日期：2020
>
> 修改日期：2023-3-11




# 一. js基础

## 1. 引入

行内引入：

```html
<a href="javaScript:alert('你想一夜暴富吗')">链接</a>
```

内部引入：

```html
<script>
        alert("输出");
</script>
```

外部引入：

```html
 <script src="js.js"></script>
```



## 2. 输出

alert:弹出一个提示或警告框   （浏览器级别）

document.write:输出内容    （文本级别，套标签）

| 方法              | 说明                           | 归属   |
| ----------------- | ------------------------------ | ------ |
| alert(msg);       | 浏览器弹出警示框               | 浏览器 |
| console.log(msg); | 浏览器控制台打印输出信息       | 浏览器 |
| prompt(info);     | 浏览器弹出输入框，用户可以输入 | 浏览器 |



## 3. 语法规则

- 所有的符号必须是英文状态
- 区分大小写
- 建议：每条语句后面加上分号
- **同时声明多个变量时，只需要写一个var,做个变量名之间使用英文逗号隔开。**



# 二. 变量

**语法**：var 变量名=值

```html
var a1 = 13;
```



## 1. 变量的形式

var a;定义变量a，不保存数据

var a=1;定义变量a，初始化数据为1

var a,b,c,d;定义变量a,b,c,d,都不给其保存数据

var a,b=1,c,d=2;定义变量a，不保存数据，定义变量b初始化数据为



## 2. 变量命名规范

- 由字母(A-Za-z). 数字(0-9)、 下划线( )、 美元符号($ )组成，如: usrAge, num01, name
- 严格区分大小写。var app;和var App;是两个变量

- 不能以数字开头。18age 是错误的


- 不能是关键字、保留字。例如:var、for、 while


- 变量名必须有意义。MMD BBD


- 遵守驼峰命名法。首字母小写,后面单词的首字母需要大写。myFirstName
- 推荐翻译网站:有道爱词霸



## 3. 变量声明的特殊情况

| 情况               | 说明                   | 结果      |
| ------------------ | ---------------------- | --------- |
| var age;log(age)   | 只声明 不赋值          | undefined |
| log(age)           | 不声明 不赋值 直接使用 | 报错      |
| age = 10; log(age) | 不声明 只赋值          | 10        |



# 三. 数据类型



| 简单数据类型 | 说明                                             | 默认值    |
| ------------ | ------------------------------------------------ | --------- |
| number       | 数字型，包含整型值和浮点值，如21、0.21           | 0         |
| boolean      | 布尔值类型，true、false，等价于1和0              | false     |
| String       | 字符串类型，如"张三" 注意js里面，字符串都带引号  | ""        |
| undefinded   | var a;声明了变量a但是没有给值，此时a = undefined | undefined |
| null         | vara= null;声明了变量 a 为空值                   | null      |

**在JS中，八进制前面加0，十六进制前面加0x**

 

**JavaScript是一种弱类型或者说是动态语言。**这就意味着不用提前声明变量的类型，在程序运行过程中会被自动确定

```javascript
var age = 10;      //这是一个数字型

var areyouok = ‘是的’;  //这是一个字符串
```

**JavaScript拥有动态类型，同时也就意味着相同的变量课用作不同的类型**

```javascript
var x = 6;         //x为数字
var x =’bill’;       //x为字符串
```

**IsNaN（）**

用来判断一个变量是否为非数字的类型，返回true或者false

```javascript
 console.log(isNaN(12));
```



## 1. 字符串型

**字符串引号嵌套**

JS可以用单引号嵌套双引号，或者用双引号嵌套单引号（**外单内双，外双内单**）

```javascript
var str = "学程序有点'头冷'呢";

var str = '学程序有点头"冷"呢';
```



## 2. 转义字符

| 转义符       | 解释说明                 |
| ------------ | ------------------------ |
| \n           | 换行符，n是newline的意思 |
| "  \\\    "  | 斜杠 \                   |
| "   \ '    " | ' 单引号                 |
| "   \\"  "   | '' 双引号                |
| \t           | tab 缩进                 |
| \b           | 空格，b是 blank 的意思   |



## 3. 字符串长度length

```javascript
var str = 'hello js';
alert(str.length);
```

**字符串拼接**

- 多个字符串之间可以使用 + 进行拼接，其拼接方式为**字符串+任何类型=拼接之后的新字符串**

- 拼接前会把与字符串相加的任何类型转化为字符串，再拼接成一个新的字符串

**数字相加，字符相连**



## 4. 布尔型boolean

布尔类型有两个值：**true**和**false**，其中true为真（对），而false表示假（错）

布尔类型和数字型相加的时候，**true的值为1**，**false的值为0**。

```javascript
 console.log(true + 1); //2
 console.log(false + 1); //1
```



## 5. undefined和null

一个声明后没有赋值的变量会有一个默认值undefined（如果进行相连或者相加时，注意结果）

```javascript
var v;
console.log(v);     	//undefined
console.log('你好'+v);   //你好undefined
console.log(11+v);   	//NaN
console.log(true+v);    //NaN
```

一个生命变量给null值，里面存的值为空

```javascript
var v = null;
console.log('你好'+v); 		//	你好null
console.log(11+v);  		// 11
console.log(true+v);    	// 1
```

# 四. 获取变量类型



## 1. typeof检测数据类型

typeof可以检测数据的类型

```javascript
var name = '张三'; 
console.log(typeof name); //string
```



## 2. 字面量

字面量是在源代码中一个固定值的表示法，通俗来说，就是字面量表示如何表达这个值

- 数字字面量：8,9,10
- 字符串字面量：‘程序员’，‘前端工程师’
- 布尔字面量：true,false

# 五. 数据类型转换



## 1. 转换为字符串

| 方式               | 说明                         | 案例                                  |
| ------------------ | ---------------------------- | ------------------------------------- |
| toString()         | 转成字符串                   | var num= 1; alert(num.toString();     |
| String()强制转换   | 转成字符串                   | var num =1; alert(String(num);        |
| **加号拼接字符串** | 和字符串拼接的结果都是字符串 | var num = 1; alert(num+“我是字符串"); |

用第三种方法更多，这种方法称之为**隐式转换**



## 2. 转换为数字型

| 方式                   | 说明                         | 案例                |
| ---------------------- | ---------------------------- | ------------------- |
| parselnt(string)函数   | 将string类型转成整数数值型   | parselnt(78')       |
| parseFloat(string)函数 | 将string类型转成浮点数数值型 | parseFloat('78.21') |
| Number()强制转换函数   | 将string类型转换为数值型     | Number('12')        |
| js隐式转换(- * /)      | 利用算术运算隐式转换为数值型 | '12'- 0             |

重点记住前两个，注意parseInt和parseFloat的**大小写**



## 3. 转换为布尔型

| 方式           | 说明                 | 案例            |
| -------------- | -------------------- | --------------- |
| boolean( )函数 | 其他类型转换成布尔值 | boolean('true') |

- 代表空、否定的值会被转换为false，如“”、0、NaN、null、nudefined
- 其余的值会被转换为true

# 六. 运算符



## 1. 算数运算符

算术运算使用的符号，用于执行两个变量或者值得算术运算

| 运算符 | 描述         | 实例                |
| ------ | ------------ | ------------------- |
| +      | 加           | 10+10=20            |
| -      | 减           | 10-10=0             |
| *      | 乘           | 10*20=200           |
| /      | 除           | 10/20=0.5           |
| %      | 取余数(取模) | 返回出发的余数9%2=1 |



## 2. 递增运算符

- **前置递增运算符：**

  ++num前置递增，就是自加1，类似于num=num+1，但是++num写起来更简单。

使用口诀：**先自加，后返回值**

- **后置递增运算符：**

  Num++后置递增，就是自加1，类似于num=num+1，但是num++写起来更简单。

使用口诀：**先返回原值，再自加**



## 3. 比较运算符

​		概念：比较运算符（关系运算符）是两个数据进行比较时所使用的运算符，比较运算后，会返回一个布尔值（true/false）作为比较运算的结果。

| 运算符名称 | 说明                         | 案例      | 结果  |
| ---------- | ---------------------------- | --------- | ----- |
| <          | 小于号                       | 1<2       | true  |
| >          | 大于号                       | 1>2       | false |
| >=         | 大于等于号(大于或者等于)     | 2>=2      | true  |
| <=         | 小于等于号(小于或者等于)     | 3<=2      | false |
| ==         | 判等于(会转型)               | 37==37    | true  |
| !=         | 不等号                       | 37！=37   | false |
| ===        | 全等 要求值和 数据类型都一致 | 37==='37' | false |



## 4. 逻辑运算符

逻辑运算符是用来进行布尔值运算的运算符，其返回值也是布尔值。后面开发中经常用于多个条件的判断

| 逻辑运算符 | 说明                    | 案例            |
| ---------- | ----------------------- | --------------- |
| &&         | "逻辑与"，简称"与"  and | true && false   |
| \|\|       | "逻辑或"，简称"或"  or  | true \|\| false |
| !          | "逻辑非"，简称"非"  not | ! true          |

- 逻辑**与**：两边都是true才返回true，否则返回false;
- 逻辑**或**：两边都是false才返回false，否则返回true;
- 逻辑**非**：也叫**取反符**，用来取一个布尔值相反的值，如true的相反值是false



## 5. 短路运算逻辑与

**语法：**表达式1 && 表达式2

- 如果第一个表达式的值为真，则返回表达式2
- 如果第一个表达式的值为假，则返回表达式1

## 6. 短路运算逻辑或

**语法：**表达式1 || 表达式2

- 如果第一个表达式的值为真，则返回表达式1
- 如果第一个表达式的值为假，则返回表达式2



## 7. 赋值运算符

| 赋值运算符 | 说明                   | 案例                       |
| ---------- | ---------------------- | -------------------------- |
| =          | 直接赋值               | var u = '我是值';          |
| +=、-=     | 加、减 一个 数后再赋值 | var age = 10; age+=5; //15 |
| *=、/=、%= | 乘、除、取模 后再赋值  | var age = 2; age*=5; //10  |



## 8. 运算符优先级

| 优先级 | 运算符     | 顺序           |
| ------ | ---------- | -------------- |
| 1      | 小括号     | ( )            |
| 2      | 一元运算符 | ++  --  !      |
| 3      | 算数运算符 | 先* / % 后 + - |
| 4      | 关系运算符 | > >= < <=      |
| 5      | 相等运算符 | == != === !=== |
| 6      | 逻辑运算符 | 先 && 后 \|\|  |
| 7      | 赋值运算符 | =              |
| 8      | 逗号运算符 | ，             |

- 一元运算符里面的逻辑非优先级很高
- 逻辑与比逻辑或优先级高



# 七. 流程控制

​		流程控制就是来控制我们的代码按照什么结构顺序来运行，主要有**顺序结构**、**分支结构**和**循环结构**，这三种结构代表三种代码执行的顺序。



## 1. if分支结构

**if语句**

```javascript
//条件式成立执行代码，否则什么也不做

if （条件表达式）{
      //条件成立执行的代码语句
}
**if else****双分支语句**
       //条件成立 执行if里面的代码，否则执行else里面的代码

if（条件表达式）{
     //条件成立执行的代码语句
}else{
     //条件不成立执行的代码
}
```

**if else if 语句（多分支语句）**

```javascript
//适合于检查多重条件
if（条件表达式1）{
      语句1
}else if（条件表达式2）{
      语句2
}else if（条件表达式3）{
      语句3
}else{
   //上述条件都不成立执行此代码
}
```



## 2. 三元运算符

有三元运算符组成的式子我们成为三元表达式

```
语法：条件表达式 ？表达式1 : 表达式2;
```

如果条件表达式结果为真 则返回表达式1的值，如果条件表达式的结果为假 则返回表达式2的值。	

```javascript
 var is = 9>10? '大于':'小于';
 alert(is);
```

数字补零案例

```javascript
var num = prompt('输入')
var is = num < 10 ? '0' + num : ''  //小于10补零
console.log(is);
```



## 3. switch分支语句

​		**执行思路：**利用表达式的值和case后面的选项值相匹配，如果匹配上，就执行该case里面的语句。如果都没匹配上，那么执行default里面的语句

**语句结构：**

```javascript
switch(表达式){
   case value1:
      //执行语句1;
      break;
   case value1:
      //执行语句1;
      break;
   default:
     //执行最后语句;
}
```

```javascript
var a = 1;
        switch (a) {
            case 1:
                console.log('这是1');
                break;
            case 2:
                console.log('这是2');
                break;
            default:
                console.log('没有');
                break;
        }
```

**注意事项：**

1. 开发中的表达式经常写成变量
2. 表达式与case后的值必须是全等，必须是值和数据类型一致才可以
3. 如果当前case里面没有break则不会退出switch，继续执行下一个case;

**if else与switch的区别：**

1. 一般情况下，他们的语句可以相互替换
2. Switch语句通常处理case为比较确定的情况，而if else语句更加灵活，常用于范围判断（大于、等于某个范围）
3. Switch语句进行条件判断后直接执行到程序的条件语句，效率更高。     而if else语句有几种条件，就得判断多少次
4. 当分支较少用if else执行效率更高，分支较多用switch语句执行效率 更高，而且结构更清晰



## 4. 循环

​		在程序中，一组被重复执行的语句被称之为**循环体**，能否继续重复执行，取决于循环的**终止条件**。由循环体及循环的终止条件组成的语句，被称之为**循环语句**

**for循环**

for循环主要用于把某些代码循环若干次，通常跟计数有关系。语法结构：

```javascript
for（初始化变量; 条件表达式; 操作表达式）{
        //循环体
}
```

**双重for循环**

​	循环嵌套是指在一个循环语句中再定义一个循环的语法结构，例如在for循环语句中，可以再嵌套一个for循环，这样的语句我们称之为双重for循环

**whil循环**

while语句可以在条件表达式为真的前提下，循环执行指定的一段代码，直到表达式不为真时结束循环。语法：

```javascript
while(){
        //循环体
}
```

```javascript
while(true){   //死循环
      continue;   //结束本次循环
      break;      //终止循环
}
```



## 7. 变量作用域

在局部作用域下定义的变量叫**局部变量**（**在函数内部定义的变量**）

- 全局变量：在任何一个地方都可以使用，只有浏览器关闭时才会被销毁，因此比较占内存
- 局部变量：只在函数内部使用，当其所在的代码块被执行时，会被初始化；当代码块运行结束后，就会被销毁，因此更节省内存空间



# 八. 数组



## 1. 创建数组

```javascript
// 1.创建对象
var arr = new Array()
// 2.使用数组字面量方式创建空的数组
var 数组名 = [];
// 3.使用数组字面量方式创建带初始化值得数组
var 数组名 = ['1','2',100]
```

- 数组的字面量是方括号[]

- 声明数组并赋值称为数组的初始化
- 数组可放任意数据类型



## 2. 遍历数组

遍历数组可使用`.length`方法

```javascript
var arr = [1, 2, 3, 4, 5, 6]
for (var i = 0; i < arr.length; i++) {
      console.log(arr[i]);
}
```



## 3. 获取数组最大值

```javascript
var arr = [111, 2, 3, 66, 5]
var max = arr[0]

for (var i = 0; i < arr.length; i++) {
      if (arr[i] > max) {
           max = arr[i]
       }
}
console.log(max);
```



## 4. 数组新增元素

- 通过修改数组长度的方法新增

```javascript
var arr = [1, 2, 3]
arr.length = 4
console.log(arr[3]); // undefined
```

- 通过索引号追加元素

```javascript
var arr = [1, 2, 3]
arr[3] = 4
console.log(arr); // [1, 2, 3, 4]
```



## 5. 筛选数组

```javascript
var arr = [13, 24, 56, 34, 92, 6, 3, 6, 3, 78]
        var newarr = []
        var j = 0
        for (var i = 0; i < arr.length; i++) {
            if (arr[i] > 10) {
                newarr[j] = arr[i]
                j++
            }
        }
        console.log(newarr);
```

```javascript
var arr = [13, 24, 56, 34, 92, 6, 3, 6, 3, 78]
        var newarr = [] 
        for (var i = 0; i < arr.length; i++) {
            if (arr[i] > 10) {
                newarr[newarr.length] = arr[i] // 数组长度为0 随着数组长度增加而增加
            }
        }
        console.log(newarr);
```



## 7. 翻转数组

```javascript
var arr = [13, 24, 56, 34, 92, 6, 3, 6, 3, 78]
        var newarr = []
        for (var i = arr.length - 1; i >= 0; i--) {
            newarr[newarr.length] = arr[i]
        } console.log(newarr);
```



## 8. 冒泡排序

```javascript
var arr = [5, 4, 3, 2, 1]
        for (var i = 0; i <= arr.length - 1; i++) { // 外层循环管趟数
            for (var j = 0; j <= arr.length - i - 1; j++) { //里面的循环管 每一趟的交换次数
                //内部交换2个变量的值 前一个和后面一个数组元素想比较
                if (arr[j] > arr[j + 1]) {
                    var temp = arr[j]
                    arr[j] = arr[j + 1]
                    arr[j + 1] = temp
                }
            }
        }

```



# 九. 函数



## 1. 声明与调用

声明方式1：**命名函数**

```javascript
//声明函数
function 函数名(){
    //函数体代码
}
```

声明方式2：**函数表达式**    (匿名函数)

```javascript
var fn = function(){
     console.log("输出");
}
fn();
```



函数就是封装了一段可以被重复执行调用的代码块 目的是让大量代码重复调用

```javascript
function sum(num1, num2) {
            console.log(num1 + num2);
        }
sum(1, 1)
```

<b>注意：声明函数本身并不会执行代码，只有调用函数时才会执行函数体代码</b>



## 2. 参数

在声明函数时，可以在函数名称后面的小括号中添加一些参数，这些参数称为形参。在调用该函数时同样也需要传递相应的参数，这些参数

| 参数个数 | 说明                               |
| -------- | ---------------------------------- |
| 相等     | 输出正常结果                       |
| 多于     | 取到形参个数                       |
| 小于     | 多的形参定义为undefined，结果为NaN |

| 参数     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| **形参** | **形**式上的参数 **函数定义**的时候传递的参数 当前并不知道是什么 |
| **实参** | **实**际上的参数 **函数调用**的时候传递的参数 实参是传递给形参的 |



## 3. return语句

可以将结果返回给调用者，没有返回值返回undefined

```javascript
function fn(num1, num2) {
     return num1 + num2;
}
console.log(fn(1, 2));
```



## 4. break，continue，return的区别

- break：结束当前循环体（如for、while）
- continue：跳出本次循环、继续执行下次循环
- return：不仅可以退出循环、还能够返回return语句中的值、同时还可以结束当前的函数内的代码



## 5.arguments

只有函数才有此对象 而且每个函数都内置了这个对象，返回的为伪数组

```javascript
function fn(){
    for(var i=0;i<arguments.length;i++){
        console.log(arguments[i]);
    }
}
fn(1,2,3,4,5)
```

伪数组：

- 具有数组的length属性
- 按照索引的方式进行存储
- 没有数组的一些方法 pop()、push()等



## 6. 作用域链

内部函数访问外部函数的变量，采取的是链式查找的方式来决定取哪个值。这种结构我们称为作用域链

```javascript
var num = 10
function fn() {
        var num = 20
        fun()
        function fun() {
            console.log(num); // 20
        }
}
fn()
```



## 7. 预解析

1. Js引擎运行js分为两步： 预解析  代码执行

2. 预解析分为变量预解析（变量提升）和函数预解析（函数提升）

   **预解析：**js引擎会把就是里面所有的var 还有function提升当前作用域的最前面

   **代码执行：**按照代码书写顺序从上往下执行

   **变量提升：**就是把所有的变量声明提升到当前的作用域最前面 不赋值、

   **函数提升：**就是把所有的函数声明提升到当前的作用域最前面 不调用

   ```javascript
   var num = 10;
   fn();
   function fn() {
        console.log(num);
        var num = 20;
   };
   // 相当于以下代码
   var num;
   function fn() {
       var num;
   	console.log(num);
        num = 20;
   };
   num = 10;
   fn();
   ```

   ```javascript
   var num = 10;
   function fn() {
   	console.log(num);
   	var num = 20;
   	console.log(num);
   };
   fn();
   // 相当于以下代码
   var num;
   function fn() {
   	var num;
   	console.log(num);
   	num = 20;
   	console.log(num);
   };
   num = 10;
   fn();
   ```

   ```javascript
    var a = 8;
     fn();
   function fn() {
        var b = 9;
        console.log(a);
        console.log(b);
        var a = '123';
   };
   // 相当于以下代码
   var a;
   function fn() {
       var b;
       var a;
       b = 9;
       console.log(a);
       console.log(b);
       a = '123';
   };
   a = 18;
   fn();
   ```

   

# 十. 对象

​	里面的属性或者方法我们采取键值对的形式

​      键 属性名：  |  值 属性值

1. 多个属性或者方法中间用逗号隔开
2. 方法名冒号后面跟的是一个匿名函数

**调用的方法**

1. 对象名.属性名
2. 对象名[‘属性名’]
3. 调用方法为  对象名.方法名（） （注意有小括号）

```javascript
 var boy = {
     name:'张三',
     age:18,
     sex:'男',
     sleep:function(){
            console.log('睡觉');
     };
};
alert(boy.age);
alert(boy['age']);
alert(boy.sleep());
```



## 1. new object创建对象

```javascript
var obj = new Object;   //创建一个空对象
obj.name = '张三';       //赋值操作
alert(obj.name);        //打印输出
```



## 2. 构造函数创建对象

**构造函数：**是一种特殊的函数，主要用来初始化对象，即为对象成员变量初始化赋值，它总与new运算符一起使用。我们可以把对象中一些公共的属性和方法抽取出来，然后封装到这个函数里

**注意事项：**

1. 构造函数名字首字母要大写
2. 我们构造函数不需要return就可以返回结果

```javascript
function star(name,age,sex){ //创造一个明星的构造函数
    this.name = name;
    this.age = age;
    this.sex = sex;
}
var ldh = new star('刘德华',18,'男');   //创建对象并赋值
```



## 3. 构造函数与对象

**构造函数：**抽去了对象的公共部分，封装到了函数里面，它泛指某一大类

**创建对象：**特指某一个，通过new关键字创建对象的过程我们也称之为对象实例化



## 4. for in 遍历对象

for in 里面的变量通常写 k 或者 key

```javascript
 var boy = {
     name:'张三',
     age:18,
     sex:'男'
}
for(var k in boy){
     console.log(k);     //k为变量 输出的到是 属性名
     console.log(boy[k]);    //得到的是属性值
}
```



# 十一. 内置对象

- Js中对象分为3种：自定义对象、内置对象、浏览器对象
- **内置对象**就是指js语言自带的一些对象，这些对象供开发者使用，并提供了一些常用的最基本而必要的功能（属性和方法）



## 1. Math()对象

返回给定的一组数字中的最大值。如果给定的参数中至少有一个参数无法被转换成数字，则会返回 [`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)。

如果没有参数，则结果为 - [`Infinity`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Infinity)。

如果有任一参数不能被转换为数值，则结果为 [`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)。

```javascript
console.log(Math.max(1,2,3));    //3
console.log(Math.max(1,2,'wx'));//NaN
console.log(Math.max());    	//-Infinity
```

Math对象不是构造函数，它具有数学常用的属性的方法。和数学有关的运算可以使用Math中的成员。

```javascript
Math.PI					//圆周率
Math.floor()			//向下取整
Math.ceil()				//向上取整
Math.round()			//四舍五入 就近取整 注意 -3.5结果是 -3
Math.abs()				//绝对值
Math.max()/Math.min() 	//求最大值和最小值
```

随机数：`Math.random`

此函数返回一个浮点数,  伪随机数在范围从**0**到小于**1**，也就是说，从0（包括0）往上，但是不包括1（排除1）

```javascript
function getRandomIntInclusive(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min + 1)) + min; //含最大值，含最小值 
}
```

```javascript
function getRandom(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min; //含最大值，含最小值 
}
console.log(getRandom(1, 10));

var arr = ['张三', '李四', '王二']
console.log(arr[getRandom(0, arr.length - 1)]);
```



## 2. Date()方法的使用

1. 获取当前时间必须实例化

2. Date()构造函数的参数

   如果括号里面有时间，就返回参数里面的时间。例如日期格式化字符串为‘2019-2-1’，可以写成new Data(‘2019-2-1’)（此写法会大一月），或者new Date(‘2019/2/1’)

```javascript
var time = new Date();
console.log(time);    //Sat Oct 17 2020 17:33:27 GMT+0800 (中国标准时间)
```

- **日期格式化**

| 方法名        | 说明                      | 代码               |
| ------------- | ------------------------- | ------------------ |
| getFullYear() | 获取当年                  | dObj.getFullYear() |
| getMonth(）   | 获取当月(0-11)            | dObj.getMonth()    |
| getDate()     | 获取当天日期              | dObj.getDate()     |
| getDay()      | 获取星期几(周日0 到周六6) | dObj.getDay()      |
| getHours()    | 获取当前小时              | dObj.getHours()    |
| getMinutes()  | 获取当前分钟              | dObj.getMinutes()  |
| getSeconds()  | 获取当前秒钟              | dObj.getSeconds()  |



## 3. 总毫秒数(时间戳)

```javascript
//1.通过valueOf()  getTime()
var date = new Date();
console.log(date.valueOf()); //就是 我们现在的时间 距离1970.1.1 总的毫秒数
console.log(date.getTime());
//2.简单的写法 (常用)
var date1 = +new Date; //+new Date() 返回的就是总的毫秒数
console.log(date1);
//3.H5新增的 获取总的毫秒数
console.log(Date.now());
```

倒计时案例

```javascript
function countdown(time) {
        var nowTime = +new Date() //返回当前时间戳
        var inputTime = +new Date(time) //输入的时间戳
        var times = (inputTime - nowTime) / 1000 //剩余时间时间戳 单位毫秒转换为秒

        var d = parseInt(times / 60 / 60 / 24) //天数
        d = d < 10 ? '0' + d : d
        var h = parseInt(times / 60 / 60 % 24) //小时
        h = h < 10 ? '0' + h : h
        var m = parseInt(times / 60 % 60) //分
        m = m < 10 ? '0' + m : m
        var s = parseInt(times % 60)    // 当前的秒 
        s = s < 10 ? '0' + s : s
        return d + '天' + h + '时' + m + '分' + s + '秒'
}
console.log(countdown('2022-1-18 20:00:00'));
```



## 4. 数组对象

```javascript
var arr = [1,2,3,];			//利用字面量创建数组
console.log(arr[0]);
//var arrl = new Array();	//创建一一个空的数组
//var arrl = new Array(10) ;//表示数组的长度为10
var arr1 = new Array(2,3) ;	//等价于[2,3]这样写表示里面有两个数组元素是2和3
console.log(arr1) ;
```

**检测是否为数组：**

```javascript
log(value instanceof Array)
Array.isArray(value) // >ie9版本
```

**添加删除数组元素的方法:**

```javascript
var arr = [1, 2, 3]
/*添加*/
//数组末尾添加
arr.push(4, '末尾') //在数组末尾添加
console.log(arr); //返回新数组的长度  (5) [1, 2, 3, 4, '末尾']

//数组开始添加
arr.unshift('之前')
console.log(arr); //(6) ['之前', 1, 2, 3, 4, '末尾']

/*删除*/
arr.pop() //删除最后一个元素
console.log(arr); //(5) ['之前', 1, 2, 3, 4]
console.log(arr.pop()); //返回值为删除的元素

//删除第一个元素
arr.shift()
console.log(arr); 
```

**筛选数组：**

```javascript
var arr = [123, 234, 34545, 242, 243, 1]
var newArr = []
for (var i = 0; i < arr.length; i++) {
    if (arr[i] > 100) {
         newArr.push(arr[i])  //使用push方法
    }
}
console.log(newArr);
```

**翻转数组：**

```javascript
var arr = [1, 2, 3, 4, 5]
arr.reverse()
console.log(arr); //(5) [5, 4, 3, 2, 1]
```

**冒泡排序：**

```javascript
var arr = [1, 324, 7, 4242, 10]
arr.sort() //默认首位数字
console.log(arr); //(5) [1, 10, 324, 4242, 7]

var arr = [1, 324, 7, 4242, 10]
arr.sort(function (a, b) {
        return a - b //升序排列 
    	return b - a //降序排列
})
console.log(arr);
```

**数组索引方法：**

| 方法名      | 说明                           | 返回值                                  |
| ----------- | ------------------------------ | --------------------------------------- |
| indexOf()   | 数组中查找给定元素的第一个索引 | 如果存在返回索引号 如果不存在，则返回-1 |
| lastIndexOf | 从后往前查找元素的索引         | 如果存在返回索引号 如果不存在，则返回-1 |

```javascript
var arr = ['pink', 'blue', 'black', 'red']

console.log(arr.indexOf('blue')); // 1
console.log(arr.lastIndexOf('blue')); // 4
```

**数组去重：**

```javascript
function unique(arr) {
   var newArr = []
   for (var i = 0; i < arr.length; i++) {
       if (newArr.indexOf(arr[i]) === -1) { //如果新数组中查不到就数组的值就存入
            newArr.push(arr[i])
       }
   }
   return newArr
}
var arr = ['pink', 'blue', 'black', 'red', 'blue']
console.log(unique(arr));
```

**数组转换未字符串：**

| 方法名         | 说明                                       | 返回值         |
| -------------- | ------------------------------------------ | -------------- |
| toString()     | 把数组转换为字符串，逗号分隔每一项         | 返回一个字符串 |
| join('分隔符') | 方法用于把数组中的所有元素转换为一个字符串 | 返回一个字符串 |

```javascript
var arr = [1, 2, 3, 4]
console.log(arr.toString()); //1,2,3,4
console.log(arr.join('&')); //1&2&3&4
```



## 5. 字符串对象

- **基本包装类型**

  为了方便操作基本数据类型，js还提供了三个特殊的因公类型：String、Number和Boolean。

  基本包装类型就是把简单数据类型包装成为复杂数据类型，这样基本数据就有了属性和方法

```javascript
//下面的代码有什么问题
var str = 'andy';
console.log(str.length);
```

​		按道理基本数据类型是没有属性和方法的而对象才有属性和方法，但是上面代码却可以执行，这是因为js会把基本数据类型包装为复杂数据类型

```javascript
//1.生成临时变量，把简单类型包装复杂数据类型
var temp = new String('andy');
//2.复制给我们声明的祖父变量
str = temp;
//3.销毁临时变量
temp = null;
```

- **字符串不可变**

  指的是里面的值不可变，虽然看上去可以改变内容，但其实是地址变了，内存中新开辟了一个内存空间

```javascript
var str = 'abc';
str = 'hello';
// 重新给str赋值的时候，常量'abc'不会被修改，依然在内存中
// 重新给字符串赋值，会重新在内存中开辟空间，这个特点就是字符串的不可变
// 由于字符串的不可变，在大量拼接字符串的时候会有效率问题
var str = '';
for (var i = 0; i < 10000; i++) {
      str += ' ';
}
console.log(str);   //这个结果要花费大量时间来显示，因为需要不断的开辟新的空间
```

- **字符串查找**

字符串所有的方法，都不会修改字符串本身（字符串是不可变的），操作完成会返回一个新的字符串

| 方法名                              | 说明                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| indexOf('要查找的字符'，开始的位置) | 返回指定内容在原字符串中的位置，如果找不到就返回-1，开始的位置是index索引号 |
| lastIndexOf()                       | 从后往前找，只找第一个匹配的                                 |

```javascript
var str = '改革春风吹满地 春风吹满地';
console.log(str.indexOf('春')); //顺序查找
console.log(str.indexOf('春',4));   //从索引号为4开始往后查找
```

**查找字符串中某个字符出现的次数：**

```javascript
var str = 'sddsdjbincanfos'
var index = str.indexOf('o')
var num = 0
while (index !== -1) {
    console.log(index);
    num++
    index = str.indexOf('o', index + 1)
}
console.log('次数为' + num);
```

**根据位置返回字符(重点)：**

| 方法名            | 说明                                     | 使用                       |
| ----------------- | ---------------------------------------- | -------------------------- |
| charAt(index)     | 返回指定位置的字符(index字符串的索引号)  | str.charAt(0)              |
| charCodeAt(index) | 获得指定位置处字符的ASCII码(index索引号) | str.charCodeAt(0)          |
| str[index]        | 获得指定位置处字符                       | H5.ie8+支持 和charAt()等效 |

```javascript
var str = 'pink'
console.log(str.charAt(3)); //k
//遍历
for (var i = 0; i < str.length; i++) {
   console.log(str.charAt(i));
}

var str = 'Apink'
console.log(str[0]);
```



# 十一. Dom

因为我们文档页面从上往下加载，所以得现有标签 所以script写到获取元素



## 1. 根据id获取

1. Get 获得element元素by通过驼峰命名 
2. 参数id是大小写敏感的字符串 
3. 返回的是一个元素

```html
 <div id="time">2020</div>
<script>
        var time = document.getElementById('time');
        console.log(time); //<div id="time">2020</div>
        console.log(typeof time); //object
        //打印我们返回的元素对象，更好的查看里面的属性的方法
        console.dir(time); //div#time
</script>
```



## 2. 根据标签名获取

使用getElementsByTagName()方法返回带有指定标签名的对象的集合

1. 因为得到的是一个对象的集合，所以我们想要操作里面的元素就需要遍历
2. 得到的元素对象是动态的
3. 如果页面只有一个li，返回的还是伪数组的形式
4. 如果页面没有这个元素，返回的是空的伪数组的形式

```html
ul>li*10
<script>
        //返回的是获取过来元素对象的集合 以伪数组的形式存储
        var lis = document.getElementsByTagName('li');
        console.log(lis);   //HTMLCollection(4) [li, li, li, li]
        //遍历打印元素对象
        for (var i = 0; i < lis.length; i++) {
            console.log(lis[i]);
        }
</script>
```

```javascript
var ul = document.getElementsByTagName('ul');   //获取标签
console.log(ul[0].getElementsByTagName('li')); //打印对象下的标签
```



## 3. h5获取

```javascript
document.getElementsByClassName('类名');	 //根据类名返回元素对象集合
document.querySelector('选择器');			//根据指定选择器返回第一个元素对象
document.querySelectorAll('选择器');		//根据指定选择器返回
```

```html
 <div class="div">盒子1</div>
 <div class="div">盒子2</div>
 <ul>
    <li>li1</li>
 </ul>
 <script>
        var divs = document.getElementsByClassName('div'); //根据类名返回对象集合
        console.log(divs); //HTMLCollection(2) [div.div, div.div]
        var div1 = document.querySelector('.div'); //根据指定选择器返回第一个元素对象
        console.log(div1); // <div class="div">盒子1</div>
        var divss = document.querySelectorAll('.div'); //根据指定选择器返回所有
        console.log(divss); //NodeList(2) [div.div, div.div]
 </script>
```



## 4. 获取特殊元素

- 获取body元素

```javascript
document.body;			//返回body元素对象
```

- 获取html元素

```javascript
docment.docmentElment	//返回html元素对象
```



# 十一. 事件基础

- Js是我们有能力创建动态页面，而事件时可以被js侦测到的行为
- 简单理解：触发---响应机制
- 事件是有三部分组成 事件源 事件类型 事件处理程序 ---事件三要素
- 事件类型 如何触发 什么事件 比如鼠标点击（onclick）还是鼠标经过 还是键盘按下
- 事件处理程序 通过一个函数赋值的方式 完成

```html
<button>按钮</button>
<script>
        var btu = document.querySelector('button');
        btu.onclick = function(){
            alert('点击了一次');
        }
</script>
```

**执行事件的步骤**

1. 获取事件源
2. 注册事件（绑定事件）
3. 添加事件处理程序（采取函数赋值形式）



## 1. 常见鼠标事件

| 鼠标事件    | 触发条件         |
| ----------- | ---------------- |
| onclick     | 鼠标点击左键触发 |
| onmouseover | 鼠标经过触发     |
| onmouseout  | 鼠标离开触发     |
| onfocus     | 获得鼠标焦点触发 |
| onblur      | 失去鼠标焦点触发 |
| onmousemove | 鼠标移动触发     |
| onmouseup   | 鼠标弹起触发     |
| onmousedown | 鼠标按下触发     |



## 2. 阻止鼠标行为

- 禁止鼠标右键菜单

```javascript
// contextmenu主要控制应该何时显示上下文菜单，主要用于程序员取消默认上下文菜单
document.addEventListener('contextmenu',function(e){
    e.preventDefault();
});
```

- 禁止鼠标选中(selectstart 开始选中)

```javascript
document.addEventListener('selectstart',function(e){
    e.preventDefault();
});
```



## 3. 操作元素

​		Js的dom操作改变网页内容、结构和样式，我们可以利用dom操作来改变元素里面的内容、属性等。注意一下都是属性

**1. 改变元素内容**

```javascript
elment.innerText  // 不识别标签直接显示
```

​	从起始位置到终止位置的内容，但它去除html标签，同时空格和换行也会去掉

```javascript
elment.innerHTML // 识别
```

​	起始位置到终止位置的全部内容，包括html标签，同时保留空格和换行

```html
<!-- 例 -->
<button>按钮</button>
<div>now</div>
<script>
    var btu = document.querySelector('button');
    var div = document.querySelector('div');
    btu.onclick = function () {
       	div.innerHTML = '2020';
    }
    log(div.innerHTML) //读写
</script>
```

**2. 表单元素的属性操作**

​	利用DOM可以操作如下表单元素的属性

```
type、value、checked、selected、disabled(true按钮禁用)
```

```html
<button>按钮</button>
<div>now</div>
<script>
	var btu = document.querySelector('button');
	var div = document.querySelector('div');
    btu.onclick = function () {
       btu.innerHTML = '点击了一次';
       this.disabled = true;	//禁用按钮
    }
</script>
```

**3. 样式属性操作**

可以通过js修改元素的大小、颜色、位置等样式

```javascript
element.style		//行内样式操作
element.className	//类名样式操作
```

**注意：**

1. 如果样式修改较多,可以采取操作类名方式更改元素样式。
2. class因为是个保留字,因此使用clas sName来操作元素类名属性
3. className 会直接更改元素的类名,会覆盖原先的类名。

**可以通过将原先的类名写上以保留原先的类名**

**4. 排他思想**

​	如果有同一组元素，我们想要某一个元素实现某种样式，需要用到循环的排他思想

1. 所有元素全部清除样式（干掉其他人）
2. 给当前元素设置样式（留下我自己）

```html
 <button>按钮</button>*4
    <script>
        var btus = document.querySelectorAll('button');
        for (var i = 0; i < btus.length; i++) {
            btus[i].onclick = function () {
                for (var j = 0; j < btus.length; j++) {
                    btus[j].style.backgroundColor = '';	//点击按钮后循环清除样式
                }
                this.style.backgroundColor = 'red';	//this按钮添样式
            }
        }
    </script>
```

**5. 自定义属性的值**

- **获取属性值**

```javascript
element.属性	//获取属性值
element.getAttribute('属性');
```

**对象的属性**

区别：

```javascript
element.属性		//获取内置属性值(元素本身自带的属性)
element.getAttribute('属性');	//主要获得自定义的属性(标准)我们程序员自定义的属性
```

- **设置属性值**

```javascript
element.属性 = '值'		//设置内置属性值
element.setAttribute('属性','值');
```

**区别：**

```
element.属性	//设置内置属性值
element.setAttribute('属性');	//主要设置自定义的属性(标准)
```

**移除属性：**

```javascript
.removeAttribute('index')
```

**例：**

```html
<div class="demo" index="1"></div>
<script>
    var demo = document.querySelector('div');
    console.log(demo.className);
    var index = demo.getAttribute('index'); //获取demo的自定义属性
    console.log(index);
</script>
```

```html
<div in='index'></div>
    <script>
        var div = document.querySelector('div');
        console.log(div.setAttribute('in',12)); 	// 将index改为了 12
    </script>
```



## 4. H5自定义属性

​	**自定义属性目的：**是为了保存并使用数据。有些数据可以保存到页面中而不用保存到数据库中。

​	设置H5自定义属性

​    H5规定自定义属性data-开头作为属性名并且赋值。

```javascript
//	比如<div data-index="1"></div>
//	或者使用JS设置
//	element.setAttribute('data-index',2);
```



# 十二. 节点操作

利用DOM树可以把节点划分为不同的层级关系，常见的是**父子层级关系**



## 1. 节点层级

1. **父级节点**

- parentNode属性可返回某节点的父节点，注意是**最近的一个父节点**
- 如果指定的节点没有父节点则返回null

```html
<div class="father">
        <div class="son"></div>
</div>
<script>
       var son = document.querySelector('.son');
       console.log(son.parentNode);
</script>
```

2. **子级节点**

- childNodes 方法会获取所有的子节点包括：元素节点、文本节点
- children 获取所有的元素子节点 也是实际开发中常用的

```html
<div class="father">
       ul>li*4 
</div>
<script>
    var ul = document.querySelector('ul');   
    console.log(ul.childNodes);  //NodeList(9) [text, li, text, li, text, li, text, li, text]
    console.log(ul.children);    //HTMLCollection(4) [li, li, li, li]
</script>
```

**获取首个与末尾的元素**

```html
ul>li*4
<script>
       var ul = document.querySelector('ul');   
       console.log(ul.firstElementChild);   //不考虑兼容性
       console.log(ul.lastElementChild);    //ie9以上才支持
       console.log(ul.children[0]);         //获取第一个元素
       console.log(ul.children.length-1);   //获取最后一个元素
</script>
```

3. **兄弟节点**

```html
<div class="demo"></div>
<div class="demo1"></div>
<script>
    var demo = document.querySelector('.demo');
    console.log(demo.nextSibling);  //下一个兄弟(包含文本节点) text
    console.log(demo.previousSibling);   //上一个兄弟(包含文本节点) text

    console.log(demo.nextElementSibling);//下一个元素兄弟
    console.log(demo.previousElementSibling);//上一个 null
</script>
```

**下面的两个方法需要ie9以上才支持，否则只能封装一个函数：**

```javascript
 function getNextElementSibling(element){
            var el = element;
            while(el=el.nextSibling){
                if(el.nodeType===1){
                    return el;
                }
            }
            return null;
        }
```



## 2. 创建节点

```javascript
 document.createElement('tagName');
```

此方法创建有tagName指定的HTML元素。因为这些元素原先不存在，是根据我们的需求动态生成的，所以我们也称为**动态创建元素节点**





## 3. 添加节点

```javascript
node.appendChild(child)	//node为父元素
```

此方法将一个节点添加到指定父节点的子节点列表**末尾**。类似css里的after伪元素

```javascript
node.insertBefore(child,指定元素) //放在前面
```

```html
<ul></ul>
<script>
    var li = document.createElement('li');
    var ul = document.querySelector('ul');
    ul.appendChild(li);
</script>
```



## 4. 删除节点

```javascript
node.removeChild(child)		//从dom中删除一个子节点，返回删除的节点
```

```html
<button>按钮</button>
ul>li*5
<script>
        var ul = document.querySelector('ul');
        var lis = document.querySelectorAll('li');
        var btu = document.querySelector('button');
        btu.addEventListener('click',function(){
                if(ul.children.length==0){
                    btu.disabled = true;
                }else{
                    ul.removeChild(ul.children[0]);
                }
            });		//点击按钮删除li
</script>	
```



## 5. 复制节点

```javascript
node.cloneNode(true)	//返回调用该方法的节点的一个副本。也成为克隆节点/拷贝节点
```

**注意：**如果括号参数为**空或者false**，则是**浅拷贝**，即克隆节点本身，不克隆里面的子节点



# 十三. 事件高级



## 1. 注册事件（绑定）

1. **addEventListener事件监听方式**

```javascript
eventTarget.addEventListener(type,listener[,useCapture]);
```

此方法将指定的监听器注册到eventTarget(目标对象)上，当该对象触发指定的时间时，就会执行时间处理函数

该方法接收三个参数：

- **type** : 事件类型字符串，比如click、mouserover，注意这里不要带on
- **listener** : 事件处理函数，事件发生时，会调用该监听函数
- **useCapture** : 可选参数，是一个布尔值，默认是false。

如果一个按钮同时绑定了两个点击事件，传统的方法后面的会覆盖前面的，而以下方法不会



## 2. 删除事件(解绑)

```javascript
eventTarget.removeEventListener(type,listener[,useCapture]);
eventTarget.detachEvent(eventNameWithOn,callback);
```

```html
<div>123</div>
<div>123</div>
<div>123</div>
<script>
        var divs = document.querySelectorAll('div');
        divs[o].onclick = function () { //传统解绑方式
            divs[0].onclick = null;
        }
        //新的解绑方式
        divs[1].addEventListener('click', fn);
        function fn() {
            alert('1')
            divs[1].removeEventListener('click',fn);
        }
</script>
```



## 3. dom事件流

**事件**发生时会在元素节点之间按照特定的顺序传播，这个**传播过程叫dom事件流**

1. JS代码中只能执行捕获或者泡其中的一个阶段。
2. onclick和attachEvent只能得到胃泡阶段。
3. addEventListener (type, listener [, useCapture])第三个参数如果是true ,表示在件捕获阶段调用骋件处理程序;如果是false (不写默认就是false)， 表示在事件泡阶段调用事件处理程序。
4. 实际开发中我们很少使用事件捕获,我们更关注事件冒泡。
5. 有些事件是没有泡的，比如onblur、onfocus、 onmouseenter、 onmouseleave



## 4. 事件对象

```javascript
event.onclick = function(event){
      //这个event就是事件对象，我们还喜欢的写成e或者evt
}
event.addEventListener('click',function(event){
      //这个event就是事件对象，我们还喜欢的写成e或者evt     
})
```

兼容性写法：e = e | window.event

- 这个event是个形参，系统帮我们设定为事件对象，不需要传递实参过去。
- 当我们注册事件时，event对象就会被系统自动创建，并以此传递给事件监听器(事件处理函数)

**事件对象常见的属性和方法：**

| 事件对象属性方法   | 说明                                                         |
| ------------------ | ------------------------------------------------------------ |
| e.target           | 返回触发事件的对象                  标准                     |
| e.srcElement       | 返回触发事件的对象                  非标准  ie6-8使用        |
| e.type             | 返回事件的类型  比如 click mouseover 不带 on                 |
| e.cancelBubble     | 该属性阻止冒泡  非标准 ie6-8使用                             |
| e.returnValue      | 该属性 阻止默认事件 (默认行为) 非标准 ie6-8 比如不让链接跳转 |
| e.preventDefault() | 该方法 阻止默认事件 (默认行为) 标准 比如不让链接跳转         |
| e.stopPropagation  | 阻止冒泡 标准                                                |

**e.type**可以获取当前的时间（经过还是点击等）

**与this.的区别：**谁绑定事件，谁就返回谁。e.target是谁触发，谁返回谁

阻止默认事件也可以用retuen false；但是后面的代码不会执行。



## 5. 事件委托

**原理：不是每个子节点单独设置事件监听器，而是事件监听器设置在其父节点上，然后利用1冒泡原理影响设置每个子节点**

```html
<ul>
    <li>gali给给</li>
    <li>gali给给</li>
    <li>gali给给</li>
</ul>
<script>
    var ul = document.querySelector('ul');
    ul.addEventListener('click',function(e){
        e.target.style.backgroundColor = 'pink';
        //e.target为获取当前被触发的对象
     })
</script>
```

以上案例：给ul注册点击事件，然后利用事件对象target来找到当前点击的li，因为点击li，事件会冒泡到ul上，ul有注册事件，就会触发事件监听器。

**事件委托的作用：**我们只操作了一次dom，提高了程序的性能



## 6. 鼠标事件对象

​		**Event**对象代表事件的状态，跟事件相关的一系列信息的集合。现阶段我们主要鼠标事件对象**MouseEvent**和键盘对象**KeyboardEvent**

| 鼠标事件对象 | 说明                                       |
| ------------ | ------------------------------------------ |
| e.clientX    | 返回鼠标相对于浏览器窗口可视化的 X 坐标    |
| e.clientY    | 返回鼠标相对于浏览器窗口可视化的 Y 坐标    |
| e.pageX      | 返回鼠标相对于文档页面的 X 坐标  IE9+ 支持 |
| e.pageY      | 返回鼠标相对于文档页面的 Y 坐标  IE9+ 支持 |
| e.screenX    | 返回鼠标相对于电脑屏幕的X坐标              |
| e.screenY    | 返回鼠标相对于电脑屏幕的Y坐标              |



## 7. 常见键盘事件

| 键盘事件   | 触发条件                                                     |
| ---------- | ------------------------------------------------------------ |
| onkeyup    | 某个键盘按键被松开时触发                                     |
| onkeydown  | 某个键盘按键被按下时触发                                     |
| onkeypress | 某个键盘按键被按下时触发 **但是它不识别功能键 比如 ctrl shift 箭头等** |

获取键盘输入的ascll码值`.keyCode`,`keypress`区分大小写



# 十四. bom

Windows对象是浏览器的顶级对象，它具有双重角色

1. 它是js访问浏览器窗口的一个窗口
2. 它是一个全局对象。定义在全局作用域的变量、函数都会变成window对象的属性和方法。在调用时可以省略window，前面学习的对话框都属于window对象的方法，如alert( )、prompt( )等

**window有一个特殊属性window.name；**



## 1. window对象的常见事件

- **窗口加载事件**

```javascript
window.onload = function(){};
//或者
window.addEventListener('load',function(){});
```

**注意：**

1. 有了window.onload就可以把js代码写在页面元素的上方，因为onload是等页面内容全部加载完毕，再去执行处理函数
2. window.onload传统注册事件方式只能写一次，如果有多个，会以最后一个window.onload为准
3. 如果使用addEventListener则没有限制

```javascript
document.addEventListener('DOMContenLoaded',function(){})
```

此事件触发时。仅当DOM加载完成，不包括样式表、图片、flash等 ie9以上才支持

如果页面的图片很多的话，从用户访问到onload触发需要较长事件，交互效果就不能实现，必然影响用户体验，此时使用此事件比较合适

- **调整窗口大小事件**

```javascript
window.onresize = function(){}
window.addEventListener('resize',function(){});
```

window.onresize是调整窗口大小加载事件，当触发时就调用的处理函数

**注意：**

1. 只要窗口大小发生像素变化，就会触发这个事件
2. 我们经常利用这个事件完成响应式布局。window.innerWidth当前屏幕宽度



## 2. setTimeout( )定时器

```javascript
window.setTimeout(调用函数，[延迟的毫秒数]);
```

setTimeout()方法用于设置一个定时器，该定时器在定时器到期后执行Dion调用函数

```javascript
function time(){
   console.log("时间到了");
}
setTimeout(time,2000);
```



## 3. 停止setTimeout( )定时器

```javascript
window.clearTimeout(timeoutID);
```

clearTimeout()方法取消了先前通过调用setTimeout()建立的定时器。

**注意：**

1. window可以省略
2. 里面的参数就是定时器标识符

```html
<button>停止</button>
<script>
        var btu = document.querySelector('button');
        var time = setTimeout(function () {
            console.log("爆炸了");
        }, 5000)
        btu.addEventListener('click', function () {
            clearTimeout(time);
        });
</script>
```



## 4. setInterval定时器

```javascript
window.setIntercal(回调函数,[间隔的毫秒数]);
```

setInterval()方法重复调用一个函数，每隔这个时间，就去调用一次回调函数。

**注意：**

1. window可以省略
2. 这个调用函数可以**直接写函数，或者写函数名**就或者采取字符串'**函数名()**'三种形式

**停止定时器：**需注意变量作用域的问题，可声明全局：var time = null

```javascript
 clearInterval('定时器名') 
```



## 5. location对象

| location对象属性  | 返回值                           |
| ----------------- | -------------------------------- |
| location.href     | 获取或者设置 整个url             |
| location.host     | 返回主机(域名)                   |
| location.port     | 返回端口号 如果未写返回 空字符串 |
| location.pathname | 返回路径                         |
| location.search   | 返回参数                         |
| location.hash     | 返回片段 常见于链接 锚点         |

**重点为：href和search**



## 6. location对象方法

| location对象方法   | 返回值                                                       |
| ------------------ | ------------------------------------------------------------ |
| location.assign()  | 跟href一样，可以跳转页面(也称为重定向页面)                   |
| location.replace() | 替换当前页面，因为不记录历史，所以不能后退页面               |
| location.reload()  | 重新加载页面，相当于刷新按钮或者f5 如果参数为true 强制刷新 ctrl+f5 |

```html
<button>跳转</button>
<script>
       var btu = document.querySelector('button');
       btu.addEventListener('click',function(){
           location.assign('http://www.baidu.com'); //可回退
       })
</script>
```



## 7.navigator对象

navigator对象包含有关浏览器的信息，它有很多属性，我们最常用的时userAgent，该属性可以返回由客户机

发送服务器的user-agent头部的值



## 8. history对象

window对象给我们提供了一个history对象，与浏览器历史记录进行交互。该对啊行包含用户(在浏览器窗口中)访问过的url

| history对象方法 | 作用                                                       |
| --------------- | ---------------------------------------------------------- |
| back()          | 可以后退功能                                               |
| forward()       | 前进功能                                                   |
| go(参数)        | 前进后退功能 参数如果是1 前进1个页面；如果是-1 后退1个页面 |



# 十五. pc网页特效



## 1. 元素偏移量offset

offset翻译过来就是偏移量，我们使用offset系列相关属性可以动态的得到该元素的位置（偏移）、大小等。

- 获得元素距离带有定位父元素的位置
- 获得元素的大小（宽度高度）
- 注意：返回的数值都不带单位

| offset系列属性       | 作用                                                        |
| -------------------- | ----------------------------------------------------------- |
| element.offsetParent | 返回作为带有定位的父级元素 如果父级元素都没有定位则返回body |
| element.offsetTop    | 返回元素相对带有定位父元素上方的偏移                        |
| element.offsetLeft   | 返回元素相对带有定位父元素左边框的偏移                      |
| element.offsetWidth  | 返回自身包括padding、边框、内容区的宽度、返回数值不带单位   |
| element.offsetHeight | 返回自身包括padding、边框、内容区的高度，返回数值不带单位   |

```html
<div class="father">
        <div class="son"></div>
</div>
<script>
        var f = document.querySelector('.father');
        var s = document.querySelector('.son');
        console.log(f.offsetLeft);
        console.log(s.offsetLeft);
</script>
```

- **offset 与 style 的区别**

**offset**

- offset可以得到任意样式表中的样式值
- offset系列后的的数值是没有单位的
- offsetWidth包含padding+border+width
- offsetWidth等属性是只读属性，只能获取不能赋值
- **所以，我们想要获得元素大小位置，用offset更合适**

**style**

- style只能得到行内样式表的样式值

- style.width获得的是带有单位的字符串

- style.width获得不包含padding和border的值

- style.width是可读写属性，可以获得也可以赋值

- **所以，我们想要给元素怒更改值，则需要用style改变**



## 2. 元素可视区 client

  ​		client翻译过来就是客户端，我们使用client系列的相关属性来获取元素可是去的相关信息。通过client系列的相关属性可以动态的得到该元素的边框大小、元素大小等。

| client系列属性       | 作用                                                         |
| -------------------- | ------------------------------------------------------------ |
| element.clientTop    | 返回元素上边框的大小                                         |
| element.clientLeft   | 返回元素左边框的大小                                         |
| element.clientWidth  | 返回自身包括padding、内容区的宽度，不含边框，返回数值不带单位 |
| element.clientHeight | 返回自身包括padding、内容区的高度，不含边框，返回数值不带单位 |



## 3. 元素滚动 scroll

scroll翻译过来就是滚动，我们使用scroll系列的相关属性可以动态的得到该元素的大小、滚动距离等

| scroll系列属性       | 作用                                           |
| -------------------- | ---------------------------------------------- |
| element.scrollTop    | 返回被卷去的上侧距离，返回数值不带单位         |
| element.scrollLeft   | 返回被卷去的左侧距离，返回数值不带单位         |
| element.scrollWidth  | 返回自身实际的宽度，不含边框，返回数值不带单位 |
| element.scrollHeight | 返回自身实际的高度，不含边框，返回数值不带单位 |

```html
div{overflow:auto;}
div:嗨咯*100
<script>
    var div = document.querySelector('div');
    div.addEventListener('scroll',function(){
          console.log(div.scrollTop);
    });
</script>
```

**overflow:auto；可以加滚动条**

**页面被卷去的头部：**可以 通过 window.pageYOffset 获得 如果是被卷去的左侧 window.pageXOffset

**注意：** 元 素 被 卷 去 头 部 是 **element.scrollTop** ， 如 果 是 页 面 被 卷 去 头 部 则 是 **window.pageOffset**

```javascript
//滚动窗口到某个位置
window.scroll(0,0)
```



## 4. 页面被卷去头部兼容性

需要注意的是，页面被卷去的头部，有兼容性问题，因此被卷区的头部通常有如下几种写法：

1. 声明了DTD，使用document.documentElment.scrollTop
2. 为声明DTD，使用document.body.scrollTop
3. 新方法window.pageYOffset和window.pageXOffset，IE9开始支持



## 5. 立即执行函数

立即执行函数(function(){})() 或者 (function({}))

主要作用：创建一个独立的作用域。避免了命名冲突问题



## 6. pageshow事件触发

下面三种情况都会刷新页面都会触发load事件。

1. a标签的超链接
2. F5或者刷新按钮(强制刷新)
3. 前进后退按钮

但是 火狐中，有个特点，有个“往返缓存”, 这个缓存中不仅保存着页面数据，还保存了DOM和JavaScript的状态;实际上是将整个页面都保存在了内存里。

所以此时后退按钮不能刷新页面。

此时可以使用pageshow事件来触发。这个事件在页面显示时触发，无论页面是否来自缓存。在重新加载页面中，pageshow会在load事件触发后触发；根据事件对象中的persisted来判断是否是缓存中的页面触发的pageshow事件，**注意这个事件给window添加。**



## 7. 三大系列总结

| 三大系列大小对比     | 作用                                                         |
| -------------------- | ------------------------------------------------------------ |
| element. offsetWidth | 返回自身包括padding、边框、内容区的宽度，返回数值不带单位    |
| element.clientWidth  | 返回自身包括padding、内容区的宽度，不含边框，返回数值不带单位 |
| element.scrollWidth  | 返回自身实际的宽度，不含边框，返回数值不带单位               |



## 8. mouseenter鼠标经过

- 当鼠标移动到元素上时就会触发mouseenter事件

- 类似mouseover ,它们两者之间的差别是

- mouseover鼠标经过自身盒子会触发,经过子盒子还会触发。mouseenter 只会经过自身盒子触发
- 之所以这样，就是因为mouseenter不会冒泡
- 跟mouseenter搭配鼠标离开 mouseleave 同样不会冒泡

**mousemove：**子盒子点击后发现没有经过时间就会冒泡，冒到父盒子发现有经过事 件就会触发，所以经过子盒子还是会触发



# 十六. 动画



## 1. 动画原理

通过 setInterval 定时器不断在盒 子原本的距离加 1 个移动距离 加一个结束定时器的条件

**此元素需要定位：position: absolute;**

```html
<div></div>
<script>
        var div = document.querySelector('div');
        var time = setInterval(function(){
            if(div.offsetLeft>=1200){
                clearTimeout(time);
            }else{
                div.style.left = div.offsetLeft+1+'px'; //当前位置加1px
            }
        },20)
</script>
```



## 2. 简单动画封装函数

**注意：**函数需要传两个参数， 动画对象和移动到的距离

```javascript
function animation(obj, value) {
            var time = setInterval(function () {
                if (obj.offsetLeft >= value) {
                    setTimeout(time);
                } else {
                    obj.style.left = obj.offsetLeft + 1 + 'px';
                }
            }, 30);
        };
animation(div,500);
```

```javascript
function animate(obj, target) {
        //为了不因为重复调用定时器造成的动画bug(速度越来越快)，可先清楚之前的定时器
        clearInterval(obj.animate)
        obj.animation = setInterval(function () { //优化：使用var会开辟不同空间，此方法可以给一个元素指定一个定时器
            if (obj.offsetLeft >= target) {
                clearInterval(obj.animation)
            } else {
                obj.style.left = obj.offsetLeft + 1 + 'px'
            }
        }, 1)
        console.dir(obj.animate);
    }
```



## 3. 缓动效果原理

缓动动画就是让元素运动速度有所变化,最常见的是让速度慢慢停下来

**思路:**

1. 让盒子每次移动的距离慢慢变小，速度就会慢慢落下来。
2. 核心算法: (目标值-现在的位置) / 10 做为每次移动的距离 步长
3. 停止的条件是 : 让当前盒子位置等于目标位就停止定时器
4. 需要取整：Math.ceil()

```javascript
    function animate(obj, target) {
        //为了不因为重复调用定时器造成的动画bug(速度越来越快)，可先清楚之前的定时器
        clearInterval(obj.animate)
        obj.animation = setInterval(function () { //优化：使用var会开辟不同空间，此方法可以给一个元素指定一个定时器
            //步长值写到定时器的里面
            var step = Math.ceil((target - obj.offsetLeft) / 10) //取整
            if (obj.offsetLeft >= target) {
                clearInterval(obj.animation)
            } else {
                //(目标值-现在的位置) / 10 做为每次移动的距离
                obj.style.left = obj.offsetLeft + step + 'px'
            }
        }, 15) //一般为15
        console.dir(obj.animate);
    }

    var div = document.querySelector('div')
    animate(div, 500)
```

```javascript
//适配两个按钮出现倒退走的情况
function animate(obj, target) {
        //为了不因为重复调用定时器造成的动画bug(速度越来越快)，可先清楚之前的定时器
        clearInterval(obj.animate)
        obj.animation = setInterval(function () { //优化：使用var会开辟不同空间，此方法可以给一个元素指定一个定时器
            //步长值写到定时器的里面
            var step = (target - obj.offsetLeft) / 10
            step = step > 0 ? Math.ceil(step) : Math.floor(step) //倒退走取整方式不一
            if (obj.offsetLeft >= target) {
                clearInterval(obj.animation)
            } else {
                //(目标值-现在的位置) / 10 做为每次移动的距离
                obj.style.left = obj.offsetLeft + step + 'px'
            }
        }, 15)
        console.dir(obj.animate);
    }

    var div = document.querySelector('div')
    animate(div, 500)
```



## 4. 添加回调函数

**回调函数原理：**函数可以作为一个参数。将这个函数作为参数传单另一个函数里面，当那个函数执行完之后，再执行传进去的这个函数，这个过程就叫做**回调**

```javascript
 function animate(obj, target, callback) {
        console.log(callback);
        //为了不因为重复调用定时器造成的动画bug(速度越来越快)，可先清楚之前的定时器
        clearInterval(obj.animate)
        obj.animation = setInterval(function () { //优化：使用var会开辟不同空间，此方法可以给一个元素指定一个定时器
            //步长值写到定时器的里面
            var step = (target - obj.offsetLeft) / 10
            step = step > 0 ? Math.ceil(step) : Math.floor(step)
            if (obj.offsetLeft >= target) {
                clearInterval(obj.animation)
                if (callback) {
                    callback()
                }
            }
            //(目标值-现在的位置) / 10 做为每次移动的距离
            obj.style.left = obj.offsetLeft + step + 'px'

        }, 15)
    }
```



# 十七. 移动端网页特效



## 1. 触摸 touch 事件

| 触屏touch  | 说明                          |
| ---------- | ----------------------------- |
| touchstart | 手指触摸到一个dom元素时触发   |
| touchmove  | 手指在一个dom元素上滑动时触发 |
| touchend   | 手指从一个dom元素上移开时触发 |



## 2. 触摸事件对象

TouchEvent是一类描述手指在触摸平面（触摸屏、触摸板等）的状态变化的事件。这类事件用于描述一个或多个触点，使开发者可以检测触点的移动，触点的增加或减少，等等

| 触摸列表       | 说明                                               |
| -------------- | -------------------------------------------------- |
| touches        | 正在触摸屏幕的所有手指的一个列表                   |
| targetTouches  | 正在触摸dom元素上的手指的一个列表                  |
| changesTouches | 手指状态发生了改变的列表，从无到有，从有到无的变化 |





# 其他

## 1.截取字符串

```javascript
.substr(起始的位置，截取几个字符)

console.log(location.search); //?uname=andy
var params = location.search.substr(1) 
```

## 2.字符串分割为字符

```javascript
.split('利用分割的符号')
var arr = params.split('=')
console.log(arr);
```

## 3. find

```js
// 当某个遍历项符合条件的时候，find会终止遍历同时返回遍历项
var stu = students.find(function (item) { //此处students为数组对象，单个item为单个对象，.id为查找里层
    return item.id == students.id
})
```











