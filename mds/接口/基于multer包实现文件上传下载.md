> 创建时间：2023-3-12
>
> 修改时间：2023-3-12




#


```
node根据multer包实现文件上传与下载
```



# 一. 客户端端请求方式



引入 axios

```html
<script src="https://cdn.bootcdn.net/ajax/libs/axios/0.26.0/axios.min.js"></script>
```



上传标签

```bash
<!-- 单文件上传 -->
<input type="file" id="file">
<!-- 多文件上传 -->
<input type="file" id="files" multiple>
<!-- 最简单的下载方式，download属性告诉浏览器要进行文件的下载 -->
<a href="http://127.0.0.1:3000/download" download="">下载</a>
```



编写js 代码

```js
const file = document.getElementById('file')
const files = document.getElementById('files')
axios.defaults.baseURL = 'http://127.0.0.1:3000'


// 单文件上传
file.addEventListener('change', async (e) => {
    const formDate = new FormData() // // 容器，承载file
    // 键值对，key,value   键为file, 值为文件
    formDate.append("file", e.target.files[0])
    const {data: res} = await axios.post("/file", formDate, {
        // 因为axios默认的Content-Type 为json，所以需要修改
        headers: {
            "Content-Type": "multipart/form-data"
        }
    })
    console.log(res);
})


// 多文件上传
files.addEventListener('change', async (e) => {
    const formDate = new FormData()
    const files = e.target.files
    // 不能用forEach ？类数组？
    for(let i = 0; i < files.length; i++){
        formDate.append('files', files[i])
    }
    const {data: res} = await axios.post("/files", formDate, {
        // 因为axios默认的Content-Type 为json，所以需要修改
        headers: {
            "Content-Type": "multipart/form-data"
        }
    })
    console.log(res);
})
```





# 二. 服务端



### 1. 文件上传



**单文件上传接口**

* 在app.js中配置 cors中间件，解决跨域问题

```js
const cors = require('cors')
app.use(cors())
```

* 在抽取的`routes/index.js`中编写接口, 并在浏览器输入http://localhost:3000/，选择第一个按钮上传文件

```js
var express = require('express')
var router = express.Router()
const multer = require('multer')

// multer配置
const upload = multer({ dest: 'assets/uploads' }) // 此处为文件的存放路径

// 单文件上传接口
router.post('/file', upload.single('file'), (req, res) => {
  console.log(req.file) 
  res.send('ok')
})

module.exports = router
```



服务器端`req.file`控制台打印信息

```js
{
  fieldname: 'file',
  originalname: 'yunyoujun.png',
  encoding: '7bit',
  mimetype: 'image/png',
  destination: 'assets/uploads',
  filename: 'fc6acbf4b3348b82d85b6cf3edc967dd',
  path: 'assets\\uploads\\fc6acbf4b3348b82d85b6cf3edc967dd',
  size: 773524
}
```



在`assets/uploads`目录下生成了文件名为`fc6acbf4b3348b82d85bdd`的文件，vs code显示

在`fc6acbf4b3348b82d85b6cf3edc967dd`加上文件名后缀`.png`就可以正常访问文件了

----



**配置multer实现自动修改文件名**

```js
const storage = multer.diskStorage({
  // 上传文件的目录
  destination: function (req, file, cb) {
    cb(null, 'assets/uploads')
  },
  // 上传文件的名称
  filename: function (req, file, cb) {
    cb(null, file.originalname)
  }
})
// multer 配置
const upload = multer({
  storage
})
```



**多文件上传**

```js
// 多文件上传
// upload.array('formDate中的字段名', 最大上传数量)
router.post('/files', upload.array('files', 4), (req, res) => {
  console.log(req.files)
  res.send('ok')
})
```







### 2. 文件下载

> node 文件下载设置响应头······的content-type 与 Content-Disposition来告诉浏览器，响应结果属于文件下载，准备好接收文件

在app.js中共享`/assets/downloads/`文件夹

```js
app.use(express.static(path.join(__dirname, './assets/downloads/')))
```

**下载接口**

先引入path模块

```js
const path = require('path')
```

编写接口

```js
router.get('/download', (req, res) => {
  const filePath = path.join(__dirname, '../assets/downloads/yunyoujun.png')
  res.download(filePath)
})
```





# 三. 将文件上传到mysql 中



### 1. 文件上传

**安装mysql 模块**

```bash
npm i mysql
```

* 在项目根目录创建`db`文件夹
* 在`db`文件夹中创建`index.js`
* 配置连接池

```js
const mysql = require('mysql')
const db = mysql.createPool({
  host: '192.168.188.100',
  user: 'db-test',
  password: 'admin123',
  database: 'db-test'
})

module.exports = db
```

在`routes/index.js`中导入`db`对象



**修改储存模式**

之前的`multer`配置更改为此，在`router/index.js`下配置

将`multer.diskStorage` 修改为 `multer.memoryStorage`

```js
// 将文件储存在 Buffer 中
const storage = multer.memoryStorage()
const upload = multer({ storage: storage })
```



此时的`req.file`对象

```js
{
  fieldname: 'file',
  originalname: '-6e4e28c3bf13a6ab.gif',
  encoding: '7bit',
  mimetype: 'image/gif',
  buffer: <Buffer 47 49 46 38 39 61 f0 00 f0 00 f7 ff 00 a6 7b 6e 8b 6a 53 29 21 18 ce 39 29 24 16 12 93 71 68 ff e7 ce fe 72 5a ff b5 5a 18 56 2d 9d 53 37 ff
ff ff d0 ... 1520754 more bytes>,
  size: 1520804
}
```



**上传到mysql 中**

```js
// 根据需求是否判断文件名重复
const file = req.file
const data = {
    value: file.buffer
  }
const sql = 'INSERT INTO file SET ?'
db.query(sql, data, (err, results) => {
    if (err) {
        return console.log(err.message)
    }
})
```

sql 语句还可以为`INSERT INTO file (value) VALUES (?) `



`tinymce`富文本编辑器插入图片需要返回一个固定格式的对象

```js
res.send({ location: 'http://127.0.0.1:5000/getfile?n=' + fileName })
```





### 2. 文件下载

```js
router.get('/dw', (req, res) => {
  const sql = 'SELECT * FROM file'
  db.query(sql, (err, results) => {
    if (err) {
      return res.send(err.message)
    }
    res.set({
      'Content-Type': 'image/jpeg',
      'Accept-Ranges': 'bytes',
      'Content-Disposition': 'attachment; filename="filename.jpg"'
    })
    res.send(results[0].value)
  })
})
```









