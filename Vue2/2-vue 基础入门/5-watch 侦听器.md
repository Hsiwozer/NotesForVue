# watch 侦听器

1. #### 什么是 watch 侦听器

   watch 侦听器允许开发者监视数据的变化，从而针对<font color="red">数据的变化做特定的操作</font>。

   ```js
   const vm = new Vue({
       el: '#app',
       data: {
           username: ''
       },
       watch: {
         // 要监听谁，就把它的数据名作为方法名
       	username(newVal, oldVal) {
       		console.log(newVal, oldVal)
       	}
       }
   })
   ```

   

2. #### **使用** **watch** **检测用户名是否可用**

   监听 username 值的变化，并使用 axios 发起 Ajax 请求，检测当前输入的用户名是否可用：

   ```js
   watch: {
   	// 监听 username 值的变化
   	async username(newVal) {
   		if (newVal === '') return
   		// 使用 axios 发送请求，判断用户名是否可用
   		const { data: res } = await axios.get('https://www.escook.cn/api/finduser/' + newVal)
   		console.log(res)
   	}
   }
   ```

   

3. #### immediate 选项

   默认情况下，组件在初次加载完毕后不会调用 watch 侦听器。如果想让 watch 侦听器<font color="red">立即被调用</font>，则需要使用 immediate 选项。示例代码如下：

   ```js
   watch: {
     username: {
       // handler 是固定写法，表示当 username 的值变化时，自动调用 handler 处理函数
       handler: async function (newVal) {
         if (newVal === '') return
         const { data: res } = await axios.get('https://www.escook.cn/api/finduser/' + newVal)
         console.log(res)
     	},
     // 表示页面初次渲染好之后，就立即触发当前的 watch 侦听器
     immediate: true
   	}
   }
   ```

   

4. #### deep 选项

   如果 watch <font color="red">侦听的是一个对象</font>，如果<font color="red">对象中的属性值发生了变化</font>，则<font color="red">无法被监听到</font>。此时需要使用 deep 选项，代码示例如下：

   ```html
   <div id="app">
       <input type="text" v-model="info.username">
   </div>
   
   <script src="./lib/vue-2.6.12.js"></script>
   <script>
       const vm = new Vue({
           el: '#app',
           data: {
               info: {
                   username: 'admin'
               }
           },
           watch: {
               info: {
                   handler(newVal) {
                       console.log(newVal);
                   },
                   deep: true
               }
           }
       })
   </script>
   ```

   

5. #### **监听对象单个属性的变化**

   如果只想监听对象中单个属性的变化，则可以按照如下的方式定义 watch 侦听器：

   ```js
   watch: {
       'info.username' (newVal) {
           console.log(newVal);
       }
   }
   ```