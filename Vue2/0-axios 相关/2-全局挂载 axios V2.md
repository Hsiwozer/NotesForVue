# 全局挂载 axios <font color="red">V2</font>

###### 安装 axios `npm i axios -S`

##### main.js

```js
import axios from 'axios'

// 全局配置 axios 的请求根路径
axios.defaults.baseURL = 'http://www.liulongbin.top:3006'
// 把 axios 挂载到 Vue.prototype 上，供每个 .vue 组件的实例直接使用
Vue.prototype.$http = axios
```



##### Left.vue

```vue
<template>
  <div class="left-container">
    <h3>Left 组件</h3>
    <button @click="getInfo">发起 GET 请求</button>
  </div>
</template>

<script>
export default {
  methods: {
    async getInfo () {
      const { data: res } = await this.$http.get('/api/get')
      console.log(res)
    }
  }
}
</script>

<style lang="less" scoped>
.left-container {
  background-color: orange;
  min-height: 200px;
  flex: 1;
}
</style>

```

