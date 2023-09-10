> 创建日期：2023-02
>
> 修改日期：2023-03-11


#


# 在vue项目中使用tinymce



TinyMCE是一个功能强大且灵活的富文本编辑器，可以嵌入到任意Web应用中使用。



在页面需要编辑文本，文章编辑发布等场景应用广泛，这里简单介绍在vue中简单快速使用

具体可参考中文网：

> http://tinymce.ax-z.cn/general/basic-setup.php



具体使用，首先在vue中安装tinymce

```shell
npm install tinymce -S
```



随后安装vue专属的tinymce

```shell
npm install @tinymce/tinymce-vue

vue2需要安装低版本，@符号后面为版本号
npm install @tinymce/tinymce-vue@3.0.1 -S 
```



在官网将包下载解压到public下

> https://www.tiny.cloud/get-tiny/self-hosted/



在官网下载语言包放入到tinymce/langs下

> https://www.tiny.cloud/get-tiny/language-packages/



随后在index.html文件中引入js文件

```html
<script src="<%= BASE_URL %>/tinymce/tinymce.min.js"></script>
```



最后新建组件，按以下代码执行即可

```vue
<template>
  <div id="sample">
    <Editor :init="init" />
  </div>
</template>

<script>
import Editor from "@tinymce/tinymce-vue";
export default {
  components: { Editor },
  data() {
    return {
      init: {
        plugins: "lists link image table code   help wordcount",
        language: "zh-Hans",
        resize: false,   
        branding: false
      },
    };
  },
};
</script>
```



页面出现类似下图样式即配置成功

![image-20230311110628755](https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20230311110628755.png)



获取编辑器内容
```vue
console.log(tinyMCE.activeEditor.getContent());
```

获取不带HTML标记的纯文本内容
```vue
var activeEditor = tinymce.activeEditor;
var editBody = activeEditor.getBody();
activeEditor.selection.select(editBody);
var text = activeEditor.selection.getContent({ format: "text" });
console.log(text);
```



init为编辑器的所有配置，如改变编辑器外观，设置按钮等操作，具体可参考官网：

> https://www.tiny.cloud/docs/



中文网：

> http://tinymce.ax-z.cn/

