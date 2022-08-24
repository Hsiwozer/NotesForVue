# vite 的基本使用

1. #### 创建 vite 的项目

   按照顺序执行如下命令，即可基于 vite 创建 <font color="red">vue3.x</font> 的工程化项目：

   ```bash
   npm init vite-app 项目名称
   
   cd 项目名称
   npm install
   npm run dev
   ```

   

2. #### 梳理项目结构

   - node_modules 目录用来存放第三方依赖包，通过命令 `npm i` 进行安装
   - public 是公共的静态资源目录
   - <font color="red">**src**</font> 是项目的源代码目录（程序员写的所有代码都要放在此目录下）
     - <font color="red">assets</font> 目录用来存放项目中所有的<font color="red">静态资源文件</font> (CSS、fonts等）
     - <font color="red">components</font> 目录用来存放项目中所有的<font color="red">自定义组件</font>
     - <font color="red">App.vue</font> 是项目的<font color="red">根组件</font>
     - <font color="red">index.css</font> 是项目的<font color="red">全局样式表文件</font>
     - <font color="red">main.js</font> 是整个项目的<font color="red">打包入口文件</font>
   - .gitignore 是 Git 的忽略文件
   - <font color="red">index.html</font> 是 SPA 单页面应用程序中唯一的 HTML 页面
   - package.json 是项目的包管理配置文件

   

3. #### vite 项目的运行流程

   在工程化的项目中，vue 要做的事情很单纯：通过 <font color="red">main.js</font> 把 <font color="red">App.vue</font> 渲染到 <font color="red">index.html</font> 的指定区域中。

   其中：

   - <font color="red">**App.vue**</font> 用来编写待渲染的<font color="red">模板结构</font>

     清空 App.vue 的默认内容，并书写如下的模版结构：

     ```vue
     <template>
       <h1>这是 App.vue 根组件</h1>
     </template>
     ```

     

   - <font color="red">**index.html**</font> 中需要预留一个 <font color="red">el 区域</font>

     打开 index.html 页面，确认预留了 el 区域：

     ```html
     <body>
       <div id="app"></div>
       <script type="module" src="/src/main.js"></script>
     </body>
     ```

     

   - <font color="red">**main.js**</font> 把 App.vue 渲染到了 index.html 所预留的区域中

     按照 <font color="red">vue 3.x</font> 的<font color="red">标准用法</font>，把 <font color="red">App.vue 中的模版内容</font>渲染到 <font color="red">index.html 页面的 el 区域</font>中：

     ```js
     // 1. 按需导入 createApp 函数
     import { createApp } from "vue";
     // 2. 导入待渲染的 App.vue 组件
     import App from './App.vue'
     
     // 3. 调用 createApp 函数，创建 SPA 应用的实例
     const app = createApp(App)
     
     // 4. 调用 mount 方法，把 APP 组件的模版结构，渲染到指定的 el 区域中
     app.mount('#app')
     ```