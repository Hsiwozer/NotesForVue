# Vuex 的基本使用

1. #### 安装 vuex 依赖包

   ```bash
   npm i vuex -S
   ```

   

2. #### 导入 vuex 包

   ```js
   // main.js
   
   import Vuex from 'vuex'
   Vue.use(Vuex)
   ```

   

3. #### 创建 store 对象

   ```js
   const store = new Vuex.Store({
     // state 中存放的是全局共享的数据
     state: { count: 0 }
   })
   ```

   

4. #### 将 store 对象挂载到 vue 实例中

   ```js
   new Vue({
     el: '#app',
     render: h => h(app),
     router,
     store
   })
   ```