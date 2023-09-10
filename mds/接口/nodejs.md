> 创建日期：2021
>
> 修改日期：2023-9-2

#

# 一. fs模块

浏览器中的js没有文件操作的能力，但是node中的js有

fs使file-system的简写，就是文件系统的意思

在node中如果想要进行文件操做，就必须引入fs这个核心模块，在fs中提供了文件操作相关的API

------

## **1. fs.readFile**用来读取文件

```js
// 1.使用require方法加载fs核心模块
var fs = require('fs');
// 2.读取文件
fs.readFile('test.txt',function(error,data){
    console.log(data.toString()); //<Buffer 68 65 6c 6c 6f 20 6e 6f 64 65> 此处为二进制转16进制
    // 以上直接使用数据会存在读取失败的问题，所以需要判断是否读取成功
    if(error){
        console.log('读取文件失败');
    }else {
        console.log(data.toString());
    }
}); //此处的data数据可使用toString()转换

fs.readFile('test.txt','utf-8',function(error,data) // 2位可选参数，意味着直接按照编码转
```

以上的回调函数参数

```js
// 第一个参数就是要读取的文件路径
// 第二个参数就是一个回调函数
// 成功
    // data 数据
    // error undefined
// 失败
    // data undefined
    // error 错误对象
```

------



## **2. fs.write()：**写入文件

```js
var fs = require('fs');
// 参数一：文件路径
// 参数二：文件内容
// 参数三：回调函数
    //error
    //成功：   文件写入成功      error使null 
    //失败：   文件写入失败      error就是错误对象    
fs.writeFile('./你好.txt','你好',function(error){
    // console.log("文件写入成功");
    // 如果写入失败，如文件名异常需要提示
    if(error){
        console.log('写入失败');
    }else {
        console.log('写入成功');
    }
})
```



## 3. appendFile / Sync 追加写入

appendFile 作用是在文件尾部追加内容，appendFile 语法与 writeFile 语法完全相同 语法:

```js
fs.appendFile(file, data[, options], callback) 
fs.appendFileSync(file, data[, options])
```

案例：

```js
fs.appendFile('./座右铭.txt','择其善者而从之，其不善者而改之。', err => {
if(err) throw err;
console.log('追加成功')
});
fs.appendFileSync('./座右铭.txt','\r\n温故而知新, 可以为师矣');
```



##  4. createWriteStream 流式写入

创建通道随时可写入

```
 fs.createWriteStream(path[, options])
```

```js
let ws = fs.createWriteStream('./观书有感.txt');
ws.write('半亩方塘一鉴开\r\n');
ws.write('天光云影共徘徊\r\n');
ws.write('问渠那得清如许\r\n');
ws.write('为有源头活水来\r\n');
ws.end()
```

> 程序打开一个文件是需要消耗资源的 ，流式写入可以减少打开关闭文件的次数。 流式写入方式适用于 大文件写入或者频繁写入 的场景, writeFile 适合于 写入频率较低的场景



## 5. createReadStream 流式读取

```js
//创建读取流对象
let rs = fs.createReadStream('./观书有感.txt');
//每次取出 64k 数据后执行一次 data 回调
rs.on('data', data => {
console.log(data);
console.log(data.length);
});
//读取完毕后, 执行 end 回调
rs.on('end', () => {
console.log('读取完成')
})

```





## 6. 文件移动与重命名 

在 Node.js 中，我们可以使用 rename 或 renameSync 来移动或重命名 文件或文件夹 语法： 

```js
fs.rename(oldPath, newPath, callback) 
fs.renameSync(oldPath, newPath) 
参数说明： oldPath 文件当前的路径 newPath 文件新的路径 callback 操作后的回调 
```

代码示例： 

```js
fs.rename('./观书有感.txt', './论语/观书有感.txt', (err) =>{
if(err) throw err;
console.log('移动完成')
});
fs.renameSync('./座右铭.txt', './论语/我的座右铭.txt')
```



## 7. 文件删除 

在 Node.js 中，我们可以使用`unlink`或`unlinkSync`来删除文件 

语法： 

```js
fs.unlink(path, callback) fs.unlinkSync(path) 
参数说明： path 文件路径 callback 操作后的回调
```

代码示例：

```js
const fs = require('fs');
fs.unlink('./test.txt', err => {
if(err) throw err;
console.log('删除成功');
});
fs.unlinkSync('./test2.txt');
```



##  8. mkdir 创建文件夹

 在 Node.js 中，我们可以使用 mkdir 或 mkdirSync 来创建文件夹 语法：

```js
 fs.mkdir(path[, options], callback)
 fs.mkdirSync(path[, options])
```

案例：

```js
fs.mkdir('./page', err => {
if(err) throw err;
console.log('创建成功');
});
//递归异步创建
fs.mkdir('./1/2/3', {recursive: true}, err => {
if(err) throw err;
console.log('递归创建成功');
});
//递归同步创建文件夹
fs.mkdirSync('./x/y/z', {recursive: true});
```



## 9. rmdir 删除文件夹 

在 Node.js 中，我们可以使用 rmdir 或 rmdirSync 来删除文件夹 语法：

```js
fs.rmdir(path[, options], callback) 
fs.rmdirSync(path[, options])
```

案例：

```js
//异步删除文件夹
fs.rmdir('./page', err => {
if(err) throw err;
console.log('删除成功');
});
//异步递归删除文件夹
fs.rmdir('./1', {recursive: true}, err => {
if(err) {
console.log(err);
}
console.log('递归删除')
});
//同步递归删除文件夹
fs.rmdirSync('./x', {recursive: true})
```









# 二. path模块



```js
path.basename   // 获取一个路径的文件名
path.dirname    // 获取一个路径中的目录部分 (路径)
path.extname    // 获取一个路径中的扩展名部分
path.parse  // 把一个路径转为对象
path.join   // 路径拼接，2个参数 ../会抵消前面的一层路径
path.isAbsolute // 判断一个路径是否是绝对路径
```



在每个模块中，除了`require`、`exports`等模块相关api之外，还有两个特殊的成员

- `__dirname`当前文件所处的目录
- `__filename`可以用来获取当前文件的绝对路径



node的文件操作路径被设计为相对于执行**node命令所处的路径**，所以使用绝对路径

为了避免手动拼接带来的错误所以使用`path.join()`辅助拼接

```js
fs.readFile(path.join(__dirname)+'./a.txt',function(err,data){})
```

模块中的路径表示不受影响，只有文件操作会

> 相对路径中所谓的 当前目录 ，指的是 命令行的工作目录 ，而并非是文件的所在目录





# 三. http

## 1. http协议

HTTP（hypertext transport protocol）协议；中文叫**超文本传输协议** ，是一种基于TCP/IP的应用层通信协议

这个协议详细规定了`浏览器`和万维网`服务器`之间互相通信的规则。

 协议中主要规定了两个方面的内容

- 客户端：用来向服务器发送数据，可以被称之为请求报文 
- 服务端：向客户端返回数据，可以被称之为响应报文 

> 报文：可以简单理解为就是一堆字符串 二、请求报文的组成 请求行 请求头 空行 请求体



<img src="C:\Users\32435\AppData\Roaming\Typora\typora-user-images\image-20230902160710660.png" alt="image-20230902160710660" style="zoom: 25%;" />



<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230902160741691.png" alt="image-20230902160741691" style="zoom: 50%;" />



## 2. 创建 HTTP 服务



可以使用node构建web服务器 在node中专门提供了核心模块：http
http模块的职责就是帮你创建编写服务器的

```javascript
// 1.加载模块
var http = require('http');

// 2.使用http.creatServer()方法创建一个web服务器
//  返回一个Server实例
var server = http.createServer();

// 3.服务器的功能：对数据的服务
//  发请求
//  接收请求
//  处理请求
//  给个反馈（发送响应）

//  注册request请求事件 当客户端请求过来，就会自动触发服务器的request请求事件，然后执行第二个参数：回调处理
server.on('request', function () {
    console.log('请求过来了');
})

// 4.绑定端口号，启动服务
server.listen(3000, function () {
    console.log('服务器启动成功');
})
```



以上只能通过浏览器发送请求，不能响应。下面则是响应

request请求事件处理函数，需要接收两个参数：

- request请求对象：请求对象可以用来获取客户端的一些请求信息，例如请求路径
- response响应对象：响应对象可以用来给客户端发送响应消息

```js
//请求处理函数
server.on('request', function (request, response) {
    console.log('请求过来了，路径是' + request.url);
    // response对象有一个方法：write    可以用来给客户端发送响应数据
    // write可以使用多次，但是最后一定要使用end来结束响应，否则客户端会一直等待
    response.write('hello');
    response.end();
})
```

> 思考：由于现在我们的服务器能力较弱，无论什么请求，都只能响应hello，那怎么请求不同的路径时响应不同的结果




```js
    if (request.url == '/') {
        response.write('index');
        response.end();
    } else if (request.url == '/login') {
        response.write('登录');
        response.end();
    }
```

上面的方式比较麻烦，推荐使用end的同时直接发送 res.end('hello');

响应内容只能是二进制或者字符串

```js
res.end(JSON.stringify(products))  //此方法可以将数组转化成字符串
```

------



## 3. 简写方式

```js
var http = require('http')
var fs = require('fs')

http
    .createServer(function (req, res) {

    })
    .listen(3000,function () {
        console.log('服务器开启');
    })
```



## 4. 重定向

```js
res.statusCode = 302    // 设置重定向状态码
res.setHeader('location', '/') // 指定去向
```



```js
// express的重定向
res.redirect('/')
```





# 四. npm与包



## 1. npm

> npm网站：npmjs.com

npm的第二层含义就是一个命令行工具，只要你安装了node就已经安装了npm

```
npm -version  //查看版本
npm install --global npm  //升级
```

**解决npm被墙**  安装淘宝的cnpm：

```shell
npm install --global cnpm
#在任意目录执行都可以
```

接下来安装包的时候替换成cnpm

```shell
#还是走国外的npm服务器
npm install jquery

#使用cnpm就会通过淘宝的服务器下载
cnpm install jquery
```

如果不想安装`cnpm`又想使用淘宝的服务器来下载：

```shell
npm install jquery --registry=http://registry.npm.taobao.org
```

还可以将这个选项接入配置文件中：

```shell
npm config set registry http://registry.npm.taobao.org

#查看npm配置信息
npm config list
```



被安装到项目的node_modules目录中的包，都是项目包

项目包分为2类：

- **开发依赖包 ** 被记录到devDependencies节点中的包，只在开发期间会用到
- **核心依赖包**  被记录到dependencies节点中的包,在开发期间和项目上线之后都会用到

```shell
npm i 包名 -D #开发依赖包
npm i 包名    #核心依赖包
```

全局包：

```shell
npm i 包名 -g #全局包  会安装到c盘···目录下
npm uninstall 包名 -g #卸载全局包
```



i5ting_toc可以将md文档转换为html的小工具

```shell
npm install -g i5ting_toc
i5ting_toc -f sample.md -o
```



##  2. package.json

`dependencies`选项可以用来帮我们保存包的依赖信息

如果node_modules删除了也不用担心，只需要在项目里输入`npm install`就会自动把依赖下载回来

- 建议每个项目的根目录都有一个`package.json`文件
- 建议执行`npm install`包名的时候都加上`--save`这个选项，目的是用来保存依赖信息
- 此文件可以通过`npm init`初始化出来  -y可跳过向导









# 五. 简单模块化

require是一个方法，它的作用就是用来加载模块的。

require 方法有两个作用

1. 加载文件模块并执行里面的代码
2. 拿到被加载文件模块导出的接口对象

在Node中，模块有三种：

1. 第三方模块，如（art-template）
2. 具名的核心模块，例如 `fs`、`http`
3. 用户自定义编写的文件模块

在node中，没有全局作用域，只有模块作用域

在每个文件模块中都提供了一个对象：`exports`，`exports`默认就是一个空对象

![image-20230310165343648](https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230310165343648.png)



https://tool.oschina.net/

## 1. 加载require

语法：

```js
var 自定义变量名称 = require
```

两个作用：

- 执行被加载模块中的代码
- 得到被加载模块中的`exports`导出接口对象



## 2. url模块

url的parse方法可以快速分析路径并生成对象

```js
// parse(url路径，[true]) 可选项true则将query转换为对象
var url = require('url')
var obj = url.parse('http://127.0.0.1:3000/pinglun?name=12312&message=1231233')
console.log(obj);
Url {
  protocol: 'http:',
  slashes: true,
  auth: null,
  host: '127.0.0.1:3000',
  port: '3000',
  hostname: '127.0.0.1',
  hash: null,
  search: '?name=12312&message=1231233',
  query: [Object: null prototype] { name: '12312', message: '1231233' },
  pathname: '/pinglun',
  path: '/pinglun?name=12312&message=1231233',
  href: 'http://127.0.0.1:3000/pinglun?name=12312&message=1231233'      
}
```

其中的pathname可以快速拿到当前的访问的目录，query可以快速拿到数据



## 3. 导出exports

- node中是模块作用域，默认文件中所有的成员只在当前文件模块有效
- 对于希望可以被其他模块访问的成员，我们就需要把这些公开的成员都挂载到`exports`接口对象中就可以了

**导出多个成员（必须在对象中）：**

```js
exports.a = 123
exports.b = '123'
exports.c = function () {
    console.log('123');
}
exports.d = {
    foo: 'bar'
}
```

**导出单个成员（拿到的就是：函数、字符串）：**

```js
moudule.exports = 'hello'
```

以下情况会覆盖：

```js
module.exports = '123'
//以后者为准
module.exports = function () {
    console.log('123');
}
//也可以导出多个成员
module.exports = {
    add: function () {
        console.log('123');
    },
    str: '123'
}
```







## 6. nodemon

可以使用第三方命令行工具：`nodemon`帮我们解决频繁修改完代码重启服务器问题

```shell
npm install nodemon -g
```

安装完后使用：

```shell
node app.js  #旧
nodemon app.js  #新
```





## 7. 加密



**md5:**

```shell
npm install md5
const md5 = require('md5')
md5('message')
md5(md5('message'))
```



**bcrypt:**

```shell
npm install bcrypt
const bcrypt = require('bcrypt')
 // 参数1：原密码  参数2：随机盐的长度
userinfo.password = bcrypt.hashSync(userinfo.password, 10)

// 将2个密码比对 返回布尔值  参数1：提交的  参数2：数据库的
const compareResult = bcrypt.compareSync(req.body.oldPwd, result[0].password) 
```





## 8. 表单验证joi

```js
npm install joi
npm i @escook/express-joi
// 新建规则 /schema/user.js

/**
 * string() 值必须是字符串
 * alphanum() 值只能是包含 a-zA-Z0-9 的字符串
 * min(length) 最小长度
 * max(length) 最大长度
 * required() 值是必填项，不能为 undefined
 * pattern(正则表达式) 值必须符合正则表达式的规则
 */


// 到如定义验证规则的包
const joi = require('joi')

// 定义规则
const username = joi.string().min(1).max(10).required()
const password = joi.string().pattern(/^[\S]{6,12}$/).required()

// 定义验证登录注册表单数据的规则对象
exports.reg_login_chaema = {
    body: {
        username,
        password
    }
}
// 路由模块使用

// 导入数据验证包
const expressjoi = require('@escook/express-joi')
// 导入需要的验证规则对象
const { reg_login_chaema } = require('../schema/user.js')

router.post('/reguser', expressJoi(reg_login_schema), userHandler.regUser)
// 错误级别中间件
const joi = require('joi')

app.use((err, req, res, next) => {
    // 验证失败导致的错误
    if (err instanceof joi.ValidationError) return res.cc(err)
    // 未知错误
    res.cc(err)
})

```

**比较：**

```js
const compareResult = bcrypt.compareSync(userinfo.password, result[0].password) // 参数1：表单的 参数2：数据库的
if (!compareResult) return res.cc('密码错误')
```





## 9. multer提交数据

一个 HTML 表单中的 enctype 有三种类型

- application/x-www-urlencoded
- multipart/form-data
- text-plain

默认情况下是 application/x-www-urlencoded，当表单使用 POST 请求时，数据会被以 x-www-urlencoded 方式编码到 Body 中来传送，而如果 GET 请求，则是附在 url 链接后面来发送。GET 请求只支持 ASCII 字符集，因此，如果我们要发送更大字符集的内容，我们应使用 POST 请求。

如果要发送大量的二进制数据（non-ASCII），application/x-www-form-urlencoded 显然是低效的，因为它需要用 3 个字符来表示一个 non-ASCII 的字符。因此，这种情况下，应该使用 “multipart/form-data” 格式。

**安装：**

```shell
npm i multer
```



```js
// 导入解析 formdata 格式表单数据的包
const multer = require('multer')
// 导入处理路径的核心模块
const path = require('path')

// 创建 multer 的实例对象，通过 dest 属性指定文件的存放路径
const upload = multer({ dest: path.join(__dirname, '../uploads') })
// 发布新文章的路由
// upload.single() 是一个局部生效的中间件，用来解析 FormData 格式的表单数据
// 将文件类型的数据，解析并挂载到 req.file 属性中
// 将文本类型的数据，解析并挂载到 req.body 属性中
router.post('/add', upload.single('cover_img'), article_handler.addArticle)
```










# 六. 使用模板引擎

安装：

```shell
npm install art-template
```

该命令在哪执行就会把包下载到哪里，默认会下载到node_modules目录中，目录不要改

**强调：**模板引擎不关心字符串内容，只关心自己能认识的模板标记语法，例如{{ }} (被称为mustache语法，八字胡)

浏览器中运用： 需要引用文件

```html
 <script src="./node_modules/art-template/lib/template-web.js"></script>
    <script type="text/template" id="tpl">
        我叫：{{name}}
        今年{{age}}岁了
        我来自{{province}}
        我喜欢:{{each hobbies}} {{$value}} {{/each}}
    </script>
    <script>
        var ret = template('tpl', {
            name: 'jack',
            age: 18,
            province: '南极',
            hobbies: [
                '唱',
                '跳',
                'rap',
                '篮球'
            ]
        })
        console.log(ret);
    </script>
```



# 七. express

安装express

```shell
npm install --save express
```

使用：

```js
var express = require('express')
//1.创建app
var app = express()

app.use('/public/',express.static('./public'))
//app.use('/a/',express.static('./public')) 相当于别名

app.get('/',function(req,res){
    res.send('shehuinode')
})
app.listen(3000,function(){
    console.log('running');
})
```



## 1.基本路由

get

```js
app.get('/',function(req,res){
    res.send('shehuinode')
})
```

post

```js
app.post('/',function(req,res){
    res.send('shehuinode')
})
```



使用：

```js
//app.js
var router = require('./router') //此为新文件
//把路由容器挂载到app服务中
app.use(router)
//router.js
//1.创建一个路由容器
var router = express.Router()
//2.把路由都挂载到路由容器上
router.get('/students/new', function (req, res) { })
//3.把router导出
module.exports = router
```





**为路由模块添加前缀**

访问挂载的模块时，必须添加统一的访问前缀

```js
app.use('/api',Router)
```







## 2. 处理静态资源

网页中加载图片等资源的时候，可以用一下方法

```js
app.use('/public/', express.static('./public/'))
// 当以public开头的时候，去./public/目录中找对应的文件


app.use(express.static('./public/'))
// 当省略第一个参数的时候，访问时url也必须省略
```



## 3.使用模板引擎

**安装：**

```shell
npm install --save art-template
npm install --save express-art-template
npm install --save art-template express-art-template  # 同时下载
```

**配置：**

```js
//第一个参数表示当渲染以.html结尾的文件时，使用模板引擎
app.engine('html', require('express-art-template'))

app.set('./views', path.join(__dirname), './views/')
```

**使用：**

```js
//express为response相应对象提供了一个方法：render，默认不可用，必须配置模板引擎

//res.render('html模板名',{模板数据})

app.get('/', function (req, res) {
    res.render('404.html',{ // 第一个参数不能写路径，默认会去项目中的views目录查找模板文件
        title:'hello'
    })
})
```

**修改默认路径：**

```js
// 如果想要修改默认的views目录，则可以
app.set('views',render函数的默认路径)
```



**配置公共部分：**

新建公共部分的文件，里面直接填入内容

```html
{{include './header.html'}} // 在需要的页面引入
```



**继承：**

为了避免重复，使用继承可以避免。

```html
<!-- layout.html -->
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="../node_modules/bootstrap/dist/css/bootstrap.css">
    {{block 'head'}}{{/block}}

</head>

<body>
    {{include './header.html'}}
    <!-- 挖一个坑 -->

    {{block 'content'}}
    <h1>默认内容</h1>
    {{/block}}


    {{include './footer.html'}}

    <script src="../node_modules/jquery/dist/jquery.js"></script>
    <script src="../node_modules/bootstrap/dist/js/bootstrap.js"></script>
    {{block 'script'}}{{/block}}
</body>
</html>
<!-- index.html -->
{{extend './layout.html'}}

{{block 'head'}}
<style>
    body {
        background-color: pink;
    }
</style>
{{/block}}

{{block 'content'}}
<h1>自己的内容</h1>
{{/block}}

{{block 'script'}}
<script>
    window.alert('index.html自己的js脚本')
</script>
{{/block}}
```



## 4.解析get请求体

```js
var express = require('express')

app.get('/pinglun',function(req,res){
     var comment = req.query //内置api
})
```



## 5.解析post请求体

在express中没有内置获取表单请求体的api，需要一个第三方包：`body-parser`

安装：

```shell
npm install --save body-parser
```

使用：

```js
var bodyParser = require('body-parser')
var express = require('express')
//配置：
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())

app.post('/post', function (req, res) {
    var comment = req.body //获得表单数据  { name: '123123', message: '1231231231' }
})
```



## 6. 路由模块的提取

**基础方式：**

```js
// app.js
var router = require('./router.js')
...
router(app)

// router.js
module.exports= function(app){  // 将其封装成函数传过去
    app.get('/', function (req, res) { })  
}
```

**express提供的方式：** 

```js
// app.js
var router = require('./router.js') // 导入得到router
// 把路由容器挂载到app服务中
app.use(router)

// router.js
var express=require('express')

var router=express.Router() // 使用express创建一个路由容器
router.get('/', function (req, res) { })  // 将路由挂载到router容器中
module.exports=router // 将router导出
```

**注意：所有其他配置必须放置在挂载路由之前**















## 8. 获取url中的动态参数

通过req.params对象，可以访问到url中，通过：匹配到的动态参数

```js
app.get('/user/:id',(req,res)=>{
    console.log(req.params);
}) // 删除文章分类通过id
app.get('/user/:id/:username',(req,res)=>{
    console.log(req.params);
})

{
    id:3,
    username:'zs'
    }
```





# 八. express中间件

中间件特指业务流程的中间处理环节

当一个请求到达express服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理



express中间件本质上就是一个function处理函数，express中间件的格式：

```js
app.get('/',function(req,res,next){
    next()
})
```

**注意：**中间件函数的列表中，必须包含next参数，二路由处理函数中只包含req,res

**next函数**是实现多个**中间件连续调用**的关键，它表示把流转关系**转交**给下一个**中间件**或**路由**



## 1. 全局生效的中间件



**全局生效的中间件：**客户端发起的任何请求，到达服务器之后，都会触发中间件，叫做全局生效的中间件，

通过调用app.use(中间件函数)，即可定义一个全局生效的中间件：

```js
var express = require('express')
var app = express()

// 注册全局生效中间件
app.use(function (req, res, next) {
    console.log('这是中间件函数');
    next() // 把流转关系交给下一个路由或中间件
})

app.listen(3000, function () {
    console.log('服务器启动');
})
```

**作用：**

多个中间件之间，共享同一个req和res，可以在上游的中间件中为req或res对象添加自定义属性或方法，供下游的中间件进行使用

```js
// 挂载当前时间，这样访问所有路径都可以拿到
app.use(req,res,next){
    const time=Date.now()
    req.startTime=time
}

app.get('/',function(req,res){
    console.log(req.startTime)
})
```



## 2. 局部生效中间件

不使用app.user()定义的中间件叫做局部生效的中间件

```js
const fn = (req, res, next) => {
    console.log('调用了局部中间件');
    next()
}

app.get('/', fn, (req, res) => res.send('Hello World!'))

// 同时使用多个中间件
app.get('/', fn1,fn2 ,(req, res) => res.send('Hello World!'))
app.get('/', [fn1,fn2] ,(req, res) => res.send('Hello World!'))
```



## 3. 错误级别中间件

作用：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题

格式：必须要有4个形参

**注意：**必须注册在所有路由之后

```js
app.get('/', (req, res) => {
    throw new Error('服务器错误')
    res.send('Hello World!')
})

app.use((err, req, res, next) => {
    console.log('发生了错误' + err.message);
    res.send('服务器错误' + err.message)
})
```





# 九、会话控制



##  1. cookie 

- cookie 是 HTTP 服务器发送到用户浏览器并保存在本地的一小块数据 
- cookie 是保存在浏览器端的一小块数据 cookie 是按照域名划分保存的



cookie 的特点 浏览器向服务器发送请求时，会**自动**将`当前域名下`可用的 cookie 设置在请求头中，然后传递给服务器

这个请求头的名字也叫 cookie ，所以将 cookie 理解为一个 HTTP 的请求头也是可以的



express 中可以使用 `cookie-parser `进行处理

```shell
npm i cookie-parser
```

```js
const express = require('express');
const cookieParser = require('cookie-parser');
const app = express();

app.use(cookieParser());

// 设置 cookie
app.get('/set-cookie', (request, response) => {
    // 不带时效性
    response.cookie('username', 'wangwu');
    // 带时效性
    response.cookie('email', '23123456@qq.com', { maxAge: 5 * 60 * 1000 });
    //响应
    response.send('Cookie的设置');
});

// 读取 cookie
app.get('/get-cookie', (request, response) => {
    //读取 cookie
    console.log(request.cookies);
    //响应体
    response.send('Cookie的读取');
});

// 删除cookie
app.get('/delete-cookie', (request, response) => {
    //删除
    response.clearCookie('username');
    //响应
    response.send('cookie 的清除');
});

app.listen(3000, () => {
    console.log('服务已经启动....');
});

```





## 2. session

session 是保存在`服务器端`的一块儿数据 ，保存当前访问用户的相关信息

**session 的作用：**实现会话控制，可以识别用户的身份，快速获取当前用户的相关信息

**session 运行流程：**填写账号和密码校验身份，校验通过后创建session信息 ，然后将`session_id`的值通过响应头返回 给浏览器



**安装：**

```shell
npm i express-session
```

**引入后配置：**

```js
app.use(session({
    name: 'sid', //设置cookie的name，默认值是：connect.sid
    secret: 'atguigu', //参与加密的字符串（又称签名）
    saveUninitialized: false, //是否为每次请求都设置一个cookie用来存储session的id
    resave: true, //是否在每次请求时重新保存session
    store: MongoStore.create({
        mongoUrl: 'mongodb://127.0.0.1:27017/project' //数据库的连接配置
    }),
    cookie: {
        httpOnly: true, // 开启后前端无法通过 JS 操作
        maxAge: 1000 * 300 // 这一条 是控制 sessionID 的过期时间的！！！
    },
}))
```

当中间件配置成功后，即可通过req.session来访问和使用session对象，从而存储用户的关键信息

调用`req.session.destroy()`函数可情况服务器保存的session信息

使用：

```js
const express = require('express');
//1. 安装包 npm i express-session connect-mongo
//2. 引入 express-session connect-mongo
const session = require("express-session");
const MongoStore = require('connect-mongo');
const app = express();
//3. 设置 session 的中间件
app.use(session({
    name: 'sid', //设置返回cookie的name，默认值是：connect.sid
    secret: 'atguigu', //参与加密的字符串（又称签名）
    saveUninitialized: false, //是否为每次请求都设置一个cookie用来存储session的id
    resave: true, //是否在每次请求时重新保存session
    store: MongoStore.create({
        mongoUrl: 'mongodb://127.0.0.1:27017/project' //数据库的连接配置
    }),
    cookie: {
        httpOnly: true, // 开启后前端无法通过 JS 操作
        maxAge: 1000 * 300 // 这一条 是控制 sessionID 的过期时间的！！！
    },
}))
//创建 session
app.get('/login', (req, res) => {
    //设置session
    req.session.username = 'zhangsan';
    req.session.email = 'zhangsan@qq.com'
    res.send('登录成功');
})
//获取 session
app.get('/home', (req, res) => {
    console.log('session的信息');
    console.log(req.session.username);
    if (req.session.username) {
        res.send(`你好 ${req.session.username}`);
    } else {
        res.send('登录 注册');
    }
})
//销毁 session
app.get('/logout', (req, res) => {
    //销毁session
    // res.send('设置session');
    req.session.destroy(() => {
        res.send('成功退出');
    });
});
app.listen(3000, () => {
    console.log('服务已经启动, 端口 ' + 3000 + ' 监听中...')
});
```



## 3. ession 和 cookie 的区别 

cookie 和 session 的区别主要有如下几点：

存在的位置：

- cookie：浏览器端 
- session：服务端

安全性 cookie：

- 是以明文的方式存放在客户端的，安全性相对较低
- session 存放于服务器中，所以安全性`相对`较好

网络传输量：

- cookie 设置内容过多会增大报文体积， 会影响传输效率
- session 数据存储在服务器，只是通过 cookie 传递 id，所以不影响传输效率

存储限制：

- 浏览器限制单个cookie保存的数据不能超过 4K ，且单个域名下的存储数量也有限制
- session 数据存储在服务器中，所以没有这些限制





## 9. token

用户的信息通过Token字符串的形式，保存在客户端浏览器中。服务器通过还原Token字符串的形式来认证用户身份的

JWT通常由三部分组成：**Header**(头部)、**Payload**(有效荷载)、**Signature**(签名)，三者之间用英文逗号分割

**Payload**部分才是真正的用户信息，是加密之后生成的字符串，其他的是安全性相关的部分



**安装：**

```shell
npm i jsonwebtoken express-jwt  # 同时安装生成token与解析token
```

​	其中：

- jsonwebtoken用于生成JWT字符串
- express-jwt用于将JWT字符串解析还原成JSON对象

**导入：**

```js
// 路由.js
const jwt = require('jsonwebtoken');
```



**定义secret秘钥：**

为了保证JWT字符串的安全性，防止被破解，所以需要加密和解密的字符串

```js
const secretKey = '-^-' // 可直接填入

//可创建 config.js文件，并向外共享加密和还原 Token 的 jwtSecretKey 字符串：
module.exports = {
  jwtSecretKey: 'itheima No1. ^_^',
}
```



**生成JWT字符串：**

调用jsonwebtoken包提供 的`sign()`方法，将用户信息加密成JWT字符串，相应给客户端：

```js
// 路由.js
// 参数1：用户的信息对象，参数2：加密的秘钥，参数3：匹配对象，可以配置当前token的有效期
const tokenStr = jwt.sign({ username: userinfo.username }, secretKey, { expiresIn: '100s', algorithm: 'HS256' })
```





**将JWT字符串还原为JSON对象：**

客户端每次在访问那些有权接口的时候，都需要主动通过请求头中的Authorization字段，将Token字符串发动给服务器进行认证

此时，服务器可以通过express-jwt中间件，自动将客户端发送过来的Token解析还原成JSON对象

```js
// app.js
const { expressjwt } = require('express-jwt');
// expressJWT({ secret: secretKey }) 用来解析Token的中间件  这里的path为指定哪些接口不需要访问权限
app.use(expressjwt({ secret: secretKey, algorithms: ["HS256"] }).unless({ path: [/^\/api\//] }))
```



**注意：**配置成功了此中间件之后，就自动的将解析出来的用户信息，挂载到**`req.auth`**属性上，后续使用可调用

```js
// TODO_03：在登录成功之后，调用 jwt.sign() 方法生成 JWT 字符串。并通过 token 属性发送给客户端
res.send(req.auth)
```



**捕获解析jwt失败后产生的错误：**

当使用express-jwt解析Token字符串是，如果客户端发送过来的Token字符串过期或不合法，会产生解析失败的错误，影响项目的正常运行，可以通过express错误中间件解决

```js
app.use((err, req, res, next) => {
  if (err.name === 'UnauthorizedError') {
    return res.send({
      status: 401,
      meg: '无效的token'
    })
  }
   // 捕获身份认证失败的错误
  if (err.name === 'UnauthorizedError') return res.cc('身份认证失败！')
    
  res.send({
    status: 500,
    meg: '未知错误'
  })
})
```



**新方法：**

```js
//导入 jsonwebtokan
const jwt = require('jsonwebtoken');
//创建 token
// jwt.sign(数据, 加密字符串, 配置对象)
let token = jwt.sign({
    username: 'zhangsan'
}, 'atguigu', {
    expiresIn: 60 //单位是 秒
})
//解析 token
jwt.verify(token, 'atguigu', (err, data) => {
    if (err) {
        console.log('校验失败~~');
        return
    }
    console.log(data);
})
```





# 九、跨域

通过ajax请求当前服务器发现会报错，因为get和post接口**不支持跨域请求**

cors是express的一个第三方中间件，可以方便的解决跨域问题

```shell
npm i cors
const cors = require('cors')
app.use(cors()) // 路由之前
```



通过ajax请求案例：

```js
// app.js
const express = require('express')
const bodyParser = require('body-parser')
const cors = require('cors')
const router = require('./router')

const app = express()

app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())

app.use(cors())


app.use(router)

app.listen(3000, () => {
    console.log('服务器启动:http://127.0.0.1:3000');
})
```



```js
// router.js
const express = require('express')

const router = express.Router()

router.get('/get', (req, res) => {
    const query = req.query
    res.send({
        status: 0,
        msg: 'get请求成功',
        data: query
    })
})

router.post('/post', (req, res) => {
    const body = req.body
    res.send({
        status: 0,
        msg: 'post请求成功',
        data: body
    })

})

module.exports = router
```



```html
<script src="https://cdn.staticfile.org/jquery/3.6.0/jquery.min.js"></script>
<body>
    <button id="btnGET">GET</button>
    <button id="btnPOST">POST</button>

    <script>
        $(function () {
            $('#btnGET').on('click', function () {
                $.ajax({
                    type: 'get',
                    url: 'http://127.0.0.1:3000/get',
                    data: { name: 'zs', age: 20 },
                    success: function (data) {
                        console.log(data);
                    }
                })
            })

            $('#btnPOST').on('click', function () {
                $.ajax({
                    type: 'post',
                    url: 'http://127.0.0.1:3000/post',
                    data: { bookname: '西游记', author: '吴承恩' },
                    success: function (data) {
                        console.log(data);
                    }
                })
            })
        })
    </script>
</body>

```





# 六. MongoDB



## 1. 安装

[[MongoDB社区下载](https://www.mongodb.com/try/download/community)]

配置环境变量：在path中填入D:\mongodb\bin

cmd中输入mongod --version

```json
Build Info: {
    "version": "5.0.9",
    "gitVersion": "6f7dae919422dcd7f4892c10ff20cdc721ad00e6",
    "modules": [],
    "allocator": "tcmalloc",
    "environment": {
        "distmod": "windows",
        "distarch": "x86_64",
        "target_arch": "x86_64"
    }
}
```



## 2. 启动和关闭

mongodb默认使用执行mongod命令下所处盼复根目录下的/data/db作为数据存储目录

所以在第一次执行之前先手动新建一个/data/db

**启动：**

```shell
mongod
```

如果想要修改默认的数据存储目录，可以：

```shell
mongod --dbpath=数据存储目录路径
```

**停止：**ctrl+c或者关闭控制台



## 3. 连接数据库

在已经开启服务的情况下再打开一个控制台，输入：

```shell
# 默认连接本机的mongodb服务
mongo
```

退出：

```shell
# 在连接状态下输入
exit
```



## 4. 基本命令

```shell
show dbs # 查看显示所有数据库
db  # 查看当前操作的数据库
use # 切换到指定的数据库(没有会新建)
```



id带引号解决方案

```html
<a href="/delete?id={{$value._id.toString()}}">删除</a>
<a href="/delete?id={{@$value._id}}">删除</a>
var id = req.body.id.replace(/"/g, '')
```



## 5.mongoose 起步

```shell
$ npm install mongoose
```

helloworld：

```js
var mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/test');

// 创建一个模型 等于设计数据库
var Cat = mongoose.model('Cat', { name: String });

// 实例化一个cat
var kitty = new Cat({ name: '猫猫' })

// 持久化保存kitty实例
kitty.save(function (err) {
    if (err) {
        console.log(err)
    }
    console.log('小猫')
})

// db.cats.find() 命令行查看
```



## 6. 设计Schema发布model



```js
var mongoose = require('mongoose')
var Schema = mongoose.Schema;

// 连接数据库
mongoose.connect('mongodb://localhost/test')

// 设计文档结构(表结构)
var userSchema = new Schema({
    username: {
        type: String,
        required: true // 必须有
    },
    password: {
        type: String,
        required: true
    },
    email: {
        type: String
    }
})
// 将文档结构发布为模型
var User = mongoose.model('User', userSchema)
// 参数1：传入一个英文大写名词的单数的字符串表示数据库名称，mongoose会自动将其小写复数化
// 参数2：架构Schema
// 返回值：模型构造函数
```



## 7. 增加数据

```js
var admin = new User({
    username: 'admin',
    password: '123',
    email: 'admin@admin.com'
})

admin.save(function (err, ret) {
    if (err) {
        console.log('存储失败')
    }
    console.log('存储成功');
    console.log(ret);
})
```



## 8. 查询数据

不跟条件即查询所有：

```js
User.find(function (err, data) {
    if (err) {
        console.log('查询失败');
    }
    console.log(data);
})
```

根据条件查询：

```js
User.find({
    username: '张三'
}, function (err, data) {
    if (err) {
        console.log('查询失败');
    }
    console.log(data);
})
```

以上会存放到数组中，下面的方法为查询一个，直接为一个对象：

```js
User.findOne({
    username: '张三'
}, function (err, data) {
    if (err) {
        console.log('查询失败');
    }
    console.log(data);
})
```



## 9. 删除数据



```js
User.remove({
    username: 'admin'
}, function (err) {
    if (err) {
        console.log('删除失败');
    }
    console.log('删除成功');
})
```



## 10.更新数据

根据id查找更改

```js
User.findByIdAndUpdate('62c12d256ce919c3fa87b8ba', {
    password: '666666'
}, function (err, ret) {
    if (err) {
        console.log('修改失败');
    } else {
        console.log('修改成功');
    }
})
```





# 七. 连接mysql



DataType数据类型：int(整数)、varchar(len)(字符串)、tinyint(1)(布尔值)、TEXT(任意长度字符串)

字段特殊标识：PK：主键、NN：不允许为空、UQ：值唯一、AI：值自动增长



如果sql只有一个占位符，函数第二个可以不写[ ]



```shell
npm install --save mysql

const mysql = require('mysql')
```

## 1. 查询数据



SELECT语句用于**从表中查询数据**，执行的结果被存储在**结果表**中(成为**结果集**)

```sql
-- 从FROM指定的表中，查询出所有的数据，*表示所有列
SELECT * FROM 表名称

-- 从FROM指定的表中，查询出指定 列名称(字段) 的数据
SELECT 列名称 FROM 表名称
```

代码示例：

```js
var mysql = require('mysql');

// 1.创建连接
var connection = mysql.createConnection({
    host: 'localhost',
    user: 'root',
    password: '123123',
    database: 'test'
});

// 2.连接数据库
connection.connect();

// 3.执行数据操作
connection.query('SELECT * FROM `users`', function (error, results, fields) {
    if (error) throw error;
    console.log('The solution is: ', results);
});

/* connection.query('INSERT INTO users VALUES(NULL,"admin","123456")', function (error, results, fields) {
    if (error) throw error;
    console.log('The solution is: ', results);
}); */

// 4.关闭连接
connection.end();
```



## 2. 插入数据



**INSERT INTO**语句用于向数据表中**插入新的数据行**

```SQL
-- 语法解读：向指定的表中，插入如下几列的数据，列的值通过values指定
-- 注意：列和值要一一对应，多个列和值之间用英文逗号分割
INSERT INTO table_name (列1,列2,...) VALUES (值1,值2,...)
```

代码示例：

```js
var addSql = 'INSERT INTO students(Id,username,age,sex,hobbise) VALUES(NULL,?,?,?,?)';
var addSqlParams = ['王二', 12, '1', '玩'];

connection.query(addSql, addSqlParams, function (err, result) {
    if (err) {
        return console.log('错误');
    }
    console.log(result);
})
```

新：

```js
const mysql = require('mysql')

const db = mysql.createPool({
    host: '127.0.0.1',
    user: 'root',
    password: '123123',
    database: 'test'
})

const sqlStr = 'INSERT INTO students (username,age,sex,hobbise) VALUES (?,?,?,?)'
const user = { username: 'zs', age: 12, sex: '0', hobbise: '吃饭' }

db.query(sqlStr, [user.username, user.age, user.sex, user.hobbise], (err, result) => {
    if (err) return console.log(err.message)
    if (result.affectedRows == 1) console.log('插入成功');
})
```



**快捷插入数据：**

向表中新增数据时，如果数据对象每个属性和数据表的字段一一对应，则可以通过以下方式插入：

```js
const mysql = require('mysql')

const db = mysql.createPool({
    host: '127.0.0.1',
    user: 'root',
    password: '123123',
    database: 'test'
})

const sqlStr = 'INSERT INTO students set ?'
const user = { username: 'zs', age: 12, sex: '0', hobbise: '吃饭' } // 除了id缺一不可

db.query(sqlStr, user, (err, result) => {
    if (err) return console.log(err.message)
    if (result.affectedRows == 1) console.log('插入成功');
})
```







## 3. 修改数据

UPDATE语句用于修改表中的数据

```sql
-- 用UPDATE指定要更新那个表中的数据
-- 用SET指定列对应的新值
-- 用WHERE指定更新的条件
UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
```



```js
var modSql = 'UPDATE students SET username = ?,age = ?,hobbise=? WHERE Id = ?'; // 根据id
var modSqlParams = ['老三', 18, '测试', 3];
//改
connection.query(modSql, modSqlParams, function (err, result) {
    if (err) {
        console.log('[UPDATE ERROR] - ', err.message);
        return;
    }
    console.log('--------------------------UPDATE----------------------------');
    console.log('UPDATE affectedRows', result.affectedRows);
    console.log('-----------------------------------------------------------------\n\n');
});
```



```js
const mysql = require('mysql')

const db = mysql.createPool({
    host: '127.0.0.1',
    user: 'root',
    password: '123123',
    database: 'test'
})

const sqlStr = 'update users set password=? where id=?'
const user = { id: 1, password: 123123 }

db.query(sqlStr, [user.password, user.id], (err, result) => {
    if (err) return console.log(err.message)
    if (result.affectedRows == 1) console.log('更新成功');
})
```



快捷方式：

向修改数据时，如果数据对象每个属性和数据表的字段一一对应，则可以通过以下方式修改：

```js
const sqlStr = 'update users set ? where id=?'
const user = { id: 1, password: 123123 }

db.query(sqlStr, [user, user.id], (err, result) => {
    if (err) return console.log(err.message)
    if (result.affectedRows == 1) console.log('更新成功');
})
```





## 4. 删除数据



DELETE语句用于删除表中的行

```sql
-- 从指定的表中，根据WHERE条件，删除对应的数据行
DELETE FROM 表名称 WHERE 列名称 = 值
```



```js
var delSql = 'DELETE FROM students WHERE id=6';
//删
connection.query(delSql, function (err, result) {
    if (err) {
        console.log('[DELETE ERROR] - ', err.message);
        return;
    }
    console.log('DELETE affectedRows', result.affectedRows);
});
```

新：

```js
const sqlStr = 'delete from students where id=?'

db.query(sqlStr, 24, (err, result) => {
    if (err) return console.log(err.message)
    if (result.affectedRows === 1) console.log('删除成功');
})
```





**标记删除：**

使用delete语句会删除真实数据，为了保险起见使用**标记删除**的方式

在表中设置类似**status**的**状态字段**，标记这条数据是否被删除

```js
const sqlStr = 'update users set status=? where id=?'

db.query(sqlStr, [1, 1], (err, result) => {
    if (err) return console.log(err.message)
    if (result.affectedRows === 1) console.log('删除成功');
})
```



## 5. 封装函数



```js
// config.js
module.exports = {
    host: 'localhost',
    user: 'root',
    password: '123123',
    database: 'test'
}
```



```js
// mysql.js
var config = require('./config')
var mysql = require('mysql')

module.exports = function (sql, params, callback) {
    //每次使用的时候需要创建链接，数据操作完成之后要关闭连接
    var connection = mysql.createConnection(config);
    connection.connect(function (err) {
        if (err) {
            console.log('数据库链接失败');
            throw err;
        }
        connection.query(sql, params, function (err, results) {
            if (err) {
                console.log('数据操作失败');
                throw err;
            }
            //将查询出来的数据返回给回调函数
            callback(null,results);
            connection.end(function (err) {
                if (err) {
                    console.log('关闭数据库连接失败！');
                    throw err;
                }
            });
        });
    });
}
```





## 6. WHERE、AND、OR



**WHERE子句：**

下面的运算符可在WHERE子句中使用，用来限定选择的标准：=、<、>、<=、>=

| 操作符  | 描述         |
| ------- | ------------ |
| <>      | 不等于       |
| BETWEEN | 在某个范围内 |
| LIKE    | 搜索某种模式 |



**AND和OR：**

AND和OR可在WHERE子句中把两个或多个条件结合起来：

- AND表示必须同时满足多个条件，相当于JS的&&
- OR表示只要满足一个条件即可，相当于JS的||

```sql
SELECT * FROM users WHERE id<10 AND username='admin'
```





## 7. 排序



```
ORDER BY  ` 语句用于根据指定的列队结果集进行排序，并默认按照升序的记录进行排序`ASC
```

`DESC ` 可进行降序排序

```sql
SELECT * FROM students ORDER BY id ASC  -- 升序默认
SELECT * FROM students ORDER BY id DESC -- 降序
```

多重排序：

```sql
SELECT * FROM students ORDER BY id DESC,sex ASC -- 先根据id降序，再根据sex升序
```





## 8. COUNT



COUNT(*)函数用于返回查询结果的总数据条数：

```sql
SELECT COUNT(*) FROM students WHERE sex=0 -- 查询sex=0的数量
```



AS关键字可以将查询出的列名称设置别名：

```sql
SELECT COUNT(*) as nan FROM students WHERE sex=0
SELECT username as un ,hobbise as ho FROM students
```





## 9. 模糊搜索

```sql
SELECT * FROM article WHERE title LIKE '%搜索内容%'
```



```js
let sql = 'SELECT * FROM article WHERE title LIKE ?'

db.query(sql, ['%' + req.query.title + '%'], (err, result) => {
    if (err) return res.send({ status: 404, msg: err.message })
    res.send({ status: 200, msg: '获取列表成功', data: result })
})
```



## 10. 分页搜索

```sql
select * from article limit (第几页-1)*每页个数,每页个数
```



```js
const num = req.query.num// 每页个数
const page = req.query.page//获取第几页

if (!num || !page) return res.send({ status: 400, msg: '字段不完整' })

db.query(`select * from article limit ${(page - 1) * num},${num}`, (err, result) => {
    if (err) return res.send({ status: 404, msg: err.message })
    res.send({ status: 200, msg: '获取文章成功', data: result })
})
```







































# 八. promise

想要让异步按照顺序执行结果的时候，不得不适用嵌套的方法，但是带来的问题是代码结构复杂

为了解决此问题(回调地狱嵌套)所以在ES6中新增了一个API，`Promise`



## 1. 基本语法

```javascript
const { resolve6 } = require('dns');
var fs = require('fs')

// 创建一个promise容器，一旦创建就开始执行里面的代码

var p1 = new Promise(function (resolve, reject) {
    fs.readFile('./files/a.txt', 'utf-8', function (err, data) {
        if (err) {
            // 失败了，承诺容器中的任务失败
            // console.log('失败');
            reject(err) // 将容器的Pending状态变为rejected
        } else {
            // 承诺容器中的任务成功
            // console.log(data);
            resolve(data)// 将容器的Pending状态变为resolved
        }
    })
})

p1.then(function (data) {
    console.log('读取成功了' + data);
}, function (err) {
    console.log('读取失败了' + err);
})
```



## 2. 链式编程

当p1读取成功的时候，当前函数的结果就可以在后面的then中function接收到

当return一个Promise对象的时候，后续的then中的方法的第一个参数会作为p2的resolve

```js
var fs = require('fs')

// 创建一个promise容器，一旦创建就开始执行里面的代码

var p1 = new Promise(function (resolve, reject) {
    fs.readFile('./files/a.txt', 'utf-8', function (err, data) {
        if (err) {
            reject(err) // 将容器的Pending状态变为rejected
        } else {
            resolve(data)// 将容器的Pending状态变为resolved
        }
    })
})

var p2 ,p3......

p1
    .then(function (data) {
        console.log('a读取成功了' + data);
        return p2
    })
    .then(function (data) {
        console.log('b读取成功了' + data);
        return p3
    })
    .then(function (data) {
        console.log('c读取成功了' + data);
    })
// a读取成功了aaa
// b读取成功了bbb
// c读取成功了ccc
```



## 3. 封装

```js
var fs = require('fs')

function preadfile(filePath) {
    return new Promise(function (resolve, reject) {
        fs.readFile(filePath, 'utf-8', function (err, data) {
            if (err) {
                reject(err)
            } else {
                resolve(data)
            }
        })
    })
}

preadfile('./files/a.txt')
    .then(function (data) {
        console.log(data);
        return preadfile('./files/b.txt')
    })
    .then(function (data) {
        console.log(data);
        return preadfile('./files/c.txt')
    })
    .then(function (data) {
        console.log(data);
    })
```



如果then之接受一个err，则为then(null,err()=>{})，简便写法为catch(()=>{})，只接受一个参数

```js
// then捕获数据，catch捕获异常的
.then(data =>{
     console.log(data);
}).catch(err=>{
     console.log(err);
})
```





## 4. 方法



**Promise.resolve()：**

将现有对象转为 Promise 对象，`Promise.resolve()`方法就起到这个作用。

```js
// 上面代码将 jQuery 生成的deferred对象，转为一个新的 Promise 对象。
const jsPromise = Promise.resolve($.ajax('/whatever.json'));
Promise.resolve('foo')
// 等价于
new Promise(resolve => resolve('foo'))
```



**Promise.all()**

`Promise.all()`方法用于将多个 Promise 实例，包装成一个新的 Promise 实例。

此时的then为全部成功才成功



**Promise.race()**

`Promise.race()`方法同样是将多个 Promise 实例，包装成一个新的 Promise 实例。

比如请求一张图片，如果成功了则为实例率先改变状态，状态就会成功，执行成功后的resolve(data)，如果5秒后还没有返回结果，就会触发失败







## 5. 操作mongoDB



```js
User.findOne({ username: '李四' })
    .then(function (user) {
        if (user) {
            console.log('用户已存在')
        } else {
            // 用户不存在，可以注册
            return new User({
                username: '李四', password: '123123', email: "213123@ad.com"
            }).save()
        }
    })
    .then(function (ret) {
    })
```





# 九. npm包



## 1. dayjs格式化时间

```shell
npm install dayjs --save
```



```js
const dayjs = require('dayjs')
const now = dayjs().format('YYYY-MM-DD HH:mm:ss')
```






> 创建日期：2022-11-26
>
> 修改日期：2023-03-11

# 十. node上传文件



## 安装

```shell
 npm i formidable
```



## 引入

```js
const formidable = require('formidable');
```





## 使用

```js
app.post('/post', (req, res) => {
    
    const form = formidable(); // 创建解析对象
    
    form.parse(req, (err, fielads, files) => { // 解析表单信息
        if (err) console.log(err);

        fs.readFile(files.name.filepath, (err, data) => { // 读取目录的文件
            if (err) console.log(err);

            fs.writeFile('./test/' + files.name.originalFilename, data, (err) => { // 将文件写入本地
                if (err) console.log(err);
                
                // 保存成功
                // 获取保存的文件的绝对路径，可能需要将\符号替换
                const src = path.join(__dirname, './test/' + files.name.originalFilename) 

                // 此处可进行数据库操作
                ...
            })
        })
    });
    form.on('end', () => {
        console.log('结束解析');
    });

})

```



## 发送

```html
<form action="/post" method="post" enctype="multipart/form-data">
    <input type="file" name="name">

    <button type="submit">发表</button>
</form>
```









## 配置跨域

```shell
npm i cors
```



```js
// 引入
const cors = require('cors')

// 配置
app.use(cors()) // 路由之前
```