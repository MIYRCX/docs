> 创建日期：2020
>
> 修改日期：2023-3-11


#

# 一. jQuery的ajax

浏览器中提供的XMLHttpRequest用法比较复杂，所以jQ对此对象进行了封装，提供了一系列ajax相关的函数，极大的降低了ajax的使用难度

**发起Ajax请求常用方法如下：**

```javascript
$.get()
$.post()
$.ajax()
```

## 1. $.get()函数的语法

此方法专门用来发起get请求，语法如下：

```javascript
$.get(url,[data],[callback]) //[]表示可选
```

| 参数名   | 参数类型 | 是否必选 | 说明                     |
| -------- | -------- | -------- | ------------------------ |
| url      | string   | 是       | 要请求的资源地址         |
| data     | object   | 否       | 请求资源期间要携带的参数 |
| callback | function | 否       | 请求成功时的回调函数     |

```javascript
//不带参数：返回所有
$(function () {
    $('#btnGet').on('click', function () {
        $.get('http://liulongbin.top:3006/api/getbooks', function (res) {
            console.log(res);
        })
    })
})
```

```javascript
//带参数：返回匹配此id的结果
$(function () {
    $('#btn').on('click', function () {
        $.get('http://liulongbin.top:3006/api/getbooks', { id: 1 }, function (res) {
            console.log(res);
        })
    })
})
```

## 2. $.post()函数的语法

此方法专门用来发起post请求，语法如下：

```javascript
$.post(url,[data],[callback])
```

| 参数名   | 参数类型 | 是否必选 | 说明                 |
| -------- | -------- | -------- | -------------------- |
| url      | string   | 是       | 提交数据的地址       |
| data     | object   | 否       | 要提交的数据         |
| callback | function | 否       | 请求成功时的回调函数 |

```javascript
$(function () {
    $('button').on('click', function () {
        $.post('http://liulongbin.top:3006/api/addbook', {
            bookname: '水浒传', author: '施耐庵', publisher: '上海图书出版社'
        }, function (res) {
            console.log(res);
        })
    })
})
```

## 3. $.ajax()函数的语法

相比于前两个，此方法是一个比较综合的函数，允许我们对ajax请求进行更详细的配置：

```javascript
$.ajax({
    type: '',   //请求的方式，例如GET或POST
    url: '',    //请求的URL地址
    data: {},   //这次请求要携带的数据
    success: function (res) { } //请求成功之后的回调函数
})
```

```javascript
//发起get
$(function () {
    $('button').on('click', function () {
        $.ajax({
            type: 'GET',
            url: 'http://liulongbin.top:3006/api/getbooks',
            data: {
                id: 1
            },
            success: function (res) {
                console.log(res);
            }
        })
    })
})
```

```javascript
//post
$(function () {
    $('button').on('click', function () {
        $.ajax({
            type: 'post',
            url: 'http://liulongbin.top:3006/api/addbook',
            data: {
                bookname: '史记shiji',
                author: '司马迁',
                publisher: '上海图书出版社'
            },
            success: function (res) {
                console.log(res);
            }

        })
    })
})
```



# 二. 接口

**接口的概念：**使用ajax请求数据时，被请求的URL地址，就叫做**数据接口**。同时每个接口必须由有**请求方式**



**接口文档：**接口文档，顾名思义就是接口的说明文档。它是我们调用接口的依据。好的接口文档包含了对接口URL，参数以及输出内容的说明，我们参照接口文档就能方便的知道接口的作用，以及接口如何进行调用。



**接口文档的组成部分：**

​	接口文档可以包含很多信息，也可以按需进行精简，不过，一个合格的接口文档，应该包含以下6项内容，从而为接口的调用提供依据:

1. 接口名称:用来标识各个接口的简单说明，如登录接口，获取图书列表接口等。
2. 接口URL:接口的调用地址。
3. 调用方式:接口的调用方式，如GET或 POST。
4. 参数格式:接口需要传递的参数，每个参数必须包含参数名称、参数类型、是否必选、参数说明这4项内容。
5. 响应格式:接口的返回值的详细描述，一般包含数据名称、数据类型、说明3项内容。
6. 返回示例(可选)︰通过对象的形式，例举服务器返回数据的结构。

**示例：**

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310164753745.png" alt="image-20230310164753745" style="zoom:50%;" />





# 三. form表单的基本使用

`<form>`标签用来采集数据，属性是用来规定如何把**采集到的数据发送到服务器**



<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310164822233.png" alt="image-20230310164822233" style="zoom:50%;" />



## 1. 通过ajax提交表单数据

**监听表单提交方式：**

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310164832369.png" alt="image-20230310164832369" style="zoom:50%;" />

**阻止表单的默认提交行为：**

当监听到表单的提交事件以后，可以调用事件对象的函数，来阻止表单的提交和页面的跳转：

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310164840637.png" alt="image-20230310164840637" style="zoom:50%;" />

## 2. 快速获取表单中的数据

为了简化表单中数据的获取操作，jQuery提供了serialize()函数，**必须添加name属性**，其语法格式：

```javascript
$(selector).serialize() // 可以一次性获取到表单中的所有数据
```

```javascript
$('#f1').submit(function (e) {
        e.preventDefault()
        var data = $(this).serialize()
        console.log();
})
```





# 四. 模板引擎

它是根据程序员指定的**模板结构**和**数据**，自动生成一个完整的html页面

1. 减少了字符串的拼接操作
2. 使代码结构更清晰
3. 使代码更易于阅读与维护

使用步骤：

1. 导入art-template
2. 定义数据
3. 定义模板
4. 调用template
5. 渲染HTML结构

aet-template提供了{{}}这种语法格式，在{{}}内可以进行变量输出，或循环数组等操作，这种{{}}语法在art-templata中被称为标准语法

```html
<div class="box"></div>
<script id="mb" type="text/html">
        <h1>{{name}}-------{{age}}</h1>
</script>
<script>
        var data = { name: 'zs', age: 10 }
        var result = template('mb', data)
        console.log(result);
        document.querySelector('.box').innerHTML = result
</script>
```







## 1. 语法

**标准语法-输出**

```javascript
{{value}}
{{obj.key}}
{{abj['key']}}
{{a?b:c}}
{{a+b}}
```

在{{}}语法中，可以进行**变量**的输出、**对象属性**的输出、**三元表达式**输出、**逻辑或**输出，**加减乘除等表达式**输出



------

**标准语法-原文输出**

```
{{@ value}}
```

如果要输出的value值中，包含了HTML标签结构，则需要使用原文输出语法，才能保证HTML标签被正常渲染



------

标准语法-条件输出

如果要实现条件输出，则可以在{{}}中使用if...else...if.../if的方式，进行按需输出

```javascript
{{if value}} 按需输出的内容
{{if $value.sex==0}} 按需输出的内容 {{else if $value.sex==1}} 按需输出的内容 {{/if}}
```



# 五. XHR请求方式

```javascript
//创建XHR对象
var xhr = new XMLHttpRequest()
//调用open函数
xhr.open('get', 'http://www.liulongbin.top:3006/api/getbooks')
//调用send发起请求
xhr.send()
//监听onreadystatechange事件
xhr.onreadystatechange = function () {
    //监听xhr对象的请求状态readyState；与服务器响应的状态status
    if (xhr.readyState == 4 && xhr.status == 200) {
        //获取响应的数据
        console.log(xhr.responseText);
    }
}
```

- **xhr对象的readystate属性**

此属性用来表示当前的ajax请求所处的状态，每个ajax请求必然处于以下的状态的一个

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310164851270.png" alt="image-20230310164851270" style="zoom:50%;" />





## 1. 使用xhr发起带参数的get请求

只需要在diaoyongxhr,open期间，为url地址指定参数即可：

```javascript
xhr.open('get', 'http://www.liulongbin.top:3006/api/getbooks?id=1')
```

这种在url地址后面拼接的参数叫做**查询字符串**:

**定义：**查询字符串（url参数）是指在url的末尾加上用于向服务器发送信息的字符串（变量）

**格式：**将英文的**?**放在URL末尾，然后再加上**参数=值**，向加上多个参数的话，使用**&**符号进行分隔。以这个形式，可以将想要发送给服务器的数据添加到URL中。

**GET请求写到参数的本质：**

无论使用$.ajax()，还是使用$.get()，又或者直接使用xhr对象发起GET请求，当需要携带参数的时候，本质上，都是直接将参数以查询字符串的形式，追加到URL地址的后面，发送到服务器的



## 2. 使用xhr发起POST请求

**步骤：**

1. 创建xhr对象
2. 调用xhr.open()函数
3. **设置Content-Type属性（固定写法）**
4. 调用xh.send()函数，同时指定要发送的数据
5. 监听xhr.onreadystatechange事件

```javascript
var xhr = new XMLHttpRequest()
xhr.open('post', 'http://www.liulongbin.top:3006/api/addbooks')
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
xhr.send('bookname=水浒传&author=施耐庵&publisher=上海图书出版社')
xhr.onreadystatechange = function () {
    if (xhr.status === 200 && xhr.readyState === 4) {
        console.log(xhr.responseText);
    }
}
```



## 3. URL编码

URL地址中，只允许出现英文相关的字母、标点符号、数字、因此，在URL地址中不允许出现中文字符

如果URL中需要包含中文这样的字符，则需要对中文字符进行**编码**（转义）

**URL编码的原则：**使用安全的字符（没有特殊用途或者特殊意义的可打印字符）去表示那些不安全的字符

URL编码原则的通俗理解：使用**英文字符**去表示非英文字符



浏览器提供了URL编码与API分别是：

- encodeURI()  编码的函数
- decodeURI()  解码的函数

```javascript
console.log(encodeURI('程序员')); // %E7%A8%8B%E5%BA%8F%E5%91%98
console.log(decodeURI('%E7%A8%8B%E5%BA%8F%E5%91%98')) // 程序员
```



# 六. 数据交换格式

数据交换格式，就是服务器端与哭护短之间进行数据传输与交换的格式。

前段领域，经常提及的两种数据交换格式分别是XML和JSON。其中XML用的非常少，所以重点学习JSON



## 1. XML

XML为课扩展标记语言。因此XML和HTML类似也是一种标记语言

XML和HTML虽然都是标记语言，但是他们两者之间没有任何关系。

- HTML被设计用来描述网页上的内容，是网页内容的载体
- XML被设计用来传输和存储数据，是数据的载体

**XML的缺点：**

- XML格式臃肿，和数据无关的代码多，体积大，传输效率低
- 在Javascript 中解析XML比较麻烦



## 2. JSON

概念：JSON即JS对象表示法，简单来讲，**JSON就是JS对象和数组的字符串表示法**，它使用文本表示一个JS对象或数组的信息，因此，**JSON的本质是字符串**

作用：JSON是一种**轻量级的文本数据交换格式**，在作用上类似于XML，专门用于存储和传输数据，但是JSON比XML更小、更快、更易解析。**JSON已经成为了主流的数据交换格式**

**JSON的两种结构：**

- **对象结构：**对象结构在JSON中表示为{}括起来的内容，数据结构为{key:value,key:value,...}的键值对结构。其中，key必须是使用**英文的双引号包裹**的字符串，value的数据类型可以是**数字、字符串、布尔值、null、数组、对象**6种类型
- **数组结构：**数组结构在JSON中表示为[ ]括起来的内容，数据结构为["java","javascript",...]。少数族中数组的类型可以是**数字、字符串、布尔值、null、数组、对象**6种类型

```javascript
["java", "python", "php"]
[100, 200, 300]
[true, false, null]
[{ "name": "zs", "age": 18 }, { "name": "ls", "age": 20 }]
[["苹果", "榴莲", "椰子"], [3, 6, 2]]
```



**JSON语法注意事项：**

1. 属性名必须使用双引号包裹
2. 字符串类型的值必须使用双引号包裹
3. JSON中不允许使用单引号表示字符串
4. JSON中不能写注释
5. JSON的最外层必须是对象或数组格式
6. 不能使用undefined或函数作为JSON的值

**JSON的作用：**在计算机与网络之间存储个传输数据

**json的本质：**用字符串来表示js对象数据或数组数据



## JSON和JS对象的关系

JSOn是JS对象的字符串表示法，它使用文本表示一个JS对象的信息，本质上是一个字符串

```javascript
var obj = { a: 'hello', b: 'world' }	//这是一个对象
var json = '{ "a": "hello", "b": "world" }'	//这是一个JSON字符串，本质是一个字符串
```



**序列化和反序列化**

把**数据对象转换为字符串**的过程，叫做**序列化**，例如：调用JSON.stringify()函数的操作，叫做JSON序列化

把**字符串转换为数据对象**的过程，叫做**反序列化**，例如调用JSON.parse()函数的操作，叫做JSON反序列化





封装ajax函数

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310164900578.png" alt="image-20230310164900578" style="zoom:50%;" />

 







# 七. XHR Level2



**旧版XMLHttpRequest的缺点：**

1. 只支持文本数据的传输无法用来读取和上传文件
2. 传送和接受数据时，没有进度信息，只能提示有没有完成



**XMLHttpRequest Level2的新功能：**

1. 可以设置HTTP请求的时限
2. 可以使用FormData对象管理表单数据
3. 可以上传文件
4. 可以获得数据传输的进度信息



## 1. 设置HTTP请求时限

有事ajax操作很耗时，而且无法预知要花多少时间。如果网速慢，用户会等很久。新版本的XMLHttpRequest对象，增加了`timeout`属性，可以设置HTTP请求的时限：

```javascript
xhr.timeout = 2000 
```

最长等待时间，过了就停止HTTP请求，与之匹配的还有timeout事件，用来指定回调函数

```javascript
xhr.ontimeout = function (e) {
       alert('请求超时')
}
```



## 2. FormData对象管理表单数据

ajax操作往往用来提交表单数据，为了方便表单处理，H5新增了一个FormData对象，可以模拟表单操作：

```javascript
// 创建实例
var fd = new FormData()
//调用append函数，向fd中追加数据
fd.append('uname', 'zs')
fd.append('pw', '123')

var xhr = new XMLHttpRequest()
xhr.open('post', 'http://www.liulongbin.top:3006/api/formdata')
xhr.send(fd)
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
        console.log(JSON.parse(xhr.responseText));
    }

}
```

FormData对象也可以用来**获取网页表单**的值

```javascript
// 获取表单元素
var form = document.querySelector('#form1')
form.addEventListener('submit', function (e) {
    // 阻止表单默认提交行为
    e.preventDefault()
    var fd = new FormData(form)

    var xhr = new XMLHttpRequest()
    xhr.open('post', 'http://www.liulongbin.top:3006/api/formdata')
    xhr.send(fd)

    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
            console.log(JSON.parse(xhr.responseText));
        }
    }
})
```



## 3. 上传文件

新版对象，不仅可以发送文本信息，还可以上传文件

**实现步骤：**

1. 定义UI结构
2. 验证是否选择了文件
3. 向formData追加文件
4. 使用xhr发起上传文件的请求
5. 监听onreadystatechange事件

```javascript
var files = document.querySelector("#file1").files; // 这是一个数组
if (files.length <= 0) {
    return alert("请选择要上传的文件");
}

fd.append("avatar", files[0]); //将用户选择的文件添加到formdata中
```

```javascript
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
        var data = JSON.parse(xhr.responseText);
        console.log(data);
        if (data.status === 200) {
            document.querySelector("#img").src ="http://www.liulongbin.top:3006" + data.url;
        } else {
            console.log(data.message);
        }
    }
};
```







# 八. jsonp



## 1. 同源策略

**同源：**如果两个页面的协议、域名和端口都相同，则两个页面具有相同的源

例如：http://www.test.com.index.html

| URL                                 | 是否同源 | 原因                  |
| ----------------------------------- | -------- | --------------------- |
| http://www.test.com/other.html      | 是       | 同源                  |
| https://www.test.com/other.html     | 否       | 协议不同(http与https) |
| http://blog.test.com/other.html     | 否       | 域名不同              |
| http://www.test.com:2000/other.html | 否       | 端口不同(默认80)      |
| http://www.test.com:80/other.html   | 是       | 同源                  |

**同源策略：**是**浏览器**提供的一个**安全功能**

通俗为：浏览器规定，A网站的Js不允许和非同源的网站C之间进行资源的交互，例如：

1. 无法读取非同源网页的Cookie、LocalStorage和indexDB
2. 无法解除非同源网页的dom
3. 无法向非同源地址发送ajax请求



## 2. 跨域

同源是指两个URL协议、域名、端口一直，反之则是跨域

出现跨域的根本原因：浏览器的同源策略不允许非同源的URL之间进行资源的交互

网页：http://www.test.com/index.com

接口：http://www.api.com/userlist

注意：浏览器允许发起跨域请求，但是，跨域请求回来的数据会被浏览器拦截，无法被页面获取到



要实现跨域数据请求，最主要的两种解决方案，分别是JSONP和CORS

JSONP：出现早，兼容性好，缺点是只支持GET请求，不支持post请求

CORS：出现的较晚，它是w3c标准，属于跨域ajax请求的根本解决方案，缺点是不兼容某些低版本的浏览器



## 3. JSONP

jsonp是json的一种“使用模式”，可用于解决主流浏览器的跨域数据访问的问题

实现原理：由于**浏览器同源策略**的限制，网页中**无法通过ajax请求非同源的接口数据**，但是`<script>`标签不收浏览器同源策略的影响，可以通过src属性，请求非同源的js脚本

因此，JSONP的时限原理，就是通过`<script>`标签的src属性，请求跨域的数据接口，并通过**函数调用**的形式，接受跨域接口响应回来的数据。



------

**jquery中的jsonp**

jq提供的$.ajax()函数，除了可以发起真正的ajax数据请求之外，还能够发起JSONP数据请求

```javascript
$.ajax({
    url: 'http://ajax.frontend.itheima.net:3006/api/jsonp?name=zs&age=20',
    dataType: 'jsonp',
    success: function (res) {
        console.log(res);
    }
})
```

默认情况下，使用jq发起jsonp请求，会自动携带一个callback=jQueryxxx的参数，后者是随机生成的一个回调函数的名称





------

**自定义参数及会回调函数名称**

在使用jQurey发起jsonp请求时，如果想要自定义jsonp的参数以及回调函数名称，可以通过如下两个参数来指定：

```javascript
$.ajax({
    url: 'http://ajax.frontend.itheima.net:3006/api/jsonp?name=zs&age=20',
    dataType: 'jsonp',
    jsonp: 'callback',
    jsonpCallback: 'abc',
    success: function (res) {
        console.log(res);
    }
})
```



**jQuery中JSONP的实现过程**

jQuery中JSONP也是通过`<script>`标签的src属性实现跨域数据访问的，只不过，jquery采用的是动态创建和一处`<script>`标签的方式，来发起JSONP数据请求

- 在发起JSONP请求的时候，动态向`<header>`一个`<script>`标签
- 在JSONP请求成功以后，动态从`<header>`中移除刚才append进去的`<script>`标签



# 九. 输入框的防抖



**防抖策略**(debounce)是当时间被触发后，**延迟n秒**后再**执行回调**，如果在这**n秒内又被触发**，则**重新计时**

用户在输入框中连续输入一串字符时，可以通过防抖策略，只在输入完成后才查询请求，这样可以有效减少请求次数，节约请求资源

