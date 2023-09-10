> 创建：2023-9-6

cdn 是什么这里就不说明了，详细可以自行搜索，市面上有很多大厂提供付费服务，也有免费的。这里使用阿里云

没使用过的用户可以免费试用，有中国内地下行流量 50GB，12 个月有限期

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230906150456427.png" alt="image-20230906150456427" style="zoom: 50%;" />

这里可以参考官方使用教程，这里也简单说明操作步骤：

1. 首先需要在 github 中创建仓库并设置 github pages，并生成一个链接：

![image-20230906151603917](https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230906151603917.png)

2. 在`全站加速dcdn`控制台选择`域名管理`，点击`添加域名`

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230906151155446.png" alt="image-20230906151155446" style="zoom:50%;" />

3. 下面`新增源站信息`，格式必须这样否则会报源站信息错误

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230906152119756.png" alt="image-20230906152119756" style="zoom:50%;" />

4. 确认后显示添加成功，此时能看到添加的域名，`复制CNAME记录`鼠标放上`等待配置`打开配置向导，打开配置 dns

![image-20230906152538383](https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230906152538383.png)

5. 在域名的解析记录添加上面填的自己想要的域名

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230906152829294.png" alt="image-20230906152829294" style="zoom:50%;" />

6. 完成操作和返回页面刷新一下，并按上面的图的位置点击`点击查询`，正确配置和会显示状态为正常运行（可能需要等几分钟），这里就完成了

![image-20230906153303233](https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230906153303233.png)

7. 返回 github pages,将自己的域名设置为自定义域名，然后通过自己的域名访问网站如成功显示，那么大功告成！

通过站长工具实测：配置前延迟大概在 200ms，配置后在 40ms 左右
