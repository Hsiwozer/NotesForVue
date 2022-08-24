# vue 的基本使用

1. #### 基本使用步骤

   - 导入 vue.js 的 script 脚本文件
   - 在页面中声明一个将要被 vue 所控制的 DOM 区域
   - 创建 vm 实例对象（vue 实例对象）

   ```html
   <div id="app">{{ username }}</div>
   
   <!-- 导入 vue 库文件 -->
   <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
   
   <!-- 创建 vue 的实例对象 -->
   <script>
       // 创建 vue 的实例对象
       const vm = new Vue({
           // el 属性是固定写法，表示当前 vm 实例要控制页面上的哪个区域，接收的值是一个选择器
           el: '#app',
           // data 对象就是要渲染到页面上的数据
           data: {
               username: 'zhangsan'
           }
       })
   </script>
   ```