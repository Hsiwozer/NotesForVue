# 全局挂载 axios <font color="red">V3</font>

###### 安装 axios `npm i axios -S`

- ##### 在 <font color="red">main.js</font> 入口文件中，通过 <font color="red">app.config.globalProperties</font> 全局挂载axios

  ```js
  // main.js
  
  import axios from 'axios'
  
  // createApp(App).mount('#app') 作如下修改
  const app = createApp(App)
  
  axios.defaults.baseURL = 'http://www.xxx.com'
  app.config.globalProperties.$http = axios
  
  app.mount('#app')
  ```

  

- ##### 在组件中发起 <font color="red">POST</font> 请求

  ```vue
  methods: {
  	async postInfo() {
  		const { data: res } = await this.$http.post('/api/post', { name: 'zs', age: 20 })
  		console.log(res)
  	}
  }
  ```

  

- ##### 在组件中发起 <font color="red">GET</font> 请求

  ```vue
  methods: {
  	async getInfo() {
  		const { data: res } = await this.$http.get('/api/get', {
  			params: {
  				name: 'ls',
  				age: 10
  			},
  		})
  		console.log(res)
  	}
  }
  ```

  