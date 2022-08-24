# Vue-cli

1. #### **什么是单页面应用程序**

   单页面应用程序（英文名：Single Page Application）简称 SPA，顾名思义，指的是<font color="red">一个 Web 网站中只有**唯一**的一个 **HTML** 页面</font>，所有的功能与交互都在这唯一的一个页面内完成。

2. ####  **什么是** **vue-cli**

   vue-cli （俗称：脚手架）是 Vue.js 开发的标准工具。它简化了程序员基于 webpack 创建工程化的 Vue 项目的过程。

   [中文官网：https://cli.vuejs.org/zh/](https://cli.vuejs.org/zh/)

3. ####  **安装和使用**

   vue-cli 是 npm 上的一个全局包，使用 npm install 命令，即可方便的把它安装到自己的电脑（Mac）上：`sudo npm install -g @vue/cli`

   查看 vue 版本：`vue -V`

   基于 vue-cli 快速生成工程化的 Vue 项目：`vue create 项目的名称`

   Please pick a preset: 提示中，建议选择 Manually select features 选项

   <img src="/Users/hsiwozer/Library/Application Support/typora-user-images/image-20220812230316381.png" alt="image-20220812230316381" style="zoom: 50%;" />

   <img src="/Users/hsiwozer/Library/Application Support/typora-user-images/image-20220812231200237.png" alt="image-20220812231200237" style="zoom:50%;" />

4. ####  **vue** **项目的运行流程**

   在工程化的项目中，vue 要做的事情很单纯：通过 <font color="red">main.js</font> 把 <font color="red">App.vue</font> 渲染到 <font color="red">index.html</font> 的指定区域中。

   其中：

   - <font color="red">App.vue</font> 用来编写待渲染的<font color="red">模板结构</font>
   - <font color="red">index.html</font> 中需要预留一个 <font color="red">el 区域</font>
   - <font color="red">main.js</font> 把 App.vue 渲染到了 index.html 所预留的区域中

5. #### vue 项目中 src 目录的构成

   - **assets** 文件夹：存放项目中用到的静态资源文件，例如：css 样式表、图片资源
   - **components** 文件夹：程序员封装的、可复用的组件，都要放到 components 目录下
   - **main.js** 是项目的入口文件。整个项目的运行，要先执行 main.js
   - **App.vue** 是项目的根组件

