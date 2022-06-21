> 哈喽,大家好 我是`xy`👨🏻‍💻。 从我最初接触`vue3`版本到现在已经有一年的时间。由于 vue3.2 版本的发布，`<script setup>` 的实验性标志已经去掉，已经陆陆续续有不少公司开始使用 `vue3.2`开发项目了。这篇文章就来帮助大家如何快速使用 `vue3.x`，`typeScript`， `vite` 搭建一套企业级的开发脚手架 🤖。废话不多说，直接上手开搞 💪

## 搭建前准备

1. `Vscode`: 前端人必备写码神器
2. `Chrome`：对开发者非常友好的浏览器(反正我是很依赖它的)
3. `Nodejs`&`npm`：配置本地开发环境，安装 Node 后你会发现 npm 也会一起安装下来
4. `Vue.js devtools`：浏览器调试插件
5. `Vue Language Features (Volar)`：Vscode 开发 vue3 必备插件，提供语法高亮提示，非常好用
6. `Vue 3 Snippets`：vue3 快捷输入

> 由于`Vue.js devtools` 需要到谷歌扩展商店才能下载,贴心 ❤️ 的`xy`已经为大家准备好了`crx`文件了,公众号回复:【`VueDevTools`】可自动获取哦 💪

## Vue2 与 Vue3 的区别

`Vue3`由于完全由`TS`进行重写，在应用中对类型判断的定义和使用有很强的表现。同一对象的多个键返回值必须通过定义对应的接口（`interface`）来进行类型定义。要不然在 ESLint 时都会报错。

`vue2` 的双向数据绑定是利用 `ES5` 的一个 `API Object.definePropert()`对数据进行劫持 结合 `发布订阅`模式的方式来实现的。`Vue3` 中使用了 `es6` 的 `ProxyAPI` 对数据代理。

`Vue3`支持碎片(`Fragments`)

Vue2 与 Vue3 最大的区别: Vue2 使用`Options API`而 Vue3 使用的`Composition API`

生命周期钩子变化:

```js
Vue2 ~~~~~~~~~~~ vue3
beforeCreate  -> setup()
created       -> setup()
beforeMount   -> onBeforeMount
mounted       -> onMounted
beforeUpdate  -> onBeforeUpdate
updated       -> onUpdated
beforeDestroy -> onBeforeUnmount
destroyed     -> onUnmounted
activated     -> onActivated
deactivated   -> onDeactivated
```

## 介绍 vite

> Vite：下一代前端开发与构建工具

- 💡 极速的开发服务器启动
- ⚡️ 轻量快速的热模块重载（HMR）
- 🛠️ 丰富的功能
- 📦 自带优化的构建
- 🔩 通用的插件接口
- 🔑 完全类型化的 API

`Vite` （法语意为 “迅速”，发音 /vit/）是一种全新的前端构建工具，它极大地改善了前端开发体验。

它主要由两部分组成：

- 一个开发服务器，它基于 原生 `ES` 模块 提供了 丰富的内建功能，如速度快到惊人的 模块热更新（HMR）。

- 一套构建指令，它使用 `Rollup` 打包你的代码，并且它是预配置的，可以输出用于生产环境的优化过的静态资源。

- Vite 意在提供开箱即用的配置，同时它的 插件 API 和 JavaScript API 带来了高度的`可扩展性`，并有完整的类型支持。

## 使用 vite 快速创建脚手架

> 兼容性注意:Vite 需要 `Node.js` 版本 `>= 12.0.0`。

1. 第一步: 在需要创建项目文件目录下打开 `cmd` 运行以下命令

```bash
# npm 6.x
npm init @vitejs/app vite_vue3_ts --template

# npm 7+, 需要额外的双横线：
npm init @vitejs/app vite_vue3_ts -- --template

# yarn
yarn create @vitejs/app vite_vue3_ts --template
```

这里我采用 `yarn` 来安装

![](https://files.mdnice.com/user/16854/befdd482-25e0-43f9-a5e3-7b34a9d8696c.png)

2. 第二步: 选择 `vue`回车 => `vue-ts`回车

![](https://files.mdnice.com/user/16854/0280afe9-2ba2-4dce-bdc4-6b756151fd5a.png)
![](https://files.mdnice.com/user/16854/d1a58b76-2bc7-489b-966c-fb2a4136e39a.png)

3. 第三步: `cd` 到项目文件夹,安装依赖,启动项目

```bash
# 进入项目文件夹
cd vite_vue3_ts
# 安装依赖
yarn
# 启动
yarn dev
```

![](https://files.mdnice.com/user/16854/64867857-9e79-426a-89e3-c92303934094.png)

## 约束代码风格

### Eslint 支持

```bash
# eslint 安装
yarn add eslint --dev
# eslint 插件安装
yarn add eslint-plugin-vue --dev

yarn add @typescript-eslint/eslint-plugin --dev

yarn add eslint-plugin-prettier --dev

# typescript parser
yarn add @typescript-eslint/parser --dev
```

注意: 如果 `eslint` 安装报错:

![](https://files.mdnice.com/user/16854/98ff3635-d460-4a8f-b3d3-2597a03e56c0.png)

可以尝试运行以下命令:

```bash
yarn config set ignore-engines true
```

运行成功后再次执行 `eslint` 安装命令

### 项目下新建 .eslintrc.js

> 配置 `eslint` 校验规则:

```js
module.exports = {
  root: true,
  env: {
    browser: true,
    node: true,
    es2021: true,
  },
  parser: 'vue-eslint-parser',
  extends: [
    'eslint:recommended',
    'plugin:vue/vue3-recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:prettier/recommended',
    // eslint-config-prettier 的缩写
    'prettier',
  ],
  parserOptions: {
    ecmaVersion: 12,
    parser: '@typescript-eslint/parser',
    sourceType: 'module',
    ecmaFeatures: {
      jsx: true,
    },
  },
  // eslint-plugin-vue @typescript-eslint/eslint-plugin eslint-plugin-prettier的缩写
  plugins: ['vue', '@typescript-eslint', 'prettier'],
  rules: {
    '@typescript-eslint/ban-ts-ignore': 'off',
    '@typescript-eslint/no-unused-vars': 'off',
    '@typescript-eslint/explicit-function-return-type': 'off',
    '@typescript-eslint/no-explicit-any': 'off',
    '@typescript-eslint/no-var-requires': 'off',
    '@typescript-eslint/no-empty-function': 'off',
    '@typescript-eslint/no-use-before-define': 'off',
    '@typescript-eslint/ban-ts-comment': 'off',
    '@typescript-eslint/ban-types': 'off',
    '@typescript-eslint/no-non-null-assertion': 'off',
    '@typescript-eslint/explicit-module-boundary-types': 'off',
    'no-var': 'error',
    'prettier/prettier': 'error',
    // 禁止出现console
    'no-console': 'warn',
    // 禁用debugger
    'no-debugger': 'warn',
    // 禁止出现重复的 case 标签
    'no-duplicate-case': 'warn',
    // 禁止出现空语句块
    'no-empty': 'warn',
    // 禁止不必要的括号
    'no-extra-parens': 'off',
    // 禁止对 function 声明重新赋值
    'no-func-assign': 'warn',
    // 禁止在 return、throw、continue 和 break 语句之后出现不可达代码
    'no-unreachable': 'warn',
    // 强制所有控制语句使用一致的括号风格
    curly: 'warn',
    // 要求 switch 语句中有 default 分支
    'default-case': 'warn',
    // 强制尽可能地使用点号
    'dot-notation': 'warn',
    // 要求使用 === 和 !==
    eqeqeq: 'warn',
    // 禁止 if 语句中 return 语句之后有 else 块
    'no-else-return': 'warn',
    // 禁止出现空函数
    'no-empty-function': 'warn',
    // 禁用不必要的嵌套块
    'no-lone-blocks': 'warn',
    // 禁止使用多个空格
    'no-multi-spaces': 'warn',
    // 禁止多次声明同一变量
    'no-redeclare': 'warn',
    // 禁止在 return 语句中使用赋值语句
    'no-return-assign': 'warn',
    // 禁用不必要的 return await
    'no-return-await': 'warn',
    // 禁止自我赋值
    'no-self-assign': 'warn',
    // 禁止自身比较
    'no-self-compare': 'warn',
    // 禁止不必要的 catch 子句
    'no-useless-catch': 'warn',
    // 禁止多余的 return 语句
    'no-useless-return': 'warn',
    // 禁止变量声明与外层作用域的变量同名
    'no-shadow': 'off',
    // 允许delete变量
    'no-delete-var': 'off',
    // 强制数组方括号中使用一致的空格
    'array-bracket-spacing': 'warn',
    // 强制在代码块中使用一致的大括号风格
    'brace-style': 'warn',
    // 强制使用骆驼拼写法命名约定
    camelcase: 'warn',
    // 强制使用一致的缩进
    indent: 'off',
    // 强制在 JSX 属性中一致地使用双引号或单引号
    // 'jsx-quotes': 'warn',
    // 强制可嵌套的块的最大深度4
    'max-depth': 'warn',
    // 强制最大行数 300
    // "max-lines": ["warn", { "max": 1200 }],
    // 强制函数最大代码行数 50
    // 'max-lines-per-function': ['warn', { max: 70 }],
    // 强制函数块最多允许的的语句数量20
    'max-statements': ['warn', 100],
    // 强制回调函数最大嵌套深度
    'max-nested-callbacks': ['warn', 3],
    // 强制函数定义中最多允许的参数数量
    'max-params': ['warn', 3],
    // 强制每一行中所允许的最大语句数量
    'max-statements-per-line': ['warn', { max: 1 }],
    // 要求方法链中每个调用都有一个换行符
    'newline-per-chained-call': ['warn', { ignoreChainWithDepth: 3 }],
    // 禁止 if 作为唯一的语句出现在 else 语句中
    'no-lonely-if': 'warn',
    // 禁止空格和 tab 的混合缩进
    'no-mixed-spaces-and-tabs': 'warn',
    // 禁止出现多行空行
    'no-multiple-empty-lines': 'warn',
    // 禁止出现;
    semi: ['warn', 'never'],
    // 强制在块之前使用一致的空格
    'space-before-blocks': 'warn',
    // 强制在 function的左括号之前使用一致的空格
    // 'space-before-function-paren': ['warn', 'never'],
    // 强制在圆括号内使用一致的空格
    'space-in-parens': 'warn',
    // 要求操作符周围有空格
    'space-infix-ops': 'warn',
    // 强制在一元操作符前后使用一致的空格
    'space-unary-ops': 'warn',
    // 强制在注释中 // 或 /* 使用一致的空格
    // "spaced-comment": "warn",
    // 强制在 switch 的冒号左右有空格
    'switch-colon-spacing': 'warn',
    // 强制箭头函数的箭头前后使用一致的空格
    'arrow-spacing': 'warn',
    'no-var': 'warn',
    'prefer-const': 'warn',
    'prefer-rest-params': 'warn',
    'no-useless-escape': 'warn',
    'no-irregular-whitespace': 'warn',
    'no-prototype-builtins': 'warn',
    'no-fallthrough': 'warn',
    'no-extra-boolean-cast': 'warn',
    'no-case-declarations': 'warn',
    'no-async-promise-executor': 'warn',
  },
  globals: {
    defineProps: 'readonly',
    defineEmits: 'readonly',
    defineExpose: 'readonly',
    withDefaults: 'readonly',
  },
}

```

### 项目下新建 .eslintignore

```bash
# eslint 忽略检查 (根据项目需要自行添加)
node_modules
dist
```

### prettier 支持

```bash
# 安装 prettier
yarn add prettier --dev
```

### 解决 eslint 和 prettier 冲突

> 解决 `ESLint` 中的样式规范和 `prettier` 中样式规范的`冲突`，以 `prettier` 的样式规范`为准`，使 ESLint 中的样式规范自动失效

```bash
# 安装插件 eslint-config-prettier
yarn add eslint-config-prettier --dev
```

### 项目下新建 .prettier.js

> 配置 `prettier` 格式化规则:

```js
module.exports = {
  tabWidth: 2,
  jsxSingleQuote: true,
  jsxBracketSameLine: true,
  printWidth: 100,
  singleQuote: true,
  semi: false,
  overrides: [
    {
      files: '*.json',
      options: {
        printWidth: 200,
      },
    },
  ],
  arrowParens: 'always',
}
```

### 项目下新建 .prettierignore

```bash
# 忽略格式化文件 (根据项目需要自行添加)
node_modules
dist
```

### package.json 配置:

```json
{
  "script": {
    "lint": "eslint src --fix --ext .ts,.tsx,.vue,.js,.jsx",
    "prettier": "prettier --write ."
  }
}
```

上面配置完成后,可以运行以下`命令`测试下代码检查个`格式化`效果:

```bash
# eslint 检查
yarn lint
# prettier 自动格式化
yarn prettier
```

### 配置 husky + lint-staged

> 使用`husky` + `lint-staged`助力团队编码规范, husky&lint-staged 安装推荐使用 `mrm`, 它将根据 `package.json` 依赖项中的代码质量工具来安装和配置 husky 和 lint-staged，因此请确保在此之前安装并配置所有代码质量工具，如 `Prettier 和 ESlint`

### 首先安装 mrm

```bash
npm i mrm -D --registry=https://registry.npm.taobao.org
```

`husky` 是一个为 git 客户端增加 `hook` 的工具。安装后，它会自动在仓库中的 `.git/` 目录下增加相应的钩子；比如 `pre-commit` 钩子就会在你执行 `git commit` 的触发。

那么我们可以在 `pre-commit` 中实现一些比如 `lint 检查`、`单元测试`、`代码美化`等操作。当然，`pre-commit` 阶段执行的命令当然要保证其速度不要太慢，每次 commit 都等很久也不是什么好的体验。

`lint-staged`，一个仅仅过滤出 Git 代码暂存区文件(被 `git add` 的文件)的工具；这个很实用，因为我们如果对整个项目的代码做一个检查，可能耗时很长，如果是老项目，要对之前的代码做一个代码规范检查并修改的话，这可能就麻烦了呀，可能导致项目改动很大。

所以这个 `lint-staged`，对团队项目和开源项目来说，是一个很好的工具，它是对个人要提交的代码的一个规范和约束

### 安装 lint-staged

> `mrm` 安装 `lint-staged` 会`自动`把 `husky` 一起安装下来

```bash
npx mrm lint-staged
```

安装成功后会发现 `package.json` 中多了一下几个配置:

![](https://files.mdnice.com/user/16854/1e23c422-c2e4-4478-ae17-6c954382c935.png)

因为我们要结合 `prettier` 代码格式化,所有修改一下配置:

```json
"husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "*.{js,jsx,vue,ts,tsx}": [
      "yarn lint",
      "prettier --write",
      "git add"
    ]
  }
```

好了,到这里代码格式化配置基本大功告成了!!!

可以修改部分代码尝试 `git commit` ,你会发现代码将自动格式化:

提交前的代码(发现编辑器`爆红`了):

![](https://files.mdnice.com/user/16854/bb28c3a6-4751-459a-a87d-c4191f758e6b.png)

执行 `commit` 操作,控制台可以看到走了哪些流程:

![](https://files.mdnice.com/user/16854/82a2612e-44d6-4015-acef-62606b1a23ce.png)

`commit` 后的代码,是不是已经被格式化了

![](https://files.mdnice.com/user/16854/4abce158-2d3f-43e8-854a-70536c89d116.png)

### 配置文件引用别名 alias

> 直接修改 `vite.config.ts` 文件配置:

```js
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import path from 'path'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, 'src'),
    },
  },
})
```

> 修改 `tsconfig.json`

```json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "esnext",
    "moduleResolution": "node",
    "strict": true,
    "jsx": "preserve",
    "sourceMap": true,
    "resolveJsonModule": true,
    "esModuleInterop": true,
    "lib": ["esnext", "dom"],
    "baseUrl": ".",
    "paths": {
      "@/*":["src/*"]
    }
  },
  "include": ["src/**/*.ts", "src/**/*.d.ts", "src/**/*.tsx", "src/**/*.vue"]
}

```

## 配置 css 预处理器 scss

> 虽然 `vite` 原生支持 `less/sass/scss/stylus`，但是你必须手动安装他们的预处理器依赖

### 安装

```bash
yarn ass sass-loader --dev
yarn add dart-sass --dev
yarn add sass --dev
```

### 配置全局 scss 样式文件

在 `src/assets` 下新增 `style` 文件夹，用于存放全局样式文件

新建 `main.scss`, 设置一个用于测试的颜色`变量` :

```scss
$test-color: red;
```

如何将这个全局样式文件`全局注入`到项目中呢？配置 `Vite` 即可：

```js
css:{
    preprocessorOptions:{
      scss:{
        additionalData:'@import "@/assets/style/main.scss";'
      }
    }
  },
```

### 组件中使用

> 不需要任何引入可以直接使用全局`scss`定义的变量

```scss
.test{
  color: $test-color;
}
```
## 路由

```bash
# 安装路由
yarn add vue-router@4
```

在 `src` 文件下新增 `router` 文件夹 => `router.ts` 文件,内容如下:

```js
import { createRouter, createWebHistory, RouteRecordRaw } from 'vue-router'

const routes: RouteRecordRaw[] = [
  {
    path: '/',
    name: 'Login',
    component: () => import('@/pages/login/Login.vue'), // 注意这里要带上 文件后缀.vue
  },
]

const router = createRouter({
  history: createWebHistory(),
  routes,
})

export default router

```

修改入口文件 `main.ts` :

```js
import { createApp } from 'vue'
import App from './App.vue'
import router from './router/index'

const app = createApp(App)

app.use(router)

app.mount('#app')

```

到这里路由的基础配置已经完成了,更多配置信息可以查看 `vue-router` 官方文档:

> vue-router: `https://next.router.vuejs.org/zh/guide/`

`vue-router4.x` 支持 `typescript`，配置路由的类型是 `RouteRecordRaw`，这里 `meta` 可以让我们有更多的发挥空间，这里提供一些参考：

- `title`:`string`; 页面标题，通常必选。
- `icon?`:`string`; 图标，一般配合菜单使用。
- `auth?`:`boolean`; 是否需要登录权限。
- `ignoreAuth?`:`boolean`; 是否忽略权限。
- `roles?`:`RoleEnum[]`; 可以访问的角色
- `keepAlive?`:`boolean`; 是否开启页面缓存
- `hideMenu?`:`boolean`; 有些路由我们并不想在菜单中显示，比如某些编辑页面。
- `order?`:`number`; 菜单排序。
- `frameUrl?`:`string`; 嵌套外链。

> 这里只提供一些思路，每个项目涉及到的业务都会存在些差异，这里就不作详细讲解了，根据自己业务需求做配置即可。

## 统一请求封装

> 使用过 vue2.x 的同学应该对 axios 很熟悉了，这里我们直接使用 axios 做封装：

```bash
# 安装 axios
yarn add axios
# 安装 nprogress 用于请求 loading
# 也可以根据项目需求自定义其它 loading
yarn add nprogress
# 类型声明，或者添加一个包含 `declare module 'nprogress'
yarn add @types/nprogress --dev
```

实际使用中可以根据项目修改，比如`RESTful` `api`中可以自行添加`put`和`delete`请求,`ResType`也可以根据后端的通用返回值动态的去修改

新增 `service` 文件夹，`service` 下新增 `http.ts` 文件以及 `api` 文件夹:

![](https://files.mdnice.com/user/16854/7c0d7393-fd70-4bfb-aae8-e750e3463625.png)

`http.ts` : 用于`axios`封装

```js
//http.ts
import axios, { AxiosRequestConfig } from 'axios'
import NProgress from 'nprogress'

// 设置请求头和请求路径
axios.defaults.baseURL = '/api'
axios.defaults.timeout = 10000
axios.defaults.headers.post['Content-Type'] = 'application/json;charset=UTF-8'
axios.interceptors.request.use(
  (config): AxiosRequestConfig<any> => {
    const token = window.sessionStorage.getItem('token')
    if (token) {
      //@ts-ignore
      config.headers.token = token
    }
    return config
  },
  (error) => {
    return error
  }
)
// 响应拦截
axios.interceptors.response.use((res) => {
  if (res.data.code === 111) {
    sessionStorage.setItem('token', '')
    // token过期操作
  }
  return res
})

interface ResType<T> {
  code: number
  data?: T
  msg: string
  err?: string
}
interface Http {
  get<T>(url: string, params?: unknown): Promise<ResType<T>>
  post<T>(url: string, params?: unknown): Promise<ResType<T>>
  upload<T>(url: string, params: unknown): Promise<ResType<T>>
  download(url: string): void
}

const http: Http = {
  get(url, params) {
    return new Promise((resolve, reject) => {
      NProgress.start()
      axios
        .get(url, { params })
        .then((res) => {
          NProgress.done()
          resolve(res.data)
        })
        .catch((err) => {
          NProgress.done()
          reject(err.data)
        })
    })
  },
  post(url, params) {
    return new Promise((resolve, reject) => {
      NProgress.start()
      axios
        .post(url, JSON.stringify(params))
        .then((res) => {
          NProgress.done()
          resolve(res.data)
        })
        .catch((err) => {
          NProgress.done()
          reject(err.data)
        })
    })
  },
  upload(url, file) {
    return new Promise((resolve, reject) => {
      NProgress.start()
      axios
        .post(url, file, {
          headers: { 'Content-Type': 'multipart/form-data' },
        })
        .then((res) => {
          NProgress.done()
          resolve(res.data)
        })
        .catch((err) => {
          NProgress.done()
          reject(err.data)
        })
    })
  },
  download(url) {
    const iframe = document.createElement('iframe')
    iframe.style.display = 'none'
    iframe.src = url
    iframe.onload = function () {
      document.body.removeChild(iframe)
    }
    document.body.appendChild(iframe)
  },
}
export default http

```

`api` : 项目中接口做统一管理，按照模块来划分

在 `api` 文件下新增 `login` 文件夹,用于存放登录模块的请求接口,login 文件夹下分别新增 `login.ts` `types.ts` :

`login.ts`:

```js
import http from '@/service/http'
import * as T from './types'

const loginApi: T.ILoginApi = {
    login(params){
        return http.post('/login', params)
    }

}
export default loginApi
```

`types.ts`:

```ts
export interface ILoginParams {
    userName: string
    passWord: string | number
}
export interface ILoginApi {
    login: (params: ILoginParams)=> Promise<any>
}
```

至此,一个简单地请求封装完成了!!!!

除了自己手动封装 axios ,这里还推荐一个 vue3 的请求库: `VueRequest`,非常好用,下面来看看 `VueRequest`有哪些比较好用的功能吧!!!

- 🚀 所有数据都具有响应式
- 🔄 轮询请求
- 🤖 自动处理错误重试
- 🗄 内置请求缓存
- 💧 节流请求与防抖请求
- 🎯 聚焦页面时自动重新请求
- ⚙️ 强大的分页扩展以及加载更多扩展
- 📠 完全使用 Typescript 编写，具有强大的类型提示
- ⚡️ 兼容 Vite
- 🍃 轻量化
- 📦 开箱即用

![](https://files.mdnice.com/user/16854/c587ba05-5a22-4024-a831-6fecffee5d20.png)

是不是很强大 💪

> 官网链接: https://www.attojs.com/

## 状态管理 pinia

> 由于 vuex 4 对 typescript 的支持让人感到难过，所以状态管理弃用了 vuex 而采取了 pinia. pinia 的作者是 Vue 核心团队成员

尤大好像说 `pinia` 可能会代替 `vuex`，所以请放心使用。

### 安装 pinia

Pinia 与 Vuex 的区别：

- `id` 是必要的，它将所使用 store 连接到 devtools。
- 创建方式：`new Vuex.Store(...)`(vuex3)，`createStore(...)`(vuex4)。
- 对比于 vuex3 ，state 现在是一个`函数返回对象`。
- 没有 `mutations`，不用担心，state 的变化依然记录在 devtools 中。

```bash
# 安装
yarn add pinia@next
```

main.ts 中增加

```js
# 引入
import { createPinia } from "pinia"
# 创建根存储库并将其传递给应用程序
app.use(createPinia())
```

在 `src` 文件夹下新增 `store` 文件夹,接在在 store 中新增 `main.ts`

### 创建 `store`, main.ts :

```js
import { defineStore } from 'pinia'

export const useMainStore = defineStore({
  id: 'main',
  state: () =>({
    name: '超级管理员'
  })
})
```

组建中获取 store :

```js
<template>
  <div>{{mainStore.name}}</div>
</template>

<script setup lang="ts">
import { useMainStore } from "@/store/main"

const mainStore = useMainStore()

</script>
```

### getters 用法介绍

> Pinia 中的 getter 与 Vuex 中的 getter 、组件中的计算属性具有相同的功能

`store` => `main.ts`

```js
import { defineStore } from 'pinia'

export const useMainStore = defineStore({
  id: 'main',
  state: () => ({
    name: '超级管理员',
  }),
  // getters
  getters: {
    nameLength: (state) => state.name.length,
  }
})
```

组件中使用:

```js
<template>
  <div>用户名:{{ mainStore.name }}<br />长度:{{ mainStore.nameLength }}</div>
  <hr/>
  <button @click="updateName">修改store中的name</button>
</template>

<script setup lang="ts">
import { useMainStore } from '@/store/main'

const mainStore = useMainStore()

const updateName = ()=>{
  // $patch 修改 store 中的数据
  mainStore.$patch({
    name: '名称被修改了,nameLength也随之改变了'
  })
}
</script>
```

![](https://files.mdnice.com/user/16854/ab70ded8-aa34-456a-9044-ac560ff5d2d4.gif)

### actions

> 这里与 `Vuex` 有极大的不同，`Pinia` 仅提供了一种方法来定义如何更改状态的规则，放弃 `mutations` 只依靠 `Actions`，这是一项重大的改变。

`Pinia` 让 `Actions` 更加的灵活：

- 可以通过组件或其他 `action` 调用
- 可以从其他 `store` 的 `action` 中调用
- 直接在 `store` 实例上调用
- 支持`同步`或`异步`
- 有任意数量的参数
- 可以包含有关如何更改状态的逻辑（也就是 vuex 的 mutations 的作用）
- 可以 `$patch` 方法直接更改状态属性

```ts
import { defineStore } from 'pinia'

export const useMainStore = defineStore({
  id: 'main',
  state: () => ({
    name: '超级管理员',
  }),
  getters: {
    nameLength: (state) => state.name.length,
  },
  actions: {
    async insertPost(data:string){
      // 可以做异步
      // await doAjaxRequest(data);
      this.name = data;
    }
  },
})

```

## 环境变量配置

> `vite` 提供了两种模式：具有开发服务器的`开发模式`（development）和`生产模式`（production）

项目根目录新建:`.env.development` :

```env
NODE_ENV=development

VITE_APP_WEB_URL= 'YOUR WEB URL'
```

项目根目录新建:`.env.production` :

```env
NODE_ENV=production

VITE_APP_WEB_URL= 'YOUR WEB URL'
```

组件中使用：

```js
console.log(import.meta.env.VITE_APP_WEB_URL)
```

配置 `package.json`:

> 打包区分开发环境和生产环境

```json
"build:dev": "vue-tsc --noEmit && vite build --mode development",
"build:pro": "vue-tsc --noEmit && vite build --mode production",
```

## 使用组件库 Naive UI

> 组件库选择，这里我们选择 `Naive UI` 至于为什么选择它？我可以直接说`尤大大`推荐的吗？

- 官方介绍：
  - 一个 `Vue 3` 组件库
  - 比较完整，`主题可调`，使用 `TypeScript`，不算太慢
  - 有点意思

介绍还是比较谦虚的，既然`尤大`推荐，肯定有它的优势了!!!

### 安装 Naive UI

```bash
# 安装 组件库
yarn add naive-ui
# 安装 字体
yarn add vfonts
```

### 如何使用

```js
import { NButton } from "naive-ui"
<n-button>naive-ui</n-button>
```

### 全局配置 Config Provider

> 全局化配置设置内部组件的`主题`、`语言`和组件卸载于其他位置的 `DOM` 的类名。

```html
<n-config-provider :locale="zhCN" :theme="theme">
    <!-- 容器 -->
</n-config-provider>
```

尤其是主题配置这个功能，我真的很喜欢 ❤️

> 组件库选择上不做任何强制，根据自己的项目需要选择合适的组件库即可

## Vite 常用基础配置

### 基础配置

`运行` `代理` 和 `打包` 配置

```js
server: {
    host: '0.0.0.0',
    port: 3000,
    open: true,
    https: false,
    proxy: {}
},
```

生产环境去除 `console` `debugger`

```js
build:{
  ...
  terserOptions: {
      compress: {
        drop_console: true,
        drop_debugger: true
      }
  }
}
```

### 生产环境生成 .gz 文件

> 开启 `gzip` 可以极大的压缩静态资源，对页面加载的速度起到了显著的作用。

使用 `vite-plugin-compression` 可以 `gzip` 或 `brotli` 的方式来压缩资源，这一步需要服务器端的配合，`vite` 只能帮你打包出 `.gz` 文件。此插件使用简单，你甚至无需配置参数，引入即可。

```bash
# 安装
yarn add --dev vite-plugin-compression
```

plugins 中添加：

```js
import viteCompression from 'vite-plugin-compression'

// gzip压缩 生产环境生成 .gz 文件
viteCompression({
      verbose: true,
      disable: false,
      threshold: 10240,
      algorithm: 'gzip',
      ext: '.gz',
    }),
```

### 最终 vite.config.ts

```js
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import path from 'path'
//@ts-ignore
import viteCompression from 'vite-plugin-compression'

// https://vitejs.dev/config/
export default defineConfig({
  base: './', //打包路径
  plugins: [
    vue(),
    // gzip压缩 生产环境生成 .gz 文件
    viteCompression({
      verbose: true,
      disable: false,
      threshold: 10240,
      algorithm: 'gzip',
      ext: '.gz',
    }),
  ],
  // 配置别名
  resolve: {
    alias: {
      '@': path.resolve(__dirname, 'src'),
    },
  },
  css:{
    preprocessorOptions:{
      scss:{
        additionalData:'@import "@/assets/style/main.scss";'
      }
    }
  },
  //启动服务配置
  server: {
    host: '0.0.0.0',
    port: 8000,
    open: true,
    https: false,
    proxy: {}
  },
  // 生产环境打包配置
  //去除 console debugger
  build: {
    terserOptions: {
      compress: {
        drop_console: true,
        drop_debugger: true,
      },
    },
  },
})

```

## 常用插件

> 可以查看官方文档：https://vitejs.cn/plugins/

- `@vitejs/plugin-vue` 提供 `Vue 3` 单文件组件支持
- `@vitejs/plugin-vue-jsx` 提供 Vue 3 `JSX` 支持（通过 专用的 Babel 转换插件）
- `@vitejs/plugin-legacy` 为打包后的文件提供传统浏览器`兼容性`支持
- `unplugin-vue-components` 组件的按需自动导入
- `vite-plugin-compression` 使用 gzip 或者 brotli 来压缩资源
- .....

## 非常推荐使用的 hooks 库

> 因为`vue3.x`和`react hooks`真的很像，所以就称为 `hooks`

`VueUse`：https://vueuse.org/

![](https://files.mdnice.com/user/16854/cbf73b46-d22b-44e7-bca1-c33764e41784.png)

看到这个库的第一眼，让我立马想到了 react 的 `ahooks`

`VueUse` 是一个基于 `Composition API` 的实用函数集合。通俗的来说，这就是一个`工具函数`包，它可以帮助你快速实现一些常见的功能，免得你自己去写，解决重复的工作内容。以及进行了基于 Composition API 的封装。让你在 vue3 中更加得心应手。

💡想要入手 vue3 的小伙伴，赶快学习起来吧！！！

💡最后给大家奉上仓库地址吧：https://github.com/xushanpei/vite_vue3_ts

## 写在最后

> `公众号`：`前端开发爱好者` 专注分享 `web` 前端相关`技术文章`、`视频教程`资源、热点资讯等，如果喜欢我的分享，给 🐟🐟 点一个`赞` 👍 或者 ➕`关注` 都是对我最大的支持。

欢迎`长按图片加好友`，我会第一时间和你分享`前端行业趋势`，`面试资源`，`学习途径`等等。

![](https://files.mdnice.com/user/16854/b382cc29-13f4-4cd7-86ae-c669cb7ae117.jpg)

关注公众号后，在首页：

- 回复`面试题`，获取最新大厂面试资料。
- 回复`简历`，获取 3200 套 简历模板。
- 回复`React实战`，获取 React 最新实战教程。
- 回复`Vue实战`，获取 Vue 最新实战教程。
- 回复`ts`，获取 TypeAcript 精讲课程。
- 回复`vite`，获取 精讲课程。
- 回复`uniapp`，获取 uniapp 精讲课程。
- 回复`js书籍`，获取 js 进阶 必看书籍。
- 回复`Node`，获取 Nodejs+koa2 实战教程。
- 回复`数据结构算法`，获取 数据结构算法 教程。
- 回复`架构师`，获取 架构师学习资源教程。
- 更多教程资源应用尽有，欢迎`关注获取`
