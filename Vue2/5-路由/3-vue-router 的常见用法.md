# vue-router 的常见方法

1. #### **路由重定向**

   路由重定向指的是：用户在访问地址 A 的时候，强制用户跳转到地址 C ，从而展示特定的组件页面。通过路由规则的 <font color="red">**redirect**</font> 属性，指定一个新的路由地址，可以很方便地设置路由的重定向：

   ```js
   const router = new VueRouter({
     routes: [
       { path: '/', redirect: '/home' },
       { path: '/home', component: Home },
       { path: '/movie', component: Movie },
       { path: '/about', component: About }
     ]
   })
   ```

   

2. #### **嵌套路由**

   通过路由实现组件的嵌套展示，叫做嵌套路由。

3. #### **子路由**

   - ##### 声明子路由链接和子路由占位符

     在 About.vue 组件中，声明 tab1 和 tab2 的子路由链接以及子路由占位符。

     ```vue
     <template>
       <div class="about-container">
         <h3>About 组件</h3>
     
         <router-link to="/about/tab1">tab1</router-link>
         <router-link to="/about/tab2">tab2</router-link>
     
         <hr>
     
         <router-view></router-view>
       </div>
     </template>
     ```

     

   - ##### **通过** **children**属性声明子路由规则

     在 src/router/index.js 路由模块中，导入需要的组件，并使用 <font color="red">**children**</font> 属性声明子路由规则：

     ```js
     import Tab1 from '@/components/tabs/Tab1.vue'
     import Tab2 from '@/components/tabs/Tab2.vue'
     
     Vue.use(VueRouter)
     
     const router = new VueRouter({
       routes: [
         { path: '/', redirect: '/home' },
         { path: '/home', component: Home },
         { path: '/movie', component: Movie },
         { 
           path: '/about',
           component: About,
           children: [
             { path: 'tab1', component: Tab1 },
             { path: 'tab2', component: Tab2 }
           ]
         }
       ]
     })
     ```

     

4. #### **动态路由匹配**

   - ##### 概念

     动态路由指的是：把 Hash 地址中可变的部分定义为参数项，从而提高路由规则的复用性。 在 vue-router 中使用英文的冒号（**:**）来定义路由的参数项。

     ```vue
     // 路由中的动态参数以 : 进行声明，冒号后面的事动态参数的名称
     { path: '/movie/:id', component: Movie }
     
     // 将一下3个路由规则合并成一个，提高了路由规则的复用性
     { path: '/movie/1', component: Movie }
     { path: '/movie/2', component: Movie }
     { path: '/movie/3', component: Movie }
     ```

     

   - ##### **$route.params** **参数对象**

     在动态路由渲染出来的组件中，可以使用 <font color="red">this.$route.params</font> 对象访问到<font color="red">动态匹配的参数值</font>。

     ```vue
     <template>
       <div class="movie-container">
         <h3>Movie 组件 --- {{ this.$route.params.id }}</h3>
       </div>
     </template>
     
     <script>
     export default {
       name: 'Movie'
     }
     </script>
     ```

     

   - ##### **使用 props 接收路由参数**

     为了简化路由参数的获取形式，vue-router 允许在路由规则中开启 props 传参。

     ```vue
     /* /src/router/index.js */
     { path: '/movie', component: Movie, props: true }
     
     /* Movie.vue */
     <template>
       <div class="movie-container">
         <h3>Movie 组件 --- {{ id }}</h3>
       </div>
     </template>
     
     <script>
     export default {
       name: 'Movie',
       props: ['id']
     }
     </script>
     ```

   - ##### query 和 fullPath

     ```vue
     <!-- 在 Hash 地址中，/ 后面的参数项，叫做 “路径参数”，通过 this.$route.params 来访问 -->
     <!-- 在 Hash 地址中，? 后面的参数项，叫做 “查询参数”，通过 this.$route.query 来访问 -->
     <!-- 在 this.$route 中，path 只是路径部分，fullPath 是完整的地址 -->
     <!-- /movie/1?name=zs&age=20 是 fullPath -->
     <!-- /movie/1 是 path -->
     <router-link to="/movie/1?name=zs&age=20">电影1</router-link>
     ```

     

5. #### **声明式导航 & 编程式导航**

   **声明式导航**：在浏览器中，点击链接实现导航的方式。普通网页中点击 `<a>` 链接、vue 项目中点击 `<router-link>` 都属于声明式导航。

   **编程式导航**：在浏览器中，调用 API 方法实现导航的方式。普通网页中调用 *location.href* 跳转到新页面的方式，属于编程式导航。

   - ##### **vue-router 中的编程式导航 API**

     - <font color="red">this.$router.push('hash 地址')</font>：跳转到指定 hash 地址，并<font color="red">增加</font>一条历史记录
     - <font color="red">this.$router.replace('hash 地址')</font>：跳转到指定的 hash 地址，并<font color="red">替换掉当前</font>的历史记录
     - <font color="red">this.$router.go(数值 n)</font>：实现导航历史前进、后退

   - ##### $router.push

     调用 this.$router.push() 方法，可以跳转到指定的 hash 地址，从而展示对应的组件页面。

     ```vue
     <template>
       <div class="home-container">
         <h3>Home 组件</h3>
         <hr>
         <button @click="gotoM1">跳转到电影1</button>
       </div>
     </template>
     
     <script>
     export default {
       name: 'Home',
       methods: {
         gotoM1() {
           this.$router.push('/movie/1')
         }
       },
     }
     </script>
     ```

     

   - ##### $router.replace

     调用 this.$router.replace() 方法，可以跳转到指定的 hash 地址，从而展示对应的组件页面。

     push 和 replace 的区别：

     - push 会增加一条历史记录
     - replace 不会增加历史记录，而是替换掉当前的历史记录

   - ##### $router.go

     调用 this.$router.go() 方法，可以在浏览历史中前进和后退。

     ```vue
     <template>
       <div class="movie-container">
         <h3>Movie 组件 --- {{ id }}</h3>
         <hr>
         <button @click="goBack">后退</button>
       </div>
     </template>
     
     <script>
     export default {
       name: 'Movie',
       props: ['id'],
       methods: {
         goBack() {
           this.$router.go(-1)
         }
       },
     }
     </script>
     ```

     在实际开发中，一般只会前进和后退一层页面。因此 vue-router 提供了如下两个便捷方法：

     - <font color="red">$router.back()</font>：在历史记录中，后退到上一个页面
     - <font color="red">$router.forward()</font>：在历史记录中，前进到下一个页面

6. #### **导航守卫**

   导航守卫可以<font color="red">控制路由的访问权限</font>。

   - ##### **全局前置守卫**

     每次发生路由的导航跳转时，都会触发全局前置守卫。因此，在全局前置守卫中，程序员可以对每个路由进行访问权限的控制。

     全局前置守卫的回调函数中接收 <font color="red">3 个形参</font>：

     - **to** 是将要访问的路由的信息对象
     - **from** 是将要离开的路由的信息对象
     - **next** 是一个函数，调用 next() 表示放行，允许这次路由导航

     next 函数的 <font color="red">3 种调用方式</font>：

     - 当前用户<font color="blue">拥有</font>后台主页的访问权限，<font color="blue">直接放行</font>：next()
     - 当前用户<font color="blue">没有</font>后台主页的访问权限，<font color="blue">强制其跳转到登录页面</font>：next('/login')
     - 当前用户<font color="blue">没有</font>后台主页的访问权限，<font color="blue">不允许跳转到后台主页，强制其停留在当前页面</font>：next(false)

     

     <font color="red">**控制后台主页的访问权限**</font>

     ```js
     // router/index.js
     router.beforeEach((to, from, next) => {
       if (to.path === '/main') {
         const token = localStorage.getItem('token')
         if (token) {
           next()  // 访问的是后台主页，且有 token 的值
         } else {
           next('/login')  // 访问的是后台主页，但是没有 token 的值
         }
       } else {
         next()  // 访问的不是后台主页，直接放行
       }
     })
     ```

     