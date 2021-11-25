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

生命周期钩子变化

## 介绍 vite

> Vite：下一代前端开发与构建工具

- 💡 极速的开发服务器启动
- ⚡️ 轻量快速的热模块重载（HMR）
- 🛠️ 丰富的功能
- 📦 自带优化的构建
- 🔩 通用的插件接口
- 🔑 完全类型化的 API

Vite （法语意为 “迅速”，发音 /vit/）是一种全新的前端构建工具，它极大地改善了前端开发体验。

它主要由两部分组成：

- 一个开发服务器，它基于 原生 ES 模块 提供了 丰富的内建功能，如速度快到惊人的 模块热更新（HMR）。

- 一套构建指令，它使用 Rollup 打包你的代码，并且它是预配置的，可以输出用于生产环境的优化过的静态资源。

- Vite 意在提供开箱即用的配置，同时它的 插件 API 和 JavaScript API 带来了高度的可扩展性，并有完整的类型支持。

## 使用 vite 快速创建脚手架

> 兼容性注意:Vite 需要 `Node.js` 版本 `>= 12.0.0`。

1. 第一步: 在需要创建项目文件目录下打开 cmd 运行以下命令

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

3. 第三步: cd 到项目文件夹,安装依赖,启动项目

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

注意: 如果 eslint 安装报错:
![](https://files.mdnice.com/user/16854/98ff3635-d460-4a8f-b3d3-2597a03e56c0.png)
可以尝试运行以下命令:

```bash
yarn config set ignore-engines true
```

运行成功后再次执行 eslint 安装命令

### 项目下新建 .eslintrc.js

> 配置 eslint 校验规则:

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
    '@typescript-eslint/no-unused-vars':'off',
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
    'no-async-promise-executor': 'warn'
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

> 解决 ESLint 中的样式规范和 prettier 中样式规范的冲突，以 prettier 的样式规范为准，使 ESLint 中的样式规范自动失效

```bash
# 安装插件 eslint-config-prettier
yarn add eslint-config-prettier --dev
```

### 项目下新建 .prettier.js

> 配置 prettier 格式化规则:

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
      files: "*.json",
      options: {
        printWidth: 200
      }
    }
  ],
  arrowParens: "always"
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

上面配置完成后,可以运行以下命令测试下代码检查个格式化效果:

```bash
# eslint 检查
yarn lint
# prettier 自动格式化
yarn prettier
```

### 配置 husk

### 配置文件引用别名

> 直接修改 vite.config.ts 文件配置:

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

