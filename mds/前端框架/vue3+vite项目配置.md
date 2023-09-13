> 创建日期：2023-7-23
>
> 修改日期：2023-9-13



# 一、 项目初始化

从 0 开始搭建一个 vue3 版本的后台管理系统。一个项目要有统一的规范，需要使用 eslint+stylelint+prettier 来对我们的代码质量做检测和修复，需要使用 husky 来做 commit 拦截，需要使用 commitlint 来统一提交规范，需要使用 preinstall 来统一包管理工具。

下面我们就用这一套规范来初始化我们的项目，集成一个规范的模版。



## 1. 环境准备

- node v16.14.2
- pnpm 8.0.0



## 2. 初始化项目

本项目使用 vite 进行构建，vite 官方中文文档参考：[cn.vitejs.dev/guide/](https://cn.vitejs.dev/guide/)

**pnpm:performant npm ，意味“高性能的 npm”。[pnpm](https://so.csdn.net/so/search?q=pnpm&spm=1001.2101.3001.7020)由 npm/yarn 衍生而来，解决了 npm/yarn 内部潜在的 bug，极大的优化了性能，扩展了使用场景。被誉为“最先进的包管理工具”**

pnpm 安装指令

```shell
npm i -g pnpm
```

项目初始化命令:

```powershell
pnpm create vite
```

进入到项目根目录 pnpm install 安装全部依赖.安装完依赖运行程序:pnpm run dev



## 3. 常用文件目录

```ts
├─src
|  ├─App.vue
|  ├─main.ts
|  ├─permission.ts //路由鉴权
|  ├─setting.ts // 项目设置
|  ├─vite-env.d.ts
|  ├─views	// 具体页面效果
|  |   ├─login
|  |   |   └index.vue
|  |   ├─home
|  |   |  └index.vue
|  |   ├─404
|  |   |  └index.vue
|  ├─utils	// 工具文件：axios二次封装，时间格式化等
|  ├─styles	// 清除默认样式，配置全局变量
|  |   ├─index.scss
|  |   ├─variable.scss
|  ├─store	// pinia仓库
|  |   ├─index.ts	// 导出大仓库
|  |   ├─modules 	// 配置小仓库
|  |   |    ├─user.ts
|  |   |    ├─types	// 定义ts类型
|  |   |    |   └type.ts
|  ├─router	// 路由
|  |   ├─index.ts	// 配置与注册路由
|  |   └routers.ts	// 分割路由
|  ├─layout // 公共页面大框架
|  |   ├─index.vue
|  |   ├─menu
|  |   |  └index.vue
|  ├─directive // 自定义指令
|  |     └has.ts
|  ├─components // 注册常用组件
|  |     ├─index.ts // 注册为全局组件
|  |     ├─SvgIcon
|  |     |    └index.vue
|  ├─assets
|  |   ├─images
|  |   ├─icons
|  ├─api // 全局管理api
|  |  ├─user
|  |  |  ├─index.ts
|  |  |  └type.ts
├─mock
|  └user.ts
```







# 二、项目配置

## 1. eslint 配置

**eslint 中文官网:http://eslint.cn/**

ESLint 最初是由[Nicholas C. Zakas](http://nczonline.net/) 于 2013 年 6 月创建的开源项目。它的目标是提供一个插件化的**javascript 代码检测工具**

首先安装 eslint

```shell
pnpm i eslint -D
```

生成配置文件:.eslint.cjs

```shell
npx eslint --init
```

**.eslint.cjs 配置文件**

```json
module.exports = {
   //运行环境
    "env": {
        "browser": true,//浏览器端
        "es2021": true,//es2021
    },
    //规则继承
    "extends": [
       //全部规则默认是关闭的,这个配置项开启推荐规则,推荐规则参照文档
       //比如:函数不能重名、对象不能出现重复key
        "eslint:recommended",
        //vue3语法规则
        "plugin:vue/vue3-essential",
        //ts语法规则
        "plugin:@typescript-eslint/recommended"
    ],
    //要为特定类型的文件指定处理器
    "overrides": [
    ],
    //指定解析器:解析器
    //Esprima 默认解析器
    //Babel-ESLint babel解析器
    //@typescript-eslint/parser ts解析器
    "parser": "@typescript-eslint/parser",
    //指定解析器选项
    "parserOptions": {
        "ecmaVersion": "latest",//校验ECMA最新版本
        "sourceType": "module"//设置为"script"（默认），或者"module"代码在ECMAScript模块中
    },
    //ESLint支持使用第三方插件。在使用插件之前，您必须使用npm安装它
    //该eslint-plugin-前缀可以从插件名称被省略
    "plugins": [
        "vue",
        "@typescript-eslint"
    ],
    //eslint规则
    "rules": {
    }
}
```

**1.1 vue3 环境代码校验插件**

```
# 让所有与prettier规则存在冲突的Eslint rules失效，并使用prettier进行代码检查
"eslint-config-prettier": "^8.6.0",
"eslint-plugin-import": "^2.27.5",
"eslint-plugin-node": "^11.1.0",
# 运行更漂亮的Eslint，使prettier规则优先级更高，Eslint优先级低
"eslint-plugin-prettier": "^4.2.1",
# vue.js的Eslint插件（查找vue语法错误，发现错误指令，查找违规风格指南
"eslint-plugin-vue": "^9.9.0",
# 该解析器允许使用Eslint校验所有babel code
"@babel/eslint-parser": "^7.19.1",
```

安装指令

```shell
pnpm install -D eslint-plugin-import eslint-plugin-vue eslint-plugin-node eslint-plugin-prettier eslint-config-prettier eslint-plugin-node @babel/eslint-parser
```

**1.2 修改.eslintrc.cjs 配置文件**

```js
// @see https://eslint.bootcss.com/docs/rules/

module.exports = {
  env: {
    browser: true,
    es2021: true,
    node: true,
    jest: true,
  },
  /* 指定如何解析语法 */
  parser: 'vue-eslint-parser',
  /** 优先级低于 parse 的语法解析配置 */
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module',
    parser: '@typescript-eslint/parser',
    jsxPragma: 'React',
    ecmaFeatures: {
      jsx: true,
    },
  },
  /* 继承已有的规则 */
  extends: [
    'eslint:recommended',
    'plugin:vue/vue3-essential',
    'plugin:@typescript-eslint/recommended',
    'plugin:prettier/recommended',
  ],
  plugins: ['vue', '@typescript-eslint'],
  /*
   * "off" 或 0    ==>  关闭规则
   * "warn" 或 1   ==>  打开的规则作为警告（不影响代码执行）
   * "error" 或 2  ==>  规则作为一个错误（代码不能执行，界面报错）
   */
  rules: {
    // eslint（https://eslint.bootcss.com/docs/rules/）
    'no-var': 'error', // 要求使用 let 或 const 而不是 var
    'no-multiple-empty-lines': ['warn', { max: 1 }], // 不允许多个空行
    'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off',
    'no-unexpected-multiline': 'error', // 禁止空余的多行
    'no-useless-escape': 'off', // 禁止不必要的转义字符

    // typeScript (https://typescript-eslint.io/rules)
    '@typescript-eslint/no-unused-vars': 'error', // 禁止定义未使用的变量
    '@typescript-eslint/prefer-ts-expect-error': 'error', // 禁止使用 @ts-ignore
    '@typescript-eslint/no-explicit-any': 'off', // 禁止使用 any 类型
    '@typescript-eslint/no-non-null-assertion': 'off',
    '@typescript-eslint/no-namespace': 'off', // 禁止使用自定义 TypeScript 模块和命名空间。
    '@typescript-eslint/semi': 'off',

    // eslint-plugin-vue (https://eslint.vuejs.org/rules/)
    'vue/multi-word-component-names': 'off', // 要求组件名称始终为 “-” 链接的单词
    'vue/script-setup-uses-vars': 'error', // 防止<script setup>使用的变量<template>被标记为未使用
    'vue/no-mutating-props': 'off', // 不允许组件 prop的改变
    'vue/attribute-hyphenation': 'off', // 对模板中的自定义组件强制执行属性命名样式
  },
}
```

**1.3 eslintignore 忽略文件**

```
dist
node_modules
```

**1.4 运行脚本**

package.json 新增两个运行脚本

```json
"scripts": {
    "lint": "eslint src", // npm run lint 检查代码
    "fix": "eslint src --fix", // 更改
}
```



## 2. 配置**prettier**

有了 eslint，为什么还要有 prettier？eslint 针对的是 javascript，他是一个检测工具，包含 js 语法以及少部分格式问题，在 eslint 看来，语法对了就能保证代码正常运行，格式问题属于其次；

而 prettier 属于格式化工具，它看不惯格式不统一，所以它就把 eslint 没干好的事接着干。另外，prettier 支持包含 js 在内的多种语言。

总结起来，**eslint 和 prettier 这俩兄弟一个保证 js 代码质量，一个保证代码美观。**

**2.1 安装依赖包**

```shell
pnpm install -D eslint-plugin-prettier prettier eslint-config-prettier
```

**2.2 prettierrc.json 添加规则**

```json
{
  "singleQuote": true,
  "semi": false,
  "bracketSpacing": true,
  "htmlWhitespaceSensitivity": "ignore",
  "endOfLine": "auto",
  "trailingComma": "all",
  "tabWidth": 2
}
```

**2.3 prettierignore 忽略文件**

```
/dist/*
/html/*
.local
/node_modules/**
**/*.svg
**/*.sh
/public/*
```

**通过 pnpm run lint 去检测语法，如果出现不规范格式,通过 pnpm run fix 修改**



## 3. 配置 stylelint

[stylelint](https://stylelint.io/)为 css 的 lint 工具。可格式化 css 代码，检查 css 语法错误与不合理的写法，指定 css 书写顺序等。

我们的项目中使用 scss 作为预处理器，安装以下依赖：

```shell
pnpm add sass sass-loader stylelint postcss postcss-scss postcss-html stylelint-config-prettier stylelint-config-recess-order stylelint-config-recommended-scss stylelint-config-standard stylelint-config-standard-vue stylelint-scss stylelint-order stylelint-config-standard-scss -D
```

**3.1 `.stylelintrc.cjs`配置文件**

**官网:https://stylelint.bootcss.com/**

```js
// @see https://stylelint.bootcss.com/

module.exports = {
  extends: [
    'stylelint-config-standard', // 配置stylelint拓展插件
    'stylelint-config-html/vue', // 配置 vue 中 template 样式格式化
    'stylelint-config-standard-scss', // 配置stylelint scss插件
    'stylelint-config-recommended-vue/scss', // 配置 vue 中 scss 样式格式化
    'stylelint-config-recess-order', // 配置stylelint css属性书写顺序插件,
    'stylelint-config-prettier', // 配置stylelint和prettier兼容
  ],
  overrides: [
    {
      files: ['**/*.(scss|css|vue|html)'],
      customSyntax: 'postcss-scss',
    },
    {
      files: ['**/*.(html|vue)'],
      customSyntax: 'postcss-html',
    },
  ],
  ignoreFiles: [
    '**/*.js',
    '**/*.jsx',
    '**/*.tsx',
    '**/*.ts',
    '**/*.json',
    '**/*.md',
    '**/*.yaml',
  ],
  /**
   * null  => 关闭该规则
   * always => 必须
   */
  rules: {
    'value-keyword-case': null, // 在 css 中使用 v-bind，不报错
    'no-descending-specificity': null, // 禁止在具有较高优先级的选择器后出现被其覆盖的较低优先级的选择器
    'function-url-quotes': 'always', // 要求或禁止 URL 的引号 "always(必须加上引号)"|"never(没有引号)"
    'no-empty-source': null, // 关闭禁止空源码
    'selector-class-pattern': null, // 关闭强制选择器类名的格式
    'property-no-unknown': null, // 禁止未知的属性(true 为不允许)
    'block-opening-brace-space-before': 'always', //大括号之前必须有一个空格或不能有空白符
    'value-no-vendor-prefix': null, // 关闭 属性值前缀 --webkit-box
    'property-no-vendor-prefix': null, // 关闭 属性前缀 -webkit-mask
    'selector-pseudo-class-no-unknown': [
      // 不允许未知的选择器
      true,
      {
        ignorePseudoClasses: ['global', 'v-deep', 'deep'], // 忽略属性，修改element默认样式的时候能使用到
      },
    ],
  },
}
```

**3.2 stylelintignore 忽略文件**

```
/node_modules/*
/dist/*
/html/*
/public/*
```

**3.3 运行脚本**

```json
"scripts": {
	"lint:style": "stylelint src/**/*.{css,scss,vue} --cache --fix"
}
```

最后配置统一的 prettier 来格式化我们的 js 和 css，html 代码

```json
 "scripts": {
    "dev": "vite --open",
    "build": "vue-tsc && vite build",
    "preview": "vite preview",
    "lint": "eslint src",
    "fix": "eslint src --fix",

    "format": "prettier --write \"./**/*.{html,vue,ts,js,json,md}\"",
    "lint:eslint": "eslint src/**/*.{ts,vue} --cache --fix",
    "lint:style": "stylelint src/**/*.{css,scss,vue} --cache --fix"
  },
```

**当我们运行`pnpm run format`的时候，会把代码直接格式化**



## 4. 配置 husky

在上面我们已经集成好了我们代码校验工具，但是需要每次手动的去执行命令才会格式化我们的代码。如果有人没有格式化就提交了远程仓库中，那这个规范就没什么用。所以我们需要强制让开发人员按照代码规范来提交。

要做到这件事情，就需要利用 husky 在代码提交之前触发 git hook(git 在客户端的钩子)，然后执行`pnpm run format`来自动的格式化我们的代码。

安装`husky`：

```shell
pnpm install -D husky
```

**执行**：

```shell
npx husky-init
```

会在根目录下生成个一个.husky 目录，在这个目录下面会有一个 pre-commit 文件，这个文件里面的命令在我们执行 commit 的时候就会执行

**在`.husky/pre-commit`文件添加如下命令：**

```
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"
pnpm run format
```

当我们对代码进行 commit 操作的时候，就会执行命令，对代码进行格式化，然后再提交。



## 5. 配置 commitlint

对于我们的 commit 信息，也是有统一规范的，不能随便写,要让每个人都按照统一的标准来执行，我们可以利用**commitlint**来实现。

**安装包：**

```shell
pnpm add @commitlint/config-conventional @commitlint/cli -D
```

**添加配置文件，新建`commitlint.config.cjs`(注意是 cjs)，然后添加下面的代码：**

```json
module.exports = {
  extends: ['@commitlint/config-conventional'],
  // 校验规则
  rules: {
    'type-enum': [
      2,
      'always',
      [
        'feat',
        'fix',
        'docs',
        'style',
        'refactor',
        'perf',
        'test',
        'chore',
        'revert',
        'build',
      ],
    ],
    'type-case': [0],
    'type-empty': [0],
    'scope-empty': [0],
    'scope-case': [0],
    'subject-full-stop': [0, 'never'],
    'subject-case': [0, 'never'],
    'header-max-length': [0, 'always', 72],
  },
}
```

**在`package.json`中配置 scripts 命令：**

```json
# 在scrips中添加下面的代码
{
"scripts": {
    "commitlint": "commitlint --config commitlint.config.cjs -e -V"
  },
}
```



**配置 husky：**

```shell
npx husky add .husky/commit-msg
```

**在生成的 commit-msg 文件中添加下面的命令：**

```
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"
pnpm commitlint
```

当我们 commit 提交信息时，就不能再随意写了，必须是 git commit -m 'fix: xxx' 符合类型的才可以，**需要注意的是类型的后面需要用英文的 :，并且冒号后面是需要空一格的，这个是不能省略的**


**配置结束，现在当我们填写`commit`信息的时候，前面就需要带着下面的`subject`：**

```
'feat',//新特性、新功能 ✨  🚧
'fix',//修改bug 🐛
'docs',//文档修改 📝
'style',//代码格式修改, 注意不是 css 修改 🏗
'refactor',//代码重构 🔨
'perf',//优化相关，比如提升性能、体验 🐎 ⚡️
'test',//测试用例修改 ✅
'chore',//其他修改, 比如改变构建流程、或者增加依赖库、工具等
'revert',//回滚到上一个版本 ⏪
'build',//编译相关的修改，例如发布版本、对项目构建或者依赖的改动 🔧
```


**emoji使用：**

| 🎨 (调色板)           | :art:                       | 改进代码结构/代码格式        |
| -------------------- | --------------------------- | ---------------------------- |
| ⚡️ (闪电)🐎 (赛马)     | :zap::racehorse:            | 提升性能                     |
| 🔥 (火焰)             | :fire:                      | 移除代码或文件               |
| 🐛 (bug)              | :bug:                       | 修复 bug                     |
| 🚑 (急救车)           | :ambulance:                 | 重要补丁                     |
| ✨ (火花)             | :sparkles:                  | 引入新功能                   |
| 📝 (备忘录)           | :memo:                      | 撰写文档                     |
| 🚀 (火箭)             | :rocket:                    | 部署功能                     |
| 💄 (口红)             | :lipstick:                  | 更新 UI 和样式文件           |
| 🎉 (庆祝)             | :tada:                      | 初次提交                     |
| ✅ (白色复选框)       | :white_check_mark:          | 更新测试                     |
| 🔒 (锁)               | :lock:                      | 修复安全问题                 |
| 🍎 (苹果)             | :apple:                     | 修复 macOS 下的问题          |
| 🐧 (企鹅)             | :penguin:                   | 修复 Linux 下的问题          |
| 🏁 (旗帜)             | :checkered_flag:            | 修复 Windows 下的问题        |
| 🤖（机器人）          | :robot:                     | 修复 Android 下的问题        |
| 🍏 (绿苹果)           | :green_apple:               | 修复 iOS 下的问题            |
| 🔖 (书签)             | :bookmark:                  | 发行/版本标签                |
| 🚨 (警车灯)           | :rotating_light:            | 移除 linter 警告             |
| 🚧 (施工)             | :construction:              | 工作进行中                   |
| 👷 (工人)             | :construction_worker:       | 添加 CI 构建系统             |
| 💚 (绿心)             | :green_heart:               | 修复 CI 构建问题             |
| ⬆️ (上升箭头)         | :arrow_up:                  | 升级依赖                     |
| ⬇️ (下降箭头)         | :arrow_down:                | 降级依赖                     |
| 📌 (图钉)             | :pushpin:                   | 将依赖项固定到特定版本       |
| 📈 (上升趋势图)       | :chart_with_upwards_trend:  | 添加分析或跟踪代码           |
| ♻️ （回收）           | :recycle:                   | 重构代码                     |
| 🐳 (鲸鱼)             | :whale:                     | Docker 相关工作              |
| 🌐 (带子午线的地球仪) | :globe_with_meridians:      | 国际化与本地化               |
| ➕ (加号)             | :heavy_plus_sign:           | 增加一个依赖                 |
| ➖ (减号)             | :heavy_minus_sign:          | 减少一个依赖                 |
| 🔧 (扳手)             | :wrench:                    | 修改配置文件                 |
| 🔨 (锤子)             | :hammer:                    | 重大重构                     |
| ✏️ (铅笔)             | :pencil2:                   | 修复 typo                    |
| 💩 (粑粑…)            | :poop:                      | 写了辣鸡代码需要优化         |
| ⏪ (倒带)             | :rewind:                    | 恢复更改                     |
| 🔀 (交叉向右的箭头)   | :twisted_rightwards_arrows: | 合并分支                     |
| 📦 (包裹)             | :package:                   | 更新编译的文件或包           |
| 👽 (外星人)           | :alien:                     | 由于外部API更改而更新代码    |
| 🚚 (货车)             | :truck:                     | 移动或者重命名文件           |
| 📄 (正面朝上的页面)   | :page_facing_up:            | 增加或更新许可证书           |
| 💥 (爆炸)             | :boom:                      | 引入突破性的变化             |
| 🍱 (铅笔)             | :bento:                     | 增加或更新资源               |
| 👌 (OK手势)           | :ok_hand:                   | 由于代码审查更改而更新代码   |
| ♿️ (轮椅)             | :wheelchair:                | 改善无障碍交互               |
| 💡 (灯泡)             | :bulb:                      | 给代码添加注释               |
| 🍻 (啤酒)             | :beers:                     | 醉醺醺地写代码…              |
| 💬 (消息气泡)         | :speech_balloon:            | 更新文本文档                 |
| 🗃 (卡片文件盒)       | :card_file_box:             | 执行与数据库相关的更改       |
| 🔊 (音量大)           | :loud_sound:                | 增加日志                     |
| 🔇 (静音)             | :mute:                      | 移除日志                     |
| 👥 (轮廓中的半身像)   | :busts_in_silhouette:       | 增加贡献者                   |
| 🚸 (孩童通行)         | :children_crossing:         | 优化用户体验、可用性         |
| 🏗 (建筑建造)         | :building_construction:     | 结构变动                     |
| 📱 (iPhone)           | :iphone:                    | 做响应式设计                 |
| 🤡 (小丑脸)           | :clown_face:                | 嘲弄事物（直译，这个没明白） |
| 🥚 (鸡蛋)             | :egg:                       | 增加彩蛋                     |
| 🙈 (看不见邪恶)       | :see_no_evil:               | 增加或更改gitignore          |
| 📸 (照相机闪光灯)     | :camera_flash:              | 增加或更新截图               |
| ⚗️ (蒸馏器)           | :alembic:                   | 尝试新东西                   |
| 🔍 (放大镜)           | :mag:                       | SEO优化                      |
| ☸️ (船的方向盘)       | :wheel_of_dharma:           | 关于Kubernetes的工作         |
| 🏷 (标签)             | :label:                     | 增加类型（FLow、Type）       |



## 6. 强制使用 pnpm 包管理器工具

团队开发项目的时候，需要统一包管理器工具,因为不同包管理器工具下载同一个依赖,可能版本不一样,

导致项目出现 bug 问题,因此包管理器工具需要统一管理！！！

在根目录创建`scritps/preinstall.js`文件，添加下面的内容：

```js
if (!/pnpm/.test(process.env.npm_execpath || '')) {
  console.warn(
    `\u001b[33mThis repository must using pnpm as the package manager ` +
      ` for scripts to work properly.\u001b[39m\n`
  )
  process.exit(1)
}
```

配置命令

```json
"scripts": {
	"preinstall": "node ./scripts/preinstall.js"
}
```

**当我们使用 npm 或者 yarn 来安装包的时候，就会报错了。原理就是在 install 的时候会触发 preinstall（npm 提供的生命周期钩子）这个文件里面的代码。**



# 三、项目集成

## 1. 集成 element-plus

官网地址:https://element-plus.gitee.io/zh-CN/

```shell
pnpm install element-plus @element-plus/icons-vue
```

**入口文件 main.ts 全局安装 element-plus,element-plus 默认支持语言英语设置为中文**：

```js
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
//@ts-ignore忽略当前文件ts类型的检测否则有红色提示(打包会失败)
import zhCn from 'element-plus/dist/locale/zh-cn.mjs'
app.use(ElementPlus, {
  locale: zhCn,
})
```

**Element Plus 全局组件类型声明**：Volar

```json
// tsconfig.json
{
  "compilerOptions": {
    "types": ["element-plus/global"]
  }
}
```

配置完毕可以测试 element-plus 组件与图标的使用.



## 2. src 别名的配置

在开发项目的时候文件与文件关系可能很复杂，因此我们需要给 src 文件夹配置一个别名！！！

```ts
// vite.config.ts
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import path from 'path'
export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: {
      '@': path.resolve('./src'), // 相对路径别名配置，使用 @ 代替 src
    },
  },
})
```

**TypeScript 编译配置**

```json
// tsconfig.json
{
  "compilerOptions": {
    "baseUrl": "./", // 解析非相对模块的基地址，默认是当前目录
    "paths": {
      //路径映射，相对于baseUrl
      "@/*": ["src/*"]
    }
  }
}
```



## 3. 环境变量的配置

**项目开发过程中，至少会经历开发环境、测试环境和生产环境(即正式环境)三个阶段。不同阶段请求的状态(如接口地址等)不尽相同，若手动切换接口地址是相当繁琐且易出错的。于是环境变量配置的需求就应运而生，我们只需做简单的配置，把环境状态切换的工作交给代码。**

**开发环境（development）**
顾名思义，开发使用的环境，每位开发人员在自己的 dev 分支上干活，开发到一定程度，同事会合并代码，进行联调。

**测试环境（testing）**
测试同事干活的环境啦，一般会由测试同事自己来部署，然后在此环境进行测试

**生产环境（production）**
生产环境是指正式提供对外服务的，一般会关掉错误报告，打开错误日志。(正式提供给客户使用的环境。)

**注意：**一般情况下，一个环境对应一台服务器,也有的公司开发与测试环境是一台服务器！！！



项目根目录分别添加开发、生产和测试环境的文件!

```
.env.development
.env.production
.env.test
```

**文件内容：**

```
# 变量必须以 VITE_ 为前缀才能暴露给外部读取
NODE_ENV = 'development'
VITE_APP_TITLE = '甄选运营平台'
VITE_APP_BASE_API = '/dev-api'
```

```
NODE_ENV = 'production'
VITE_APP_TITLE = '甄选运营平台'
VITE_APP_BASE_API = '/prod-api'
```

```
# 变量必须以 VITE_ 为前缀才能暴露给外部读取
NODE_ENV = 'test'
VITE_APP_TITLE = '甄选运营平台'
VITE_APP_BASE_API = '/test-api'
```

配置运行命令：package.json

```json
 "scripts": {
    "dev": "vite --open",
    "build:test": "vue-tsc && vite build --mode test",
    "build:pro": "vue-tsc && vite build --mode production",
    "preview": "vite preview"
  },
```

通过`import.meta.env`获取环境变量



## 4. SVG 图标配置

在开发项目的时候经常会用到 svg 矢量图,而且我们使用 SVG 以后，页面上加载的不再是图片资源,

这对页面性能来说是个很大的提升，而且我们 SVG 文件比 img 要小的很多，放在项目中几乎不占用资源。

**安装 SVG 依赖插件**：

```shell
pnpm install vite-plugin-svg-icons -D
```

**在`vite.config.ts`中配置插件**：

```ts
import { createSvgIconsPlugin } from 'vite-plugin-svg-icons'
import path from 'path'
export default () => {
  return {
    plugins: [
      createSvgIconsPlugin({
        // Specify the icon folder to be cached
        iconDirs: [path.resolve(process.cwd(), 'src/assets/icons')],
        // Specify symbolId format
        symbolId: 'icon-[dir]-[name]',
      }),
    ],
  }
}
```

**入口文件导入**：

```ts
import 'virtual:svg-icons-register'
```



## 5. svg 封装为全局组件

因为项目很多模块需要使用图标,因此把它封装为全局组件！！！

**在 src/components 目录下创建一个 SvgIcon 组件:代表如下**

```vue
<template>
  <div>
    <svg :style="{ width: width, height: height }">
      <use :xlink:href="prefix + name" :fill="color"></use>
    </svg>
  </div>
</template>

<script setup lang="ts">
defineProps({
  //xlink:href属性值的前缀
  prefix: {
    type: String,
    default: '#icon-',
  },
  //svg矢量图的名字
  name: String,
  //svg图标的颜色
  color: {
    type: String,
    default: '',
  },
  //svg宽度
  width: {
    type: String,
    default: '16px',
  },
  //svg高度
  height: {
    type: String,
    default: '16px',
  },
})
</script>
<style scoped></style>
```

在 src 文件夹目录下创建一个 index.ts 文件：用于注册 components 文件夹内部全部全局组件！！！

```ts
import SvgIcon from './SvgIcon/index.vue'
import type { App, Component } from 'vue'
const components: { [name: string]: Component } = { SvgIcon }
export default {
  install(app: App) {
    Object.keys(components).forEach((key: string) => {
      app.component(key, components[key])
    })
  },
}
```

在入口文件引入 src/index.ts 文件,通过 app.use 方法安装自定义插件

```ts
import gloablComponent from './components/index'
app.use(gloablComponent)
```



## 6. 集成 sass

我们目前在组件内部已经可以使用 scss 样式,因为在配置 styleLint 工具的时候，项目当中已经安装过 sass sass-loader,因此我们再组件内可以使用 scss 语法！！！需要加上 lang="scss"

```vue
<style scoped lang="scss"></style>
```

接下来我们为项目添加一些全局的样式

在 src/styles 目录下创建一个 index.scss 文件，当然项目中需要用到清除默认样式，因此在 index.scss 引入 reset.scss

```scss
@import reset.scss;
```

在入口文件引入

```scss
import '@/styles'
```

但是你会发现在 src/styles/index.scss 全局样式文件中没有办法使用$变量.因此需要给项目中引入全局变量$.

在 style/variable.scss 创建一个 variable.scss 文件

在 vite.config.ts 文件配置如下:

```ts
// 配置全局使用
export default defineConfig((config) => {
	css: {
      preprocessorOptions: {
        scss: {
          javascriptEnabled: true,
          additionalData: '@import "./src/styles/variable.scss";',
        },
      },
    },
	}
}
```

**`@import "./src/styles/variable.less";`后面的`;`不要忘记，不然会报错**!

配置完毕你会发现 scss 提供这些全局变量可以在组件样式中使用了！！！



## 7. mock 数据

安装依赖:https://www.npmjs.com/package/vite-plugin-mock

```shell
pnpm install -D vite-plugin-mock@2.9.6 mockjs
```

在 vite.config.js 配置文件启用插件:

```ts
import { UserConfigExport, ConfigEnv } from 'vite'
import { viteMockServe } from 'vite-plugin-mock'
import vue from '@vitejs/plugin-vue'
export default ({ command }) => {
  return {
    plugins: [
      vue(),
      viteMockServe({
        localEnabled: command === 'serve',
      }),
    ],
  }
}
```

在根目录创建 mock 文件夹:去创建我们需要 mock 数据与接口！！！

在 mock 文件夹内部创建一个 user.ts 文件

```ts
//用户信息数据：模拟数据
function createUserList() {
  return [
    {
      userId: 2,
      avatar:
        'https://wpimg.wallstcn.com/f778738c-e4f8-4870-b634-56703b4acafe.gif',
      username: 'system',
      password: '111111',
      desc: '系统管理员',
      roles: ['系统管理员'],
      buttons: ['cuser.detail', 'cuser.user'],
      routes: ['home'],
      token: 'System Token',
    },
  ]
}

export default [
  // 用户登录接口
  {
    url: '/api/user/login', //请求地址
    method: 'post', //请求方式
    response: ({ body }) => {
      //获取请求体携带过来的用户名与密码
      const { username, password } = body
      //调用获取用户信息函数,用于判断是否有此用户
      const checkUser = createUserList().find(
        (item) => item.username === username && item.password === password
      )
      //没有用户返回失败信息
      if (!checkUser) {
        return { code: 201, data: { message: '账号或者密码不正确' } }
      }
      //如果有返回成功信息
      const { token } = checkUser
      return { code: 200, data: { token } }
    },
  },
  // 获取用户信息
  {
    url: '/api/user/info',
    method: 'get',
    response: (request) => {
      //获取请求头携带token
      const token = request.headers.token
      //查看用户信息是否包含有次token用户
      const checkUser = createUserList().find((item) => item.token === token)
      //没有返回失败的信息
      if (!checkUser) {
        return { code: 201, data: { message: '获取用户信息失败' } }
      }
      //如果有返回成功信息
      return { code: 200, data: { checkUser } }
    },
  },
]
```

**安装 axios**

```
pnpm install axios
```

最后通过 axios 测试接口！！！



## 8. axios 二次封装

在开发项目的时候避免不了与后端进行交互,因此我们需要使用 axios 插件实现发送网络请求。在开发项目的时候

我们经常会把 axios 进行二次封装。

目的:

1:使用请求拦截器，可以在请求拦截器中处理一些业务(开始进度条、请求头携带公共参数)

2:使用响应拦截器，可以在响应拦截器中处理一些业务(进度条结束、简化服务器返回的数据、处理 http 网络错误)

在根目录下创建 utils/request.ts

```ts
import axios from 'axios'
import { ElMessage } from 'element-plus'
//创建axios实例
let request = axios.create({
  baseURL: import.meta.env.VITE_APP_BASE_API,
  timeout: 5000,
})
//请求拦截器
request.interceptors.request.use((config) => {
  return config
})
//响应拦截器
request.interceptors.response.use(
  (response) => {
    return response.data
  },
  (error) => {
    //处理网络错误
    let msg = ''
    let status = error.response.status
    switch (status) {
      case 401:
        msg = 'token过期'
        break
      case 403:
        msg = '无权访问'
        break
      case 404:
        msg = '请求地址错误'
        break
      case 500:
        msg = '服务器出现问题'
        break
      default:
        msg = '无网络'
    }
    ElMessage({
      type: 'error',
      message: msg,
    })
    return Promise.reject(error)
  }
)
export default request
```



## 9. API 接口统一管理

在开发项目的时候,接口可能很多需要统一管理。在 src 目录下去创建 api 文件夹去统一管理项目的接口；

- index.ts 主要为暴露定义过请求参数**类型**的方法，这样调用接口传参时就能限制个数与类型
- type.ts 主要定义这个接口参数的具体类型，如登录接口需携带 string 类型的 username、password

比如下面方式：

```ts
// src/api/user/index.ts
// 统一管理用户相关接口
import request from '@/utils/request'
import type { loginFrom, loginResponseData } from './type'
/* 统一管理接口 */
enum API {
  LOGIN_URL = '/user/login',
  USERINFO_URL = '/user/info',
}

/* 暴露请求函数 */

//登录接口方法
export const reqLogin = (data: loginFrom) =>
  request.post<any, loginResponseData>(API.LOGIN_URL, data)

//获取用户信息接口方法
export const reqUserInfo = () => request.get(API.USERINFO_URL)
```

```ts
// src/api/user/type.ts

// 登录接口需要携带参数类型
export interface loginFrom {
  username: string
  password: string
}

export interface dataType {
  token: string
}
// 登录接口返回类型
export interface loginResponseData {
  code: number
  data: dataType //返回值为{ code: 200, data: { token } }
}

export interface user {
  token: string
}
// 服务器返回用户信息相关的数据类型
export interface userResponseData {
  code: number
  data: dataType //返回值为{ code: 200, data: { token } }
}
```





# 四、其他



## 1. 按钮权限-自定义指令

在项目中通常会设计路由权限问题，如每个账号不拥有此按钮的权限，此时就不应该展示此按钮，这是可以使用自定义指令执行操作

**思路：**首先在仓库中获取用户信息时保存用户按钮权限的数组并在这里引入，页面使用自定义指令时会执行函数判断是否包含按钮传入的字段，不包含就移除此按钮



**在src下创建directive/has.ts：**

```ts
import pinia from '@/store'
import useUserStore from '@/store/modules/user'
let UserStore = useUserStore(pinia) // 组件之外使用需传入

export const isHasButton = (app: any) => {
    app.directive('has', {
        // dom挂载完毕执行一次
        mounted(el: any, options: any) {
            if (!UserStore.buttons.includes(options.value)) {
                // 从dom树去除
                el.parentNode.removeChild(el)
            }
        },
    })
}

```



**在main.ts中配置传入app：**

```ts
// 自定义指令
import { isHasButton } from '@/directive/has'
isHasButton(app)
```



**使用：**

```vue
<el-button v-has="`btn.Role.update`">
```





## 2. 路由权限

在项目中每个账号的权限是不一样的，如A账号可展示所有路由，B没有某些路由权限，此时需要将路由分割

- constantRoute-常量路由：每个人都有的如`/login`、`/`、`/404`
- asyncRoute-异步路由：不同人不同的菜单
- anyRoute-任意路由：没有定义的路由，重定向404



**main.ts配置：**

```ts
// 路由配置
import router from './router'
app.use(router)
```



**在`src/router/routers.ts`中将路由分割：**

```ts
// 常量路由：每个人都有
export const constantRoute = [
    {
        path: '/login',
        component: () => import('@/views/login/index.vue'),
        name: 'login', // 命名路由
        meta: {
            title: '登录',
            hidden: true, // 是否隐藏
        },
    },
    {
        path: '/',
        component: () => import('@/layout/index.vue'),
        name: 'layout',
        meta: {
            title: '',
            hidden: false,
            icon: '',
        },
        redirect: '/home',
        children: [
            {
                path: '/home',
                component: () => import('@/views/home/index.vue'),
                meta: {
                    title: '首页',
                    hidden: false,
                    icon: 'HomeFilled',
                },
            },
        ],
    },
    {
        path: '/404',
        component: () => import('@/views/404/index.vue'),
        name: '404',
        meta: {
            title: '404',
            hidden: true,
        },
    },
]

// 异步路由：不同人不同的菜单
export const asyncRoute = [
    {
        path: '/acl',
        component: () => import('@/layout/index.vue'),
        name: 'Acl',
        meta: {
            title: '权限管理',
            hidden: false,
            icon: 'Lock',
        },
        redirect: '/acl/user',
        children: [
            {
                path: '/acl/user',
                component: () => import('@/views/acl/user/index.vue'),
                name: 'User',
                meta: {
                    title: '用户管理',
                    hidden: false,
                    icon: 'User',
                },
            },
        ],
    },
]

// 任意路由
export const anyRoute = [
    {
        path: '/:pathMatch(.*)*',
        redirect: '/404',
        name: 'Any',
        meta: {
            title: '任意',
            hidden: true,
        },
    },
]

```



**在`src/router/index.ts`中配置：**

```ts
import { createRouter, createWebHashHistory } from 'vue-router'
import { constantRoute } from './routers'

let router = createRouter({
    history: createWebHashHistory(),
    routes: constantRoute, // 注意此时只注册了静态路由：每个人都有的
    // 滚动行为
    scrollBehavior() {
        return {
            left: 0,
            top: 0,
        }
    },
})

export default router

```



**再需要配置路由的地方如`store/user.ts`仓库中：**



1. 首先先将在`src/router/routers.ts`中已分割的路由引入到仓库：

```ts
import { constantRoute, asyncRoute, anyRoute } from '@/router/routers'
```

2. 创建过滤路由的函数：

```ts
function filterAsyncRoute(asyncRoute: any, routers: any) {
    return asyncRoute.filter((item: any) => {
        if (routers.includes(item.name)) {
            // routers: ['aaa', 'User', 'Category','Sku']
            if (item.children && item.children.length > 0) {
                item.children = filterAsyncRoute(item.children, routers)
            }
            return true
        }
    })
}
```

3. 在仓库中声明一个存储要生成菜单的路由数组`menuRoutes`

4. 在登录成功后获取用户信息时调用以上方法：传入所有的`asyncRoute`和自己的`result.routes`。避免路由出现路由登录后越来越少的情况，引入深拷贝方法调用

```ts
// 引入深拷贝方法
import { cloneDeep } from 'lodash'

// 计算当前用户的异步路由
let userAsyncRoute = filterAsyncRoute(cloneDeep(asyncRoute),res.data.routes,)
```

5. 将所有路由解构存放数组中

```ts
this.menuRoutes = [...constantRoute,...userAsyncRoute,...anyRoute,]
```

6. 将路由追加：

```ts
this.menuRoutes.forEach((route: any) => {
         router.addRoute(route)
})
```



7. 此时可能出现另一个问题：登录成功后本地有用户信息，页面刷新直接next()，如果页面没有用户信息或者页面重新刷新pinia仓库数据丢失，需要重新获取用户信息，但刷新的路由是异步路由，但是还没有加载完毕，页面出现白屏，可如下配置next()

```ts
next({...to})
```



## 3. 登录携带token的路由守卫配置

处理不需要携带token的路由之外，其他的路由需要携带token才能进行下一步操作



`src/permission.ts`：专门配置路由守卫

```ts
// 路由鉴权
import router from '@/router'
import pinia from './store'
import useUserStore from './store/modules/user'
let UserStore = useUserStore(pinia)

// 全局前置守卫
router.beforeEach(async (to, _from, next) => {
    nprogress.start()
    if (UserStore.token) {
        // 已登录
        if (to.path == '/login') {
            next({ path: '/' })
        } else {
            if (UserStore.username) {
                next()
            } else {
                /*  如页面刷新仓库没有了所有数据包括用户信息，需要重获用户信息，而仓库的token没了会获取localStorage的token
                    此时请求携带此token如果有问题如过期，篡改获取用户信息会err，则执行重新登录的页面跳转
              */
                await UserStore.userInfo().then(
                    () => {
                        // 刷新的时候异步路由没有加载完毕，出现白屏
                        next({ ...to, replace: true })
                    },
                    async (err) => {
                        await UserStore.userLogout()
                        console.log(err) // 服务器报服务异常
                        next({ path: '/login' })
                    },
                )
            }
        }
    } else {
        // 用户未登录
        if (to.path == '/login') {
            next()
        } else {
            next({ path: '/login' })
        }
    }
})
// 全局后置守卫
router.afterEach((to, _from, _next) => {
})

```



**在mian.ts中引入：**

```ts
// 路由鉴权
import '@/permission'
```





**axios的请求拦截器配置：**

```ts
request.interceptors.request.use((config) => {
    // 携带token
    let UserStore = useUserStore()
    if (UserStore.token) {
        config.headers.token = UserStore.token
    }
    return config
})
```



## 4. pina仓库

Pinia是vue生态里Vuex的替代者，一个全新的vue状态管理库。在Vue3成为正式版以后，尤雨溪强势推荐的项目就是Pinia。



**安装：**

```shell
npm install pinia
```



**main.ts中配置：**

```ts
// pinia仓库配置
import pinia from './store'
app.use(pinia)
```



**创建大仓库：`src/store/index.ts`**

```ts
import { createPinia } from 'pinia'

// 创建大仓库
let pinia = createPinia()

export default pinia
```



**创建定义具体业务小仓库：`src/store/modules/user.ts`**

- defineStore( ) 方法的第一个参数：相当于为容器起一个名字。注意：这里的名字必须唯一，不能重复。
- defineStore( ) 方法的第二个参数：可以简单理解为一个配置对象，里边是对容器仓库的配置说明。当然这种说明是以对象的形式。
- state 属性： 用来存储数据的
- getters属性： 用来监视或者说是计算状态的变化的，有缓存的功能。
- actions属性： 对state里数据变化的业务逻辑，需求不同，编写逻辑不同。说白了就是修改state全局状态数据的。编写函数

```ts
import { defineStore} from 'pinia'

export const useUserStore = defineStore('User',{
  state:()=>{
    return {
        title: '',
    }
  },
    // 相当于methods
  actions:{
     test() {
          this.title = '标题'
          console.log(this.title)
      },
  }
    // 相当于computed
  getters:{},
})

export default useUserStore
```



**页面使用：**

```ts
import useUserStore from '@/store/modules/user'

let UserStore = useUserStore()
UserStore.test()
```



在实际开发中可能需要定义仓库中存储数据的ts类型，则创建文件定义：`src/store/modules/types/type.ts`



**state批量修改值：**

```ts
let Test = useUserStore()
Test.$patch({
	age:18,
	name:'asd'
})

// 函数式写法
Test.$patch((state)=>{
    state.age=18
})
```





**pinia解构响应式：**

```ts
let Test = useUserStore()
const {age}=Test

pinia提供了方法：
import {storeToRefs} from 'pinia'
const {age}=storeToRefs(Test)
```





**$reset**：
重置store到他的初始状态

```ts
state: () => ({
     user: <Result>{},
     name: "default",
     current:1
}),
```

Vue 例如我把值改变到了10

```ts
const change = () => {
     Test.current++
}
```

调用$reset();

将会把state所有值 重置回 原始状态


**订阅state的改变：**

类似于Vuex 的abscribe 只要有state 的变化就会走这个函数

```typescript
Test.$subscribe((args,state)=>{
   console.log(args,state);

})
```

如果你的组件卸载之后还想继续调用请设置第二个参数

```ts
Test.$subscribe((args,state)=>{
   console.log(args,state);
},{
  detached:true
})
```



**订阅Actions的调用：**
 只要有actions被调用就会走这个函数

```
Test.$onAction((args)=>{
   console.log(args);
})
```

