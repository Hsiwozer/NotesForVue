# vue-router 4.x 的基本使用

##### [vue-router 的官方文档地址：https://router.vuejs.org/zh/](https://router.vuejs.org/zh/)

1. #### 在项目中安装 vue-router

   ###### 在 vue3 的项目中，只能安装并使用 vue-router 4.x。

   `npm i vue-router@next -S`

2. #### 定义路由组件

   定义需要使用到路由的组件。

3. #### 声明路由链接和占位符

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

   

4. #### 创建路由模块

   ##### 在项目中<font color="red">创建 router.js</font> 路由模块，并按一下步骤创建并得到路由的实例对象。

   - 从 vue-router 中按需导入两个方法

     ```js
     // router.js
     
     // createRouter 方法用于创建路由的实例对象
     // createWebHashHistory 用于指定路由的工作模式（hash 模式）
     import { createRouter, createWebHashHistory } from 'vue-router'
     ```

     

   - 导入需要使用路由控制的组件

     ```js
     // router.js
     
     import Home from './components/Home.vue'
     import Movie from './components/Movie.vue'
     import About from './components/About.vue'
     ```

     

   - 创建路由实例对象

     ```js
     // router.js
     
     const router = createRouter({
       // history 属性指定路由的工作模式
       history: createWebHashHistory(),
       // routes 数组指定路由规则
       routes: [
         { path: '/home', component: Home },
         { path: '/movie', component: Movie },
         { path: '/about', component: About }
       ],
     })
     ```

     

   - 向外共享路由实例对象

     ```js
     // router.js
     
     export default router
     ```

     

   - 在 main.js 中导入并挂载路由模块

     ```js
     // main.js
     
     // 导入路由模块
     import router from './router'
     
     const app = createApp(App)
     
     // 挂载路由模块
     app.use(router)
     
     app.mount('#app')
     ```