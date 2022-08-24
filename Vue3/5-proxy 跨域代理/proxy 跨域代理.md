# proxy 跨域代理

1. #### 什么是跨域问题？

   ###### 同源策略：同一协议，同一域名，同一端口号。只要不满足三者其中一种都是属于跨域问题。

2. #### 通过<font color="red">代理</font>解决接口的跨域问题

   - 把 axios 的<font color="red">请求根路径</font>设置为 <font color="red">vue 项目的运行地址</font>（接口请求不再跨域）
   - vue 项目发现请求的接口不存在，把请求<font color="red">转交给 proxy 代理</font>
   - 代理把请求根路径<font color="red">替换</font>为 devServer.proxy 属性的值，<font color="red">发起真正的数据请求</font>
   - 代理把请求到的数据，<font color="red">转发给 axios</font>

   ```xml
   // App.vue
   async getUsers() {
   	const { data: res } = await this.$http.get('/api/users')
   	console.log(res)
   }
   
   // main.js
   axios.defaults.baseURL = 'http://localhost:8080'
   
   // src/vue.config.js
   module.exports = {
   	devServer: {
   		proxy: 'https://www.escook.cn',
   	}
   }
   // 随后从起打包服务器 npm run serve
   ```



##### 注意：

- devserver.proxy 提供的代理功能，<font color="red">仅在开发调试阶段生效</font>
- 项目上线发布时，依旧需要 API 接口服务器<font color="red">开启 CORS</font> 跨域资源共享