> 创建日期：2022
>
> 修改日期：2023-03-11


```
统一域名已隐藏，仅供开发测试研究用
```



#

# 首页热门

请求地址：http:///v4/homepage/vertical?limit=30&adult=false&did=&first=1&order=hot

```json
{
  "msg": "success",
  "res": {
    "vertical": [
      {
        "preview": "http://img5.adesk.com/624e34b8e7bce73e9353c0ac?sign=320e4da8002574ffceb0af6c5551aa8a&t=63311e07",
        "thumb": "http://img5.adesk.com/624e34b8e7bce73e9353c0ac?imageMogr2/thumbnail/!350x540r/gravity/Center/crop/350x540&sign=320e4da8002574ffceb0af6c5551aa8a&t=63311e07",
        "img": "http://img5.adesk.com/624e34b8e7bce73e9353c0ac?imageMogr2/thumbnail/!1080x1920r/gravity/Center/crop/1080x1920&sign=320e4da8002574ffceb0af6c5551aa8a&t=63311e07",
        "views": 0,
        "cid": ["4e4d610cdf714d2966000003"],
        "rule": "&imageMogr2/thumbnail/!$<Width>x$<Height>r/gravity/Center/crop/$<Width>x$<Height>",
        "ncos": 68,
        "rank": 348714,
        "source_type": "vertical",
        "tag": [],
        "url": [],
        "wp": "http://img5.adesk.com/624e34b8e7bce73e9353c0ac?sign=320e4da8002574ffceb0af6c5551aa8a&t=63311e07",
        "xr": false,
        "cr": false,
        "favs": 1018,
        "atime": 1657807506,
        "id": "624e34b8e7bce73e9353c0ac",
        "store": "qiniu",
        "desc": ""
      }
    ],
    "alert": {
      "msg": ""
    }
  },
  "code": 0
}

```





# 首页加载

请求地址：https:///v4/homepage/vertical?limit=2&skip=0&adult=false&did=&first=0&order=hot

请求方法：get

参数：

| 参数名 | 参数说明         | 备注 |
| ------ | ---------------- | ---- |
| limit  | 每次请求限制数量 |      |
| skip   | 从第几个开始请求 |      |





# 竖屏分类



请求地址：http:///v1/vertical/category?adult=false&first=1

请求方法：get



单个模块-使用分类里的id：http:///v1/vertical/category/4e4d610cdf714d2966000003/vertical?limit=30&skip=30&adult=false&first=0&order=new





# 横屏首页

请求地址：http:///v3/homepage?limit=30&skip=30&adult=false&did=&first=0&order=hot





# 横屏分类

请求地址：http:///v1/wallpaper/category?adult=false&first=1



单个模块-使用分类里的id：https:///v1/wallpaper/category/4e4d610cdf714d2966000000/wallpaper?limit=30&skip=0&adult=false&first=0&order=new

携带参数：

| 请求头  | 参数名          | 参数值            |
| ------- | --------------- | ----------------- |
| Headers | User-Agent      | picasso,289,adesk |
|         | Accept-Encoding | gzip              |



