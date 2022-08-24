# vue 的过滤器

1. #### 什么是过滤器

   过滤器（Filters）是 vue 为开发者提供的功能，常用于<font color="red">文本的格式化</font>。过滤器可以用在两个地方：<font color="red">插值表达式</font>和 <font color="red">v-bind 属性绑定</font>。

   过滤器应该被添加在 JavaScript 表达式的尾部，由 <font color="red">“管道符”</font> 进行调用。

   

2. #### 定义过滤器

   在创建 vue 实例期间，可以在 filters 节点中定义过滤器，示例代码如下：

   ```html
   <div id="app">
       <p>message 的值是：{{ message | capitalize }}</p>
   </div>
   
   <script src="./lib/vue-2.6.12.js"></script>
   <script>
       const vm = new Vue({
           el: '#app',
           data: {
               message: 'hello world!'
           },
           filters: {
               capitalize(str) {
                   return str.charAt(0).toUpperCase() + str.slice(1)
               }
           }
       })
   </script>
   ```

   ⚠️**注意点：**

   - 过滤器函数必须被定义在 filters 节点中
   - 过滤器中一定要有返回值
   - 过滤器函数中的参数 str 为 “ ｜ ”前面的值

   

3. #### 私有过滤器和全局过滤器

   在 filters 节点下定义的过滤器，称为 “<font color="red">私有过滤器</font>”，因为它只能在<font color="red">当前 vm 实例所控制的 el 区域内使用</font>。如果希望在<font color="red">多个 vue 实例之间共享过滤器</font>，则可以按照如下的格式定义<font color="red">全局过滤器</font>：

   ```js
   // 全局过滤器 - 独立于每个 vm 实例之外
   // Vue.filter() 方法接收两个参数：
   // 1. 全局过滤器的名字
   // 2. 全局过滤器的处理函数
   Vue.filter('capitalize', (str) => {
   	return str.charAt(0).toUpperCase() + str.slice(1)
   })
   ```
