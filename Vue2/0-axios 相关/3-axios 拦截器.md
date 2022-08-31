# axios 拦截器

1. #### 什么是拦截器？

   拦截器会在<font color="red">每次发起 ajax 请求</font>和<font color="red">得到响应</font>的时候自动触发。

2. #### 应用场景

   - Token 身份认证
   - Loading 效果
   - etc...

3. #### 配置<font color="red">请求拦截器</font>

   通过 <font color="blue">axios.interceptors</font>.<font color="red">request</font>.<font color="blue">use</font>(<font color="red">成功的回调</font>, 失败的回调) 可以配置请求拦截器。

   ```js
   axios.interceptors.request.use((config) => {
     return config;
   }, (error) => {
     return Promise.reject(error);
   })
   ```

   注意：失败的回调可以被省略！

   

   - ##### 请求拦截器 —— <font color="red">Token 认证</font>

     ```js
     import axios from 'axios'
     
     axios.defaults.baseURL = 'http://www.escook.cn'
     
     axios.interceptors.request.use((config) => {
       config.headers.Authorization = 'Bearer xxx'
       return config
     })
     ```

     

   - ##### 请求拦截器 —— <font color="red">Loading 效果</font>

     借助于 element ui 提供的 Loading 效果组件实现：

     ```js 
     import { Loading } from 'element-ui'
     
     let loadingInstance = null
     
     axios.interceptors.request.use((config) => {
       loadingInstance = Loading.service({ fullscreen: true })
       return config
     })
     ```

   

4. #### 配置<font color="red">响应拦截器</font>

   通过 <font color="blue">axios.interceptors</font>.<font color="red">response</font>.<font color="blue">use</font>(<font color="red">成功的回调</font>, 失败的回调) 可以配置响应拦截器。

   ```js
   axios.interceptors.request.use((response) => {
     return response;
   }, (error) => {
     return Promise.reject(error);
   })
   ```

   注意：失败的回调可以被省略！

   

   - ##### 响应拦截器 —— <font color="red">关闭 Loading 效果</font>

     调用 Loading 实例提供的 close() 方法即可关闭 Loading 效果。

     ```js
     axios.interceptors.request.use((response) => {
       loadingInstance.close()
       return response
     })
     ```
