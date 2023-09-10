> 创建日期：2023-5-12
>
> 修改日期：2023-5-12


#


在vue中使用栅格布局

介绍：在页面中可拖动小模块/组件，并可保存样式，layout数组就是坐标等数据



## 安装

```shell
npm install vue-grid-layout --save
```



vue3报错需安装版本插件

```shell
npm install vue-grid-layout@3.0.0-beta1 --save
```

随后在main.js配置

```js
import VueGridLayout from ‘vue-grid-layout’

const app = createApp(App)
app.use(VueGridLayout)
app.mount('#app')
```



## 基本使用

```vue
<template>
  <div class="container">
    <grid-layout
      :layout.sync="layout"
      :col-num="12"
      :row-height="30"
      :is-draggable="true"
      :is-resizable="false"
      :vertical-compact="true"
      :use-css-transforms="true"
      
    >
      <grid-item
        v-for="item in layout"
        :static="item.static"
        :x="item.x"
        :y="item.y"
        :w="item.w"
        :h="item.h"
        :i="item.i"
        :key="item.i" class="gridItem"
      >
      </grid-item>
    </grid-layout>
  </div>
</template>

<script>
import { GridLayout, GridItem } from "vue-grid-layout";
export default {
  components: {
    GridLayout,
    GridItem,
  },
  data() {
    return {
      layout: [
        { x: 10, y: 4, w: 2, h: 4, i: "11", static: false },
        { x: 0, y: 10, w: 2, h: 5, i: "12", static: false },
        { x: 2, y: 10, w: 2, h: 5, i: "13", static: false },
        { x: 4, y: 8, w: 2, h: 4, i: "14", static: false },
        { x: 6, y: 8, w: 2, h: 4, i: "15", static: false },
        { x: 8, y: 10, w: 2, h: 5, i: "16", static: false },
        { x: 10, y: 4, w: 2, h: 2, i: "17", static: false },
        { x: 0, y: 9, w: 2, h: 3, i: "18", static: false },
        { x: 2, y: 6, w: 2, h: 2, i: "19", static: false },
      ],
    };
  },
  methods: {},
};
</script>

<style>
.layout{
  touch-action: auto;
}
.container .vue-grid-item.vue-grid-placeholder {
  background: green;
}
.vue-grid-layout {
  background: #eee;
}
.vue-grid-item:not(.vue-grid-placeholder) {
  background: #ccc;
  border: 1px solid black;
}
.vue-grid-item .resizing {
  opacity: 0.9;
}
.vue-grid-item .static {
  background: #cce;
}
.vue-grid-item .text {
  font-size: 24px;
  text-align: center;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
  height: 100%;
  width: 100%;
}
.vue-grid-item .no-drag {
  height: 100%;
  width: 100%;
}
.vue-grid-item .minMax {
  font-size: 12px;
}
.vue-grid-item .add {
  cursor: pointer;
}
.gridItem {
  touch-action: none
}
</style>

```



## 动态添加/删除元素

动态添加元素就是往数组对象中 push 新的item数据项：

```javascript
 add() {
      this.layout.push({
        x: 1,
        y: 2, // puts it at the bottom
        w: 1,
        h: 1,
        i: this.layout.length + 1,
      });
},
```



```js
dele(i) {
      this.layout.splice(
        this.layout.findIndex((item) => item.i === i),
        1
      );
},
```





## 更多

官网介绍只能重复生成格式相同的组件拖动，且内部不能放置多个组件，比如生成不同大小，不同格式的组件拖动，经过作者研究，想出了一个临时办法



在src下新建config/config文件

```vue
<template>
 <Image v-if="props.info.i == 12"  :info="props.info"/>
 <SmallTag v-else :info="props.info"/>
 <SmallTag :info="props.info"/>
</template>

<script setup>
import SmallTag from "../components/SmallTag.vue";
import Image from "../components/Image.vue";
import Calendar from "../components/Calendar.vue";

const props = defineProps(["info"]);

</script>

<style lang="less" scoped></style>
```




页面引入组件后在布局中只填入一行内容：info为传单个layout的数据

```html
<div><Config :info="item" /></div> 
```




**详解：**将每个layout的数据传入config文件，config文件通过props收到单个的数据后根据i属性判断此条数据，随后根据判断结果渲染不同的组件，随后又会进入下一轮的渲染，达到实现不同大小不同组件的效果

**注意：**layout数据中的i为类似id属性，为字符串且不能重复，layout数据除了基本必备的几个属性之外可以插入其他属性保存数据











> 更加详细参考：
>
> [vue-grid-layout中文网](https://jbaysolutions.github.io/vue-grid-layout/zh/guide/)，
>
> [稀土掘金](https://juejin.cn/post/7200194519986372663#heading-14)



更多组件：[vue.draggable中文网](https://www.itxst.com/vue-draggable/tutorial.html)















