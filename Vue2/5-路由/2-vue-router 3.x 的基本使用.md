# vue-router 3.x 的基本使用

1. #### **什么是 vue-router**

   vue-router 是 vue.js 官方给出的路由解决方案。它只能结合 vue 项目进行使用，能够轻松的管理 SPA 项目中组件的切换。

   [vue-router 的官方文档地址：https://router.vuejs.org/zh/](https://router.vuejs.org/zh/)

2. #### **vue-router 安装和配置的步骤**

   - ##### 安装 vue-router 包

     在 vue2 的项目中，安装 vue-router 的命令：`npm install vue-router@3.5.2 -S`

   - ##### 创建路由模块

     在 src 源代码目录下，新建 router/index.js 路由模块，并初始化如下的代码：

     ```js
     // src/router/index.js 就是当前项目的路由模块
     import Vue from 'vue'
     import VueRouter from 'vue-router'
     
     Vue.use(VueRouter)
     
     const router = new VueRouter()
     
     export default router
     ```

     

   - ##### 导入并挂载路由模块

     在 src/main.js 入口文件中，导入并挂载路由模块。示例代码如下：

     ```js
     // 导入路由模块
     import router from '@/router'
     
     new Vue({
       render: h => h(App),
       // 挂载路由模块
       router
     }).$mount('#app')
     ```

     

   - ##### 声明路由链接和占位符

     在 src/App.vue 组件中，使用 vue-router 提供的 `<router-link>` 和 `<router-view>` 声明路由链接和占位符：

     ```vue
     <template>
       <div class="app-container">
         <h1>App2 组件</h1>
     
         <router-link to="/home">首页</router-link>
         <router-link to="/movie">电影</router-link>
         <router-link to="/about">关于</router-link>
     
         <hr />
     
         <router-view></router-view>
       </div>
     </template>
     ```

     

3. #### 声明路由的匹配规则

   在 src/router/index.js 路由模块中，通过 routes 数组声明路由的匹配规则。示例代码如下：

   ```js
   import Home from '@/components/Home.vue'
   import Movie from '@/components/Movie.vue'
   import About from '@/components/About.vue'
   
   const router = new VueRouter({
     routes: [
       { path: '/home', component: Home },
       { path: '/movie', component: Movie },
       { path: '/about', component: About }
     ]
   })
   ```

   