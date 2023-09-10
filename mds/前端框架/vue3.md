> 创建日期：2022
>
> 修改日期：2023-9-9



# 一、创建工程


## 1.使用 vue-cli 创建

官方文档：https://cli.vuejs.org/zh/

```shell
## 查看@vue/cli版本，确保@vue/cli版本在4.5.0以上
vue --version
## 安装或者升级你的@vue/cli
npm install -g @vue/cli
## 创建
vue create vue_test
## 启动
cd vue_test
npm run serve
```



## 2.使用 vite 创建

vite官网：https://cn.vitejs.dev/

- 什么是vite？—— 下一代的前端工具链。
- 优势如下：
  - 开发环境中，无需打包操作，可快速的冷启动。
  - 轻量快速的热重载（HMR）。
  - 真正的按需编译，不再等待整个应用编译完成。
- 传统构建 与 vite构建对比图



<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20221120093614569.png" alt="image-20221120093614569" style="zoom: 67%;" />



```shell
## 创建工程
pnpm create vite
## 进入工程目录
cd <project-name>
## 安装依赖
pnpm install
## 运行
pnpm run dev
```





# 二、常用 Composition API

官方文档: https://v3.cn.vuejs.org/guide/composition-api-introduction.html



## 1.拉开序幕的setup

1. 理解：Vue3.0中一个新的配置项，值为一个函数。
2. setup是所有<strong style="color:#DD5145">Composition API（组合API）</strong><i style="color:gray;font-weight:bold">“ 表演的舞台 ”</i>。
3. 组件中所用到的：数据、方法等等，均要配置在setup中。
4. setup函数的两种返回值：
   1. 若返回一个对象，则对象中的属性、方法, 在模板中均可以直接使用。（重点关注！）
   2. <span style="color:#aad">若返回一个渲染函数：则可以自定义渲染内容。（了解）</span>

```vue
<template>
  <h1>信息</h1>
  <h2>姓名:{{ name }}</h2>
  <h2>年龄:{{ age }}</h2>
  <button @click="sayHello">说活</button>
</template>

<script>
import { h } from "vue";
export default {
  name: "App",
  setup() {
    // 数据
    let name = "张三";
    let age = 18;

    // 方法
    function sayHello() {
      alert(`我是${name}，我${age}岁了，你好`);
    }

    // 返回一个对象
    return {
      // 模板中直接使用
      name,
      age,
      sayHello,
    };

    // 返回一个渲染函数 不常用
    return () => h("h1", "哈哈哈");
  },
};
</script>
```

注意点：

1. 尽量不要与Vue2.x配置混用
   - Vue2.x配置（data、methos、computed...）中<strong style="color:#DD5145">可以访问到</strong>setup中的属性、方法。
   - 但在setup中<strong style="color:#DD5145">不能访问到</strong>Vue2.x配置（data、methos、computed...）。
   - 如果有重名, setup优先。
2. setup不能是一个async函数，因为返回值不再是return的对象, 而是promise, 模板看不到return对象中的属性。（后期也可以返回一个Promise实例，但需要Suspense和异步组件的配合）





##  2.ref函数

- 作用: 定义一个响应式的数据
- 语法: ```const xxx = ref(initValue)``` 
  - 创建一个包含响应式数据的<strong style="color:#DD5145">引用对象（reference对象，简称ref对象）</strong>。
  - JS中操作数据： ```xxx.value```
  - 模板中读取数据: 不需要.value，直接：```<div>{{xxx}}</div>```
- 备注：
  - 接收的数据可以是：基本类型、也可以是对象类型。
  - 基本类型的数据：响应式依然是靠``Object.defineProperty()``的```get```与```set```完成的。
  - 对象类型的数据：内部 <i style="color:gray;font-weight:bold">“ 求助 ”</i> 了Vue3.0中的一个新函数—— ```reactive```函数。



```vue
<template>
  <h2>姓名:{{ name }}</h2>
  <h2>年龄:{{ age }}</h2> <!-- 不用.value -->

  <h3>工作种类:{{ job.type }}</h3>
  <h3>工作薪水:{{ job.salary }}</h3>
  <button @click="changeInfo()">修改信息</button>
</template>

<script>
import { ref } from "vue";
export default {
  name: "App",
  setup() {
    let name = ref("张三");
    let age = ref(18);
    let job = ref({type: "前端工程师", salary: "30k"});

    function changeInfo() {
      job.value.type = "ui设计";  // 不用再多加.value
      job.value.salary = "40k";
    }

    return {name,age,changeInfo,job};
  },
};
</script>
```





## 3.reactive函数

- 作用: 定义一个<strong style="color:#DD5145">对象类型</strong>的响应式数据（基本类型不要用它，要用```ref```函数）
- 语法：```const 代理对象= reactive(源对象)```接收一个对象（或数组），返回一个<strong style="color:#DD5145">代理对象（Proxy的实例对象，简称proxy对象）</strong>
- reactive定义的响应式数据是“深层次的”。
- 内部基于 ES6 的 Proxy 实现，通过代理对象操作源对象内部数据进行操作。



```js
// ref函数
RefImpl {__v_isShallow: false, dep: Set(1), __v_isRef: true, _rawValue: {…}, _value: Proxy}


// reactive函数 同上，不同多写.value 
Proxy {type: '前端工程师', salary: '30k'}
```



```js
// 简略写法--一个对象包含数据
let person = reactive({
    name: "张三",
    age: 18,
    job: {
        type: "前端工程师",
        salary: "30k",
    },
    hobby: ["抽烟", "喝酒", "烫头"],
});

function changeInfo() {
    person.job.type = "ui设计";
    person.job.salary = "40k";
}
return {
    person,
    changeInfo,
};
```





## 4.Vue3.0中的响应式原理

### 4.1 vue2.x的响应式

- 实现原理：

  - 对象类型：通过```Object.defineProperty()```对属性的读取、修改进行拦截（数据劫持）。

  - 数组类型：通过重写更新数组的一系列方法来实现拦截。（对数组的变更方法进行了包裹）。

    ```js
    Object.defineProperty(data, 'count', {
        get () {}, 
        set () {}
    })
    ```

- 存在问题：

  - 新增属性、删除属性, 界面不会更新。
  - 直接通过下标修改数组, 界面不会自动更新。

### 4.2 Vue3.0的响应式

- 实现原理: 
  - 通过Proxy（代理）:  拦截对象中任意属性的变化, 包括：属性值的读写、属性的添加、属性的删除等。
  - 通过Reflect（反射）:  对源对象的属性进行操作。
  - MDN文档中描述的Proxy与Reflect：
    - Proxy：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy

    - Reflect：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect



```js
// 原操作方式
let person = { name: '张三',age: 19 }
const p = new Proxy(person, {
    // 读取某个属性调用
    get(target, propName) {
        console.log(`读取了${propName}`);
        return target[propName]
    },
    // 修改某个属性或追加某个属性调用
    set(target, propName, value) {
        console.log(`修改了${propName}属性，更新页面了`);
        target[propName] = value
    },
    // 多出来的 -- 删除某个属性时调用
    deleteProperty(target, propName) {
        console.log(`删除了${propName}属性，更新页面了`);
        return delete target[propName]
    }
})
```

```js
// Reflect操作方式
new Proxy(data, {
	// 拦截读取属性值
    get (target, prop) {
    	return Reflect.get(target, prop)
    },
    // 拦截设置属性值或添加新属性
    set (target, prop, value) {
    	return Reflect.set(target, prop, value)
    },
    // 拦截删除属性
    deleteProperty (target, prop) {
    	return Reflect.deleteProperty(target, prop)
    }
})

proxy.name = 'tom'   
```





## 5.reactive对比ref

-  从定义数据角度对比：
   -  ref用来定义：<strong style="color:#DD5145">基本类型数据</strong>。
   -  reactive用来定义：<strong style="color:#DD5145">对象（或数组）类型数据</strong>。
   -  备注：ref也可以用来定义<strong style="color:#DD5145">对象（或数组）类型数据</strong>, 它内部会自动通过```reactive```转为<strong style="color:#DD5145">代理对象</strong>。
-  从原理角度对比：
   -  ref通过``Object.defineProperty()``的```get```与```set```来实现响应式（数据劫持）。
   -  reactive通过使用<strong style="color:#DD5145">Proxy</strong>来实现响应式（数据劫持）, 并通过<strong style="color:#DD5145">Reflect</strong>操作<strong style="color:orange">源对象</strong>内部的数据。
-  从使用角度对比：
   -  ref定义的数据：操作数据<strong style="color:#DD5145">需要</strong>```.value```，读取数据时模板中直接读取<strong style="color:#DD5145">不需要</strong>```.value```。
   -  reactive定义的数据：操作数据与读取数据：<strong style="color:#DD5145">均不需要</strong>```.value```。





## 6.setup的两个注意点

- setup执行的时机
  - 在beforeCreate之前执行一次，this是undefined。

- setup的参数
  - props：值为对象，包含：组件外部传递过来，且组件内部声明接收了的属性。
  - context：上下文对象
    - attrs: 值为对象，包含：组件外部传递过来，但没有在props配置中声明的属性, 相当于 ```this.$attrs```。
    - slots: 收到的插槽内容, 相当于 ```this.$slots```。
    - emit: 分发自定义事件的函数, 相当于 ```this.$emit```。





## 7.计算属性与监视

### 7.1 computed函数

- 与Vue2.x中computed配置功能一致

- 写法



```vue
<script>
import { reactive, computed } from 'vue'
export default {
  name: 'Demo',
  setup() {
    let person = reactive({firstName: '张',lastName: '三'})
    
    // 计算属性-简写
    person.fullName = computed(() => { // 直接追加到person对象上
      return person.firstName + '-' + person.lastName
    })
      
    // 计算属性-完整写法
    person.fullName = computed({
      get() {
        return person.firstName + '-' + person.lastName
      },
      set(value) {
        const nameArr = value.split('-')
        person.firstName = nameArr[0]
        person.lastName = nameArr[1]
      },
    })
      
    return {person}
  },
}
</script>

```





### 7.2 watch函数

- 与Vue2.x中watch配置功能一致

- 两个小“坑”：

  - 监视reactive定义的响应式数据时：oldValue无法正确获取、强制开启了深度监视（deep配置失效）。
  - 监视reactive定义的响应式数据中某个属性时：deep配置有效。

  ```js
  //情况一：监视ref定义的响应式数据
  watch(sum,(newValue,oldValue)=>{
  	console.log('sum变化了',newValue,oldValue)
  },{immediate:true})
  
  //情况二：监视多个ref定义的响应式数据
  watch([sum,msg],(newValue,oldValue)=>{
  	console.log('sum或msg变化了',newValue,oldValue)
  }) 
  
  /* 情况三：监视reactive定义的响应式数据
  			若watch监视的是reactive定义的响应式数据，则无法正确获得oldValue！！
  			若watch监视的是reactive定义的响应式数据，则强制开启了深度监视 
  */
  watch(person,(newValue,oldValue)=>{
  	console.log('person变化了',newValue,oldValue)
  },{immediate:true,deep:false}) //此处的deep配置不再奏效
  
  //情况四：监视reactive定义的响应式数据中的某个属性
  watch(()=>person.job,(newValue,oldValue)=>{
  	console.log('person的job变化了',newValue,oldValue)
  },{immediate:true,deep:true}) 
  
  //情况五：监视reactive定义的响应式数据中的某些属性
  watch([()=>person.job,()=>person.name],(newValue,oldValue)=>{
  	console.log('person的job变化了',newValue,oldValue)
  },{immediate:true,deep:true})
  
  //特殊情况
  watch(()=>person.job,(newValue,oldValue)=>{
      console.log('person的job变化了',newValue,oldValue)
  },{deep:true}) //此处由于监视的是reactive素定义的对象中的某个属性，所以deep配置有效
  ```

 

### 7.3 watchEffect函数

- watch的套路是：既要指明监视的属性，也要指明监视的回调。

- watchEffect的套路是：不用指明监视哪个属性，监视的回调中**用到哪个属性，那就监视哪个属性**。

- watchEffect有点像computed：

  - 但computed注重的计算出来的值（回调函数的返回值），所以必须要写返回值。
  - 而watchEffect更注重的是过程（回调函数的函数体），所以不用写返回值。

  ```js
  //watchEffect所指定的回调中用到的数据只要发生变化，则直接重新执行回调。
  const stop = watchEffect((oninvalidate)=>{
      const x1 = sum.value
      const x2 = person.age
      console.log('watchEffect配置的回调执行了')
      oninvalidate(()=>{})
  })
  ```
  
  - 此函数会返回一个停止函数，调用一下会停止监听
  - 函数可以接收一个回调函数，会最先执行，可以停止接口调用等操作







## 8.生命周期

- Vue3.0中可以继续使用Vue2.x中的生命周期钩子，但有有两个被更名：
  - ```beforeDestroy```改名为 ```beforeUnmount```
  - ```destroyed```改名为 ```unmounted```
- Vue3.0也提供了 Composition API 形式的生命周期钩子，与Vue2.x中钩子对应关系如下：
  - `beforeCreate`===>`setup()`
  - `created`====>`setup()`
  - `beforeMount` ===>`onBeforeMount`
  - `mounted`====>`onMounted`
  - `beforeUpdate`===>`onBeforeUpdate`
  - `updated` ====>`onUpdated`
  - `beforeUnmount` ====>`onBeforeUnmount`
  - `unmounted` ====>`onUnmounted`

一样使用前先引入





## 9.自定义hook函数

- 什么是hook？—— 本质是一个函数，把setup函数中使用的Composition API进行了封装。

- 类似于vue2.x中的mixin。

- 自定义hook的优势: 复用代码, 让setup中的逻辑更清楚易懂。

```js
// components/hooks.usePoint.js
import { reactive, onMounted, onUnmounted } from 'vue'
export default function () {
    // 实现鼠标坐标数据
    let point = reactive({
        x: 0,
        y: 0,
    })

    // 实现鼠标坐标方法
    function savePoint(e) {
        console.log(e.pageX, e.pageY)
        point.x = e.x
        point.y = e.y
    }
    // 实现鼠标坐标钩子
    onMounted(() => {
        window.addEventListener('click', savePoint)
    })

    onUnmounted(() => { // 关闭组件卸载
        window.removeEventListener('click', savePoint)
    })

    return point // 返回坐标点
}


```

```js
// Demo.vue
import { ref } from 'vue'
import usePoint from '../hooks/usePoint'
export default {
  name: 'Demo',
  setup() {
    let sum = ref(0)

    let point = usePoint() // 调用函数返回坐标

    return { sum, point } // 模板使用即可
  },
}
```





## 10.toRef/toRefs

- 作用：创建一个 ref 对象，其value值指向另一个对象中的某个属性。
- 语法：```const name = toRef(person,'name')```
- 应用:   要将响应式对象中的某个属性单独提供给外部使用时。


- 扩展：```toRefs``` 与```toRef```功能一致，但可以批量创建多个 ref 对象，语法：```toRefs(person)```

```js
const name2 = toRef(person, 'name')
console.log(name2)

return { // 使用如下方式返回，好处在于模板可以少写一个person.调用对象数据
    person,
    name: toRef(person, 'name'),
    age: toRef(person, 'age'),
    salary: toRef(person.job.j1, 'salary'),
}
```



**toref：**只能修改响应式对象的值，非响应式试图毫无变化

```js
const mane={like:'吃饭'}
const like =toRef(man,'like') // 将属性单独提取出来
```



**toRefs：**结构reactive对象

**toRaw：**将proxy响应式对象变为普通对象





## 11. 动态组件

动态组件 就是：让多个组件使用同一个挂载点，并动态切换，这就是动态组件。

类似路由切换，这个使用场景在Tab栏切换居多

```html
<component :is="A"></component>
```



> 如果你把组件实例放到Reactive Vue会给你一个警告runtime-core.esm-bundler.js:38 [Vue warn]: Vue received a Component which was made a reactive object. This can lead to unnecessary performance overhead, and should be avoided by marking the component with `markRaw` or using `shallowRef` instead of `ref`. 
> Component that was made reactive: 
>
> 这是因为reactive 会进行proxy 代理 而我们组件代理之后毫无用处 节省性能开销 推荐我们使用shallowRef 或者  markRaw 跳过proxy 代理

```ts
const tab = reactive<Com[]>([{
    name: "A组件",
    comName: markRaw(A)
}, {
    name: "B组件",
    comName: markRaw(B)
}])
```







# 三、vue3组件通信方式

**vue2组件通信方式**

**props:**可以实现父子组件、子父组件、甚至兄弟组件通信

**自定义事件**:可以实现子父组件通信

**全局事件总线$bus**:可以实现任意组件通信

**pubsub:**发布订阅模式实现任意组件通信

**vuex**:集中式状态管理容器，实现任意组件通信

**ref**:父组件获取子组件实例VC,获取子组件的响应式数据以及方法

**slot:**插槽(默认插槽、具名插槽、作用域插槽)实现父子组件通信........

## 1. props

props可以实现父子组件通信,在vue3中我们可以通过defineProps获取父组件传递的数据。且在组件内部不需要引入defineProps方法可以直接使用！

**父组件给子组件传递数据**

```vue
<Child info="我爱祖国" :money="money"></Child>
```



**子组件获取父组件传递数据:方式1**

```ts
// js方式
let props = defineProps({
  info:{
   type:String,//接受的数据类型
   default:'默认参数',//接受默认数据
  },
  money:{
   type:Number,
   default:0
}})

// ts方式
const props = defineProps<{
  title: Number
  arr: number[]
}>()
```



**定义默认值：**

```ts
// ts特有的定义默认值
withDefaults(
  defineProps<{
    title: Number
    arr: number[]
  }>(),
  {
    arr: () => [999],
  }
)
```



**子组件获取父组件传递数据:方式2**

```js
let props = defineProps(["info",'money']);
```

子组件获取到props数据就可以在模板中使用了,但是切记props是只读的(只能读取，不能修改)



## 2. 自定义事件

在vue框架中事件分为两种:一种是原生的DOM事件，另外一种自定义事件。

原生DOM事件可以让用户与网页进行交互，比如click、dbclick、change、mouseenter、mouseleave....

自定义事件可以实现子组件给父组件传递数据



- **原生DOM事件：**

代码如下:

```vue
 <pre @click="handler">
      我是祖国的老花骨朵
 </pre>
```


当前代码级给pre标签绑定原生DOM事件点击事件,默认会给事件回调注入event事件对象。当然点击事件想注入多个参数可以按照下图操作。但是切记注入的事件对象务必叫做$event.

```vue
  <div @click="handler1(1,2,3,$event)">我要传递多个参数</div>
```

在vue3框架click、dbclick、change(这类原生DOM事件),不管是在标签、自定义标签上(组件标签)都是原生DOM事件。

**<!--vue2中却不是这样的,在vue2中组件标签需要通过native修饰符才能变为原生DOM事件-->**



- **子传父数据**

自定义事件可以实现子组件给父组件传递数据.在项目中是比较常用的。

比如在父组件内部给子组件(Event2)绑定一个自定义事件

在Event2子组件内部触发这个自定义事件：

```vue
<template>
  <div>
    <button @click="handler">点击我触发xxx自定义事件</button>
  </div>
</template>

<script setup>
let $emit = defineEmits(["xxx"]);
const handler = () => {
  $emit("xxx", "法拉利", "茅台");
};
</script>

ts写法
<script setup lang="ts">
const emit = defineEmits<{
  (e: 'on-click', title: string): void
}>()
</script>
```

父组件：

```vue
<Event2  @xxx="handler3"></Event2>

<script setup lang="ts">
const handler3 = (param1,param2)=>{
    console.log(param1,param2);
}
</script>
```





我们会发现在script标签内部,使用了`defineEmits`方法，此方法是vue3提供的方法,不需要引入直接使用。

defineEmits方法执行，传递一个数组，数组元素即为将来组件需要触发的自定义事件类型，此方执行会返回一个$emit方法用于触发自定义事件。

当点击按钮的时候，事件回调内部调用$emit方法去触发自定义事件,第一个参数为触发事件类型，第二个、三个、N个参数即为传递给父组件的数据。

需要注意的是:代码如下

```vue
<Event2  @xxx="handler3" @click="handler"></Event2>
```

正常说组件标签书写@click应该为原生DOM事件,但是如果子组件内部通过defineEmits定义就变为自定义事件了

```js
let $emit = defineEmits(["xxx",'click']);
```



## 3. 全局事件总线

全局事件总线可以实现任意组件通信，在vue2中可以根据VM与VC关系推出全局事件总线。

但是在vue3中没有Vue构造函数，也就没有Vue.prototype.以及组合式API写法没有this，

那么在Vue3想实现全局事件的总线功能就有点不现实啦，如果想在Vue3中使用全局事件总线功能

可以使用插件mitt实现。

**mitt:官网地址:https://www.npmjs.com/package/mitt**



首先创建对象：ts文件

```js
import mitt from "mitt";
const $bus = mitt();
export default $bus;
```



发送数据：

```vue
<button @click="handler">点击送车</button>

<script setup>
import $bus from "../bus";
const handler=()=>{
    $bus.emit('car','法拉利')
}
<script/>
```



接收数据：

```vue
<script setup>
import $bus from "../bus";
import {onMounted}from "vue";
onMounted(()=>{
    $bus.on('car',(car)=>{
        console.log(car);
    })
})
</script>
```





## 4. v-model

v-model指令可是收集表单数据(数据双向绑定)，除此之外它也可以实现父子组件数据同步。

而v-model实指利用props[modelValue]与自定义事件[update:modelValue]实现的。

下方代码:相当于给组件Child传递一个props(modelValue)与绑定一个自定义事件update:modelValue

实现父子组件数据同步

```vue
<Child v-model="msg"></Child>
```

在vue3中一个组件可以通过使用多个v-model,让父子组件多个数据同步,下方代码相当于给组件Child传递两个props分别是pageNo与pageSize，以及绑定两个自定义事件update:pageNo与update:pageSize实现父子数据同步

```vue
<Child v-model:pageNo="msg" v-model:pageSize="msg1"></Child>
```



## 5. useAttrs

在Vue3中可以利用useAttrs方法获取组件的属性与事件(包含:原生DOM事件或者自定义事件),次函数功能类似于Vue2框架中$attrs属性与$listeners方法。

比如:在父组件内部使用一个子组件my-button

```vue
<my-button type="success" size="small" title='标题' @click="handler"></my-button>
```

子组件内部可以通过useAttrs方法获取组件属性与事件.因此你也发现了，它类似于props,可以接受父组件传递过来的属性与属性值。需要注意如果defineProps接受了某一个属性，useAttrs方法返回的对象身上就没有相应属性与属性值。

```vue
<script setup lang="ts">
import {useAttrs} from 'vue';
let $attrs = useAttrs();
</script>
```



## 6. ref与$parent

ref,提及到ref可能会想到它可以获取元素的DOM或者获取子组件实例的VC。既然可以在父组件内部通过ref获取子组件实例VC，那么子组件内部的方法与响应式数据父组件可以使用的。

比如:在父组件挂载完毕获取组件实例

父组件内部代码:

```vue
<template>
  <div>
    <h1>ref与$parent</h1>
    <Son ref="son"></Son>
  </div>
</template>
<script setup lang="ts">
import Son from "./Son.vue";
import { onMounted, ref } from "vue";
const son = ref();
onMounted(() => {
  console.log(son.value);
});
</script>
```

但是需要注意，如果想让父组件获取子组件的数据或者方法需要通过`defineExpose`对外暴露,因为vue3中组件内部的数据对外“关闭的”，外部不能访问

```vue
<script setup lang="ts">
import { ref } from "vue";
//数据
let money = ref(1000);
//方法
const handler = ()=>{
}
defineExpose({
  money,
   handler
})
</script>
```

`$parent`可以获取某一个组件的父组件实例VC,因此可以使用父组件内部的数据与方法。必须子组件内部拥有一个按钮点击时候获取父组件实例，当然父组件的数据与方法需要通过defineExpose方法对外暴露

```vue
<button @click="handler($parent)">点击我获取父组件实例</button>
```



## 7. provide与inject

**provide[提供]**  **inject[注入]**

vue3提供两个方法provide与inject,可以实现隔辈组件传递参数

组件组件提供数据:

provide方法用于提供数据，此方法执需要传递两个参数,分别提供数据的key与提供数据value

```vue
<script setup lang="ts">
import {provide} from 'vue'
provide('token','admin_token');
</script>
```

后代组件可以通过inject方法获取数据,通过key获取存储的数值

```vue
<script setup lang="ts">
import {inject} from 'vue'
let token = inject('token');
</script>
```







## 8. pinia

**pinia官网:https://pinia.web3doc.top/**

pinia也是集中式管理状态容器,类似于vuex。但是核心概念没有mutation、modules,使用方式参照官网





## 9. slot插槽

插槽：默认插槽、具名插槽、作用域插槽可以实现父子组件通信.



### 9.1 默认插槽

在子组件内部的模板中书写slot全局组件标签

```vue
<template>
  <div>
    <slot></slot>
  </div>
</template>
<script setup lang="ts">
</script>
<style scoped>
</style>
```

在父组件内部提供结构：Todo即为子组件,在父组件内部使用的时候，在双标签内部书写结构传递给子组件

注意开发项目的时候默认插槽一般只有一个

```vue
<Todo>
  <h1>我是默认插槽填充的结构</h1>
</Todo>
```



### 9.2 具名插槽

顾名思义，此插槽带有名字在组件内部留多个指定名字的插槽。

下面是一个子组件内部,模板中留两个插槽

```vue
<template>
  <div>
    <h1>todo</h1>
    <slot name="a"></slot>
    <slot name="b"></slot>
  </div>
</template>
<script setup lang="ts">
</script>

<style scoped>
</style>
```

父组件内部向指定的具名插槽传递结构。需要注意v-slot：可以替换为#

```vue
<template>
  <div>
    <h1>slot</h1>
    <Todo>
      <template v-slot:a>  //可以用#a替换
        <div>填入组件A部分的结构</div>
      </template>
      <template v-slot:b>//可以用#b替换
        <div>填入组件B部分的结构</div>
      </template>
    </Todo>
  </div>
</template>

<script setup lang="ts">
import Todo from "./Todo.vue";
</script>
<style scoped>
</style>
```



### 9.3 作用域插槽

作用域插槽：可以理解为，子组件数据由父组件提供，但是子组件内部决定不了自身结构与外观(样式)

子组件Todo代码如下:

```vue
<template>
  <div>
    <h1>todo</h1>
    <ul>
     <!--组件内部遍历数组-->
      <li v-for="(item,index) in todos" :key="item.id">
         <!--作用域插槽将数据回传给父组件-->
         <slot :$row="item" :$index="index"></slot>
      </li>
    </ul>
  </div>
</template>
<script setup lang="ts">
defineProps(['todos']);//接受父组件传递过来的数据
</script>
<style scoped>
</style>
```

父组件内部代码如下:

```vue
<template>
  <div>
    <h1>slot</h1>
    <Todo :todos="todos">
      <template v-slot="{$row,$index}">
         <!--父组件决定子组件的结构与外观-->
         <span :style="{color:$row.done?'green':'red'}">{{$row.title}}</span>
      </template>
    </Todo>
  </div>
</template>

<script setup lang="ts">
import Todo from "./Todo.vue";
import { ref } from "vue";
//父组件内部数据
let todos = ref([
  { id: 1, title: "吃饭", done: true },
  { id: 2, title: "睡觉", done: false },
  { id: 3, title: "打豆豆", done: true },
]);
</script>
<style scoped>
</style>
```





## 10.provide与inject祖传后



<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20221125204414331.png" alt="image-20221125204414331" style="zoom: 67%;" />

- 作用：实现<strong style="color:#DD5145">祖与后代组件间</strong>通信

- 套路：父组件有一个 `provide` 选项来提供数据，后代组件有一个 `inject` 选项来开始使用这些数据

- 具体写法：

  1. 祖组件中：

```js
import { provide } from 'vue' // 引入

let car = reactive({ name: '车', price: 10 })

provide('car', car) // 给后代传数据
```

​		 2. 后代组件中：

```js
import { inject } from '@vue/runtime-core'

let car = inject('car') // 接收

return { car}
```





## 11. mitt发布订阅

```shell
npm install mitt -S
```



在mian.ts配置：

```ts
import mitt from 'mitt'
const Mit = mitt()


//TypeScript注册
// 由于必须要拓展ComponentCustomProperties类型才能获得类型提示
declare module "vue" {
    export interface ComponentCustomProperties {
        $Bus: typeof Mit
}
    
app.config.globalProperties.$Bus = Mit
```



A组件发布消息：

```ts
// 引入当前组件实例
import { getCurrentInstance } from 'vue'

const instance = getCurrentInstance()
// 点击触发
const emit = () => {
  instance?.proxy?.$Bus.emit('on-yr', '消息')
}
```



B组件接收消息：

```ts
import { getCurrentInstance } from 'vue'

const instance = getCurrentInstance()
instance?.proxy?.$Bus.on('on-yr', (str) => {
  console.log(str)
})
```



监听多条消息时可以：

```ts
instance?.proxy?.$Bus.on('*', (type,str) => {
  console.log(str)
})
```



取消指定mitt事件：

```ts
const bus = (str: any) => {
  console.log(str)
}
instance?.proxy?.$Bus.on('on-yr', bus)
instance?.proxy?.$Bus.off('on-yr', bus)

instance?.proxy?.$Bus.all.clear() // 清除所有
```













# 四、其它 Composition API



## 1.shallowReactive 与 shallowRef

- shallowReactive：只处理对象最外层属性的响应式（浅响应式）。
- shallowRef：只处理基本数据类型的响应式, 不进行对象的响应式处理。

- 什么时候使用?
  -  如果有一个对象数据，结构比较深, 但变化时只是外层属性变化 ===> shallowReactive。
  -  如果有一个对象数据，后续功能不会修改该对象中的属性，而是生新的对象来替换 ===> shallowRef。



```js
import { shallowReactive, shallowRef } from 'vue'

let person = shallowReactive({
      name: '张三',
      age: 19,
      job: {
        j1: {
          salary: 20,
        },
      },
    })
```





## 2.readonly 与 shallowReadonly

- readonly: 让一个响应式数据变为只读的（深只读）。
- shallowReadonly：让一个响应式数据变为只读的（浅只读）。
- 应用场景: 不希望数据被修改时。



```js
let person = reactive({
      name: '张三',
      age: 19,
      job: {
        j1: {
          salary: 20,
        },
      },
    })
person = readonly(person)
person = shallowReadonly(person)
```



## 3.toRaw 与 markRaw

- toRaw：
  - 作用：将一个由```reactive```生成的<strong style="color:orange">响应式对象</strong>转为<strong style="color:orange">普通对象</strong>。
  - 使用场景：用于读取响应式对象对应的普通对象，对这个普通对象的所有操作，不会引起页面更新。
- markRaw：
  - 作用：标记一个对象，使其永远不会再成为响应式对象。
  - 应用场景:
    1. 有些值不应被设置为响应式的，例如复杂的第三方类库等。
    2. 当渲染具有不可变数据源的大列表时，跳过响应式转换可以提高性能。





## 4.customRef

- 作用：创建一个自定义的 ref，并对其依赖项跟踪和更新触发进行显式控制。

- 实现防抖效果：

```vue
<script>
import { ref, customRef } from 'vue'
export default {
  name: 'App',
  setup() {
    // let keyword = ref('hello') // 使用vue提供的ref

    //自定义ref
    function myRef(value) {
      let timer
      return customRef((track, trigger) => {
        return {
          get() {
            track() // 通知vue追踪value的变化（提前和get商量，使之认为value是有用的）
            return value
          },
          set(newvalue) {
            value = newvalue
            clearTimeout(timer)
            timer = setTimeout(() => {
              trigger() // 通知vue解析模板
            }, 1000)
          },
        }
      })
    }

    let keyword = myRef('hello')
    return { keyword }
  },
}
</script>
```









## 5.响应式数据的判断

- isRef: 检查一个值是否为一个 ref 对象
- isReactive: 检查一个对象是否是由 `reactive` 创建的响应式代理
- isReadonly: 检查一个对象是否是由 `readonly` 创建的只读代理
- isProxy: 检查一个对象是否是由 `reactive` 或者 `readonly` 方法创建的代理

```js
let car = reactive({ name: '车', price: 10 })
let sum = ref(0)
let car2 = readonly(car)

console.log(isRef(sum))
console.log(isReactive(car))
console.log(isReadonly(car2))
console.log(isProxy(car))
```








# 五、新的组件

## 1.Fragment

- 在Vue2中: 组件必须有一个根标签
- 在Vue3中: 组件可以没有根标签, 内部会将多个标签包含在一个Fragment虚拟元素中
- 好处: 减少标签层级, 减小内存占用





## 2.Teleport组件移动

- 什么是Teleport？—— `Teleport` 是一种能够将我们的<strong style="color:#DD5145">组件html结构</strong>移动到指定位置的技术。

```vue
<teleport to="移动位置">
	<div v-if="isShow" class="mask">
		<div class="dialog">
			<h3>我是一个弹窗</h3>
			<button @click="isShow = false">关闭弹窗</button>
		</div>
	</div>
</teleport>
```





## 3.Suspense异步

- 等待异步组件时渲染一些额外内容，让应用有更好的用户体验

- 在大型应用中，我们可能需要将应用分割成小一些的代码块 并且减少主包的体积



子组件顶层 `await`：setup中可以使用顶层 await。结果代码会被编译成 async setup()

```html
<script setup>
const post = await fetch(`/api/post/1`).then(r => r.json())
</script>
```



异步引入组件：  使用```Suspense```包裹组件，并配置好```default``` 与 ```fallback```

```html
<template>
	<div class="app">
		<Suspense>
			<template v-slot:default>
				<Dialog/>
			</template>
			<template v-slot:fallback>
				<h3>加载中.....</h3>
			</template>
		</Suspense>
	</div>
</template>


<script setup lang="ts">
import { reactive, ref, markRaw, toRaw, defineAsyncComponent } from 'vue'
 
const Dialog = defineAsyncComponent(() => import('../../components/Dialog/index.vue'))
 
//完整写法
const AsyncComp = defineAsyncComponent({
  // 加载函数
  loader: () => import('./Foo.vue'),
 
  // 加载异步组件时使用的组件
  loadingComponent: LoadingComponent,
  // 展示加载组件前的延迟时间，默认为 200ms
  delay: 200
  // 加载失败后展示的组件
  errorComponent: ErrorComponent,
  // 如果提供了一个 timeout 时间限制，并超时了
  // 也会显示这里配置的报错组件，默认值是：Infinity
  timeout: 3000
})
```



## 4. keep-alive缓存

有时候我们不希望组件被重新渲染影响使用体验；或者处于性能考虑，避免多次重复渲染降低性能。而是希望组件可以缓存下来,维持当前的状态，比如表单输入。这时候就需要用到`keep-alive`组件。

```html
<keep-alive>
  <comp-a v-if="a > 1"></comp-a>
  <comp-b v-else></comp-b>
</keep-alive>
```



有条件的进行缓存，`include`表示缓存哪个、`exclude`表示不缓存哪个、`max`表示缓存组件数量，缓存常使用的

```html
<keep-alive :include="['a']" :max=""> 
  <a v-if="a > 1"></a>
  <b v-else></b>
</keep-alive>
```



**开启keep-alive新增2个生命周期：**`onActivated`，`deactivated`

- 初次进入时： onMounted> onActivated
- 退出后触发 deactivated

再次进入：只会触发 onActivated
事件挂载的方法等，只执行一次的放在 onMounted中；组件每次进去执行的方法放在 onActivated中





## 5. Transition动画

官网：https://cn.vuejs.org/guide/built-ins/transition.html#css-based-transitions

是一个内置组件，这意味着它在任意别的组件中都可以被使用，无需注册。它可以将进入和离开动画应用到通过默认插槽传递给它的元素或组件上。进入或离开可以由以下的条件之一触发：

- 由 `v-if` 所触发的切换
- 由 `v-show` 所触发的切换
- 由特殊元素 `<component>` 切换的动态组件
- 改变特殊的 `key` 属性



### 5.1 基础使用

首先将组件包裹并命名：

```html
<Transition name="fade">
  <p v-if="show">hello</p>
</Transition>
```



1. `v-enter-from`：进入动画的起始状态。
2. `v-enter-active`：进入动画的生效状态。写过渡的c3 transition动画
3. `v-enter-to`：进入动画的结束状态。一般不写或与原始保持一致
4. `v-leave-from`：离开动画的起始状态。
5. `v-leave-active`：离开动画的生效状态。写过渡的c3 transition动画
6. `v-leave-to`：离开动画的结束状态。在一个离开动画被触发后的下一帧被添加 (也就是 `v-leave-from` 被移除的同时)，在过渡或动画完成之后移除。



**控制过渡时长：**

```html
<Transition :duration="550">...</Transition>
<Transition :duration="{enter:50,leave:500}">...</Transition>
```



### 5.2 第三方库

每个状态都能**自定义类名**：可以结合第三方库使用

```shell
npm i animate.css -S
```

页面引入：

```js
import 'animate.css'
```

使用：

```html
<Transition
  name="custom-classes"
  enter-active-class="animate__animated animate__tada"
  leave-active-class="animate__animated animate__bounceOutRight"
>
  <p v-if="show">hello</p>
</Transition>
```



### 5.3 Transition-group

用法一致，主要应用在如v-for渲染的列表





# 六、其他

## 1.全局API的转移

- Vue 2.x 有许多全局 API 和配置。

  - 例如：注册全局组件、注册全局指令等。

    ```js
    //注册全局组件
    Vue.component('MyButton', {
      data: () => ({
        count: 0
      }),
      template: '<button @click="count++">Clicked {{ count }} times.</button>'
    })
    
    //注册全局指令
    Vue.directive('focus', {
      inserted: el => el.focus()
    }
    ```

- Vue3.0中对这些API做出了调整：

  - 将全局的API，即：```Vue.xxx```调整到应用实例（```app```）上

    | 2.x 全局 API（```Vue```） | 3.x 实例 API (`app`)                        |
    | ------------------------- | ------------------------------------------- |
    | Vue.config.xxxx           | app.config.xxxx                             |
    | Vue.config.productionTip  | <strong style="color:#DD5145">移除</strong> |
    | Vue.component             | app.component                               |
    | Vue.directive             | app.directive                               |
    | Vue.mixin                 | app.mixin                                   |
    | Vue.use                   | app.use                                     |
    | Vue.prototype             | app.config.globalProperties                 |





## 2. css绑定setup



```js
const color=ref('pink')

.box{
	color:v-bind(color)
}
```



## 3. 自动引包插件

```shell
npm i unplugin-auto-import
```

vite.config.ts

```ts
import AutoImport from 'unplugin-auto-import/vite'

plugins: [
    vue(),
    AutoImport({
      imports: ['vue'],
      dts: 'src/auto-import.d.ts'
})],
```

