> 创建日期：2020
>
> 修改日期：2023-3-11


#

# 一. php

## 1. 基本语法

php的语句写在`<?php ?>`的标签中

用点拼接字符串

使用变量也要加 **$**

写在php标签之外的代码会原封不动的执行

引入文件：include

```php
utf-8: header('content-type:text/html;charset=utf-8');	//设置中文编码
```

```php
echo '输出';	//输出语句
```

一个php文件可以写多个php标签

```php+HTML
<!-- for循环的半边 -->
<?php for ($i=0; $i < count($heroArr); $i++) { ?>
    <h2><?php echo $heroArr[$i]['champion_name']?>感觉自己萌萌哒</h2>
    <a href="">你儿豁</a>
<?php } ?>
```



## 2. **变量声明与使用**

```php
$name = '吴京';
echo $name;
```

```php
echo '<br>';	//打印标签会执行代码
```

## 3. **分支语句**

```php
//	if语句
$if = false;
if ($if==false) {
   echo '萌妹子';
}else{
   echo '糙汉子';
}
```

```php
//	switch case语句
$day = '星期er';
switch($day){
   case '星期一':
       echo '上班';
   break;
   default:
       echo '放假';
}
```

## 4. **循环语句**

```php
// for循环
for($i = 1;$i<=10;$i++){
        echo '感觉自己萌萌哒'.$i; //用点拼接字符串
        echo '<br>';
}
```

```php
// while循环
$w = 1;
while($w<=50){
   echo '哈哈'.$w;
   echo '<br>';
   $w++;
}
```

## 5. **数组**

```php
$foodarr = array('土豆','薯片','炸鸡');
echo $foodarr[2];	// 打印单个值
print_r($foodarr);	// 打印整个数组
```

```php
count($foodarr); // 获取数组的长度
for ($i=0; $i < count($foodarr); $i++) { 	// 遍历数组
    echo '<br>';
    echo $foodarr[$i];
}
```

## 6. **关系型数组**

```php
$person = array('name'=>'无e凡','ni'=>'加拿大电鳗');	//键值对的形式
echo $person['name'];	//用键取值
print_r($person);	//打印数组
```

```php
// 遍历数组
foreach ($person as $key => $value) {
   echo $key.'------'.$value.'<br>';
}
```

**二维数组**

```php
$stararr = array(
        array('name'=>'劲夫','position'=>'lol','Occupation'=>'拳皇'),
        array('name'=>'无e凡','position'=>'lol','Occupation'=>'射手'),
        array('name'=>'耐格包','position'=>'lol','Occupation'=>'肉的一批')
);
```

```php
 echo $stararr[0]['name'];	// 取索引为0的 键为name的值
```

```php
for($i=0;$i<count($stararr);$i++){	// 遍历
        echo '<h2><span>'.$stararr[$i]['name'].'</span>在'.$stararr[$i]['position'].'里的位				置是'.$stararr[$i]['Occupation'].'</h2>';
        echo '<br>';
}
```

# 二. 数据提交

**form表单发送数据：**

1.  action指定提交的 url
2.  提交的方式 method 不设置默认是get
3.  表单元素 需要提交的数据使用name属性进行标记 尽可能起的有意义

## 1. get提交

```html
<form action="./getData.php" method="GET">
     <input type="text" name="foodname" placeholder="请输入你喜欢的食物">
     <input type="submit">
</form>
```

```php+HTML
<!-- 数据接收页面使用html ！框架在标签里面使用设置的 name 属性取值 -->
<h2>你喜欢用<?php echo $_GET['type'] ?>方式吃<?php echo $_GET['food'] ?></h2>
```

```php+HTML
<a href="lol_detail.php?name='.$heroArr[$i]['champion_name'].'">详情</a>	
<!-- 标签里面直接拼接 -->
```

get提交数据的方式是在url里面

多条数据的格式 xxx.php?key1=value1&key2=value2

get方式提交数据**总结**

1. 数据是拼接在url中，安全性不好，有些浏览器会限制数据长度
2. 测试方便

## 2. post提交

**必须设置method**

1. 提交的数据不在url中，安全性好一些
2. post提交数据 没有长度限制，浏览器端只要你想，随意添加，服务器可以选择是否接受这么多数据
3. 如果要上传文件，必须使用post

```php+HTML
<form action="./postData.php" method="POST">
        <input type="text" name="food" placeholder="你喜欢的食物">
        <input type="text" name="type" placeholder="做法">
        <input type="submit">
</form>
```

**post上传文件必须设置属性**：

```php
enctype="multipart/form-data"
```

post提交文件会产生一个临时文件，而php执行结束后此文件会销毁，如果想要拿到这个文件就要使用以下函数

如果要严谨一些 还需要添加一些判断

```php
move_uploaded_file(file,newloc);
// 参数1 移动的文件
// 参数2 移动到那里去
sleeps(5)
```

# 三. ajax

## 1. 请求报文&响应报文

![Snipaste_2020-10-22_21-05-43](C:\Users\YRCX\Desktop\Snipaste_2020-10-22_21-05-43.png)

## 2. 异步对象的使用

```php+HTML
<input type="button" value="发送请求报文">

    <script>
        //绑定点击事件
        var btu = document.querySelector('input');
        btu.onclick = function () {
            //创建异步对象
            var xhr = new XMLHttpRequest();
            //请求行
            xhr.open('get','xxx.php');
            //请求头 参数1 键名 参数2 值
            xhr.setRequestHeader('heima','ashucoashiosa');
            //请求主体 发送
            xhr.send(null);
        }
    </script>
```

## 3. ajax发送get请求

```html
<h2>点击的时候发送请求报文---不刷新页面</h2>
    <input type="button" value="get请求">

    <script>
        document.querySelector('input').onclick = function(){
            // 1.创建对象
            var xhr = new XMLHttpRequest();

            // 2.设置请求行(get请求数据写在url后面)
            xhr.open('get','getData.php?name=rose&a=swim');

            // 3.设置请求头(get请求可以省略,post不发送数据也可以省略
            // 3.5 注册回调函数
            xhr.onload = function(){
                //获取数据
                console.log(xhr.responseText);
                //修改页面元素
                document.querySelector('h2').innerHTML = xhr.responseText;
            }
            // 4. 请求主体发送(get请求为空，或者写null，post请求数据写在这里,如果没有数据,直接为空或者写null
            xhr.send(null);
        }

    </script>
```

可以在回调函数中修改dom元素展示返回的数据

返回的数据使用**xhr.responseText**

个体发请求可以直接在url后面拼接：

```javascript
xhr.open('get', 'checkName.php?name='+this.value);
```

```php
$name = $_GET['name']; //php页面接收在url后面拼接的键对应的值
//判断是否在数组中存在
// 参数1 查什么
// 参数2 去哪查
$result = in_array($name,$nameArr);
if($result){
    echo '存在'; //返回数据，在回调函数接收的数据来自这里
}else{
    echo '可以';
}
```

## 4. ajax发送post请求

发送post请求必须设置请求头，具体代码如下：

```javascript
xhr.setRequestHeader('Content-type','application/x-www-form-urlencoded');
```

post请求发送数据，写在send中		

```javascript
xhr.send('name=tom&friend=jerry');	// key1=value1&key2=value2
```

## 5. 案例：图灵机器人

```javascript
//需导入jq包
<script>
    $(function () {
        $('.sendButton').click(function () {
            //创建自己的聊天框
            var $cloneSelf = $('.self').first().clone(); //克隆写好的
            //添加到容器中
            $('.message').append($cloneSelf);
            $cloneSelf.show();
            //获取输入框的内容，设置给克隆的元素内部的 p标签
            $cloneSelf.find('p').html($('.inputBox').val());


            var xhr = new XMLHttpRequest();
            xhr.open('post', 'https://api.ownthink.com/bot');
            xhr.setRequestHeader('Content-type','application/x-www-form-urlencoded');
            xhr.onload = function () {
                console.log(xhr.responseText);
                var $cloneRobot = $('.robot').first().clone();
                $cloneRobot.appendTo('.message');
                $cloneRobot.find('p').html(xhr.responseText);
            }
            xhr.send('appid=xiaosi&userid=user&spoken='+$('.inputBox').val());
        })
    })
</script>
```

## 6.回调函数照顾兼容性

```javascript
 xhr.onreadystatechange = function () { //状态改变就触发   兼容性更好
            console.log("我触发了");
            console.log(xhr.readyState); //会调用很多次
            console.log(xhr.responseText);

            //如果页面不存在，还是会进入if里面，所以需要进行判断
            if(xhr.readyState==4&&xhr.status==200){
                //只有等于4的时候执行  4代表操作完成
            }
        }
```

xhr.readyState会返回四个代码，分别对应不同的意思

| 值   | 状态             | 描述                                           |
| ---- | ---------------- | ---------------------------------------------- |
| 0    | UNSENT           | 代理被创建，但尚未调用open()方法               |
| 1    | OPENED           | open()方法已经被调用                           |
| 2    | HEADER_SRECEIVED | send()方法已经被调用，并且头部和状态已经可获得 |
| 3    | LOADING          | 下载中；responseTest属性已经包含部分数据       |
| 4    | DONE             | 下载操作已完成                                 |

只有当等于4的时候才算完成

当页面不存在的时候还是会执行回调函数里面的if(上面的代码)，所以需要加判断，只有当页面存在的时候才执行

## 7. 多个数据返回的解决

当请求发出去之后，可能会同时返回多个数据，而服务器会将这些数据揉成一团，此时可以使用切割字符串的方法解决

```php
//返回图片路径
echo $someOne['icon'];
//额外返回用来切割的内容
echo '|||';
//返回信息
echo $someOne['info'];

// 返回为：  图片地址|||代表作：雅俗共赏
```

此时返回就是数组。将数组的索引上的值进行页面渲染

```javascript
var re = xhr.responseText.split('|||');
$('img').attr('src', re[0]);
$('p').html(re[1]);
```

## 8. 获取XML文件

xml是一种文件格式

要想接收，必须设置编码格式：

```php
header('content-type:text/xml;charset=utf-8');
```

```php
// =>哪个分类中 文件分类中找
// 参数1 文件的路径名
$xmlString = file_get_contents('data/person.xml');	//读取xml 返回
```

在回调函数里面，接收xml返回的数据，要使用responseXM

```javascript
//如果返回的是xml，用responseXML接收
console.log(xhr.responseXML);
```

此方法返回的是xml文件里面一样的格式的数据，如果想要解析，则需要通过一些方法执行

```javascript
//解析
var name = xhr.responseXML.querySelector('name').innerHTML;
var age = xhr.responseXML.querySelector('age').innerHTML;
var sing = xhr.responseXML.querySelector('sing').innerHTML;
 document.querySelector('h3').innerHTML = name + "--" + age + "--" + sing; //渲染到页面
```

xml的缺点：

1. 传输的数据量大
2. 解析略微有点复杂

## 9. JSON

设置返回的是JSON：header('content-type:application/json;charset=utf-8');

JSON的简单介绍：

1. JSON是一种数据的格式
2. JSON跟编程语言没有关系
3. JSON的载体是字符串
4. 基本上所有的编程语言都提供了对应的方法来解析JSON
5. JSON格式的字符串转化完毕之后，会变成  数组/对象

**要使用，必须转换为对应的 数组/对象**

**JSON的写法--用来表示对象**

​	对象使用{}

​	属性名属性值必须使用""包裹，如果属性值是数值 可以不使用双引号

```javascript
var jsonObj = '{"name":"张三","age":18}';
console.log(jsonObj);	//输出字符串
var jobj = JSON.parse(jsonObj);	//转换
console.log(jobj);		//输出对象
```

**JSON的写法--用来表示数组**

```javascript
var jArr = '["苹果","香蕉","梨"]';
var arr = JSON.parse(jArr);
console.log(jArr);
console.log(arr);
```

**JSON的写法--对象数组**

```javascript
var objArr = '{"name":"李四","age":"19","friends":["社会王","吊毛"]}';
var objArrjiexi = JSON.parse(objArr);
console.log(objArrjiexi);
console.log(objArrjiexi.friends[0]);	//取数组的值
```

# 四. 工具函数封装

## 1. 封装get请求

```js
/**
 * ajax工具函数-get
 * @param {*} url 
 * @param {*} data(key1=value1&key2=value2) 
 * @param {*} success 
 */
function get(url, data, success) {
    var xhr = new XMLHttpRequest();
    if (data) {
        url += '?';
        url += data;
    }
    xhr.open('get', url);
    xhr.onreadystatechange = function () {
        if (xhr.readyState == 4 && xhr.status == 200) {
            success(xhr.responseText);
        }
    }
    xhr.send(null);
}
```

## 2. 封装post请求

```js
/**
 * ajax工具函数-post
 * @param {*} url 
 * @param {*} data (key1=value1&key2=value2) 
 * @param {*} success 
 */
function post(url, data, success) {
    var xhr = new XMLHttpRequest();
    xhr.open('post', url);
    if (data) {
        xhr.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
    }
    xhr.onreadystatechange = function () {
        if (xhr.readyState == 4 && xhr.status == 200) {
            console.log(xhr.responseText);
            success(xhr.responseText);
        }
    }
    xhr.send(data);
}
```

## 3. 自选类型

```js
/**
 * 参数越来越多之后 用户如果要传递参数 必须遵循
 * @param {*} url 
 * @param {*} type 
 * @param {*} data 
 * @param {*} success 
 */
function ajax_test(url, type, data, success) {
    var xhr = new XMLHttpRequest();
    // 如果是get 并且有数据
    if (type == 'get' && data) {
        url += '?';
        url += data;
        data = null; // 这样最后直接send data即可 
    }
    xhr.open(type, url);
    // post请求 并且有数据
    if (type == 'post' && data) {
        xhr.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
    }
    xhr.onreadystatechange = function () {
        if (xhr.readyState == 4 && xhr.status == 200) {
            success(xhr.responseText);
        }
    }
    xhr.send(data);
}
```

## 4. 对象请求方式

```js
// 只传递一个参数
// 用户传入的是 对象
/*
  键名
    url
    type
    data
    success
  用户不需要记忆 参数的顺序 只需要记忆 参数的属性名即可
  大部分的框架 都是这么做的
*/
function ajax(option) {
    var xhr = new XMLHttpRequest();
    // 如果是get 并且有数据
    if (option.type == 'get' && option.data) {
        option.url += '?';
        option.url += option.data;
        option.data = null; // 这样最后直接send data即可 
    }
    xhr.open(option.type, option.url);
    // post请求 并且有数据
    if (option.type == 'post' && option.data) {
        xhr.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
    }
    xhr.onreadystatechange = function () {
        if (xhr.readyState == 4 && xhr.status == 200) {
            // option.success(xhr.responseText);
            // console.log(xhr.getResponseHeader('Content-Type'));
            var type = xhr.getResponseHeader('Content-Type');
            // 是否为json
            if (type.indexOf('json') != -1) {
                option.success(JSON.parse(xhr.responseText));
            }
            // 是否为xml
            else if (type.indexOf('xml') != -1) {
                option.success(xhr.responseXML);
            }
            // 普通字符串
            else {
                option.success(xhr.responseText);
            }
        }
    }
    xhr.send(option.data);
}
```

**总结：**封装的目的，让我们把精力集中在逻辑页面的交互效果，基础的部分不用每次都来一遍。

封装的步骤：固定的部分 抽取，不固定的部分 作为参数

参数很多==>使用对象 来优化

封装的好坏：

1.    功能能否正常执行
2.    代码的简洁程度(可读性)
3.    考虑的问题是否足够多,兼容性问题,异常处理

