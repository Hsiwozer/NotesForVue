# axios 的基本使用

###### 安装 axios `npm i axios -S`

- #### 基础语法

  ###### 基本用法

  ```js
  const result = axios({
    method: '请求类型', // GET POST
    url: '请求的 URL 地址'
  })
  
  result.then(() => {
    // 回调函数
  })
  ```

  ###### 链式编程

  ```js
  axios({
    method: '请求类型', // GET POST
    url: '请求的 URL 地址'
  }).then((result) => {
    // .then 用来指定请求成功之后的回调函数
    // 形参中的 result 是请求成功之后的结果
  })
  ```

  

- #### 传参

  ```js
  axios({
    method: '请求类型', // GET POST
    url: '请求的 URL 地址',
    // URL 中的查询参数（GET 传参使用）
    params: {},
    // 请求体参数（POST 传参使用）
    data: {}
  }).then((result) => {
    // .then 用来指定请求成功之后的回调函数
    // 形参中的 result 是请求成功之后的结果
  })
  ```

  

- #### async 和 await

  ```js
  document.querySelector('btn').addEventListener('click', async function() {
    // 如果调用某个方法的返回值是 Promise 实例，则前面可以添加 await
    // await 只能用在被 async 修饰的方法中
    await axios({
      method: 'POST',
      url: 'URL 地址',
      data: {
        name: 'zs',
        age: 20
      }
    })
  })
  ```

  

- #### <font color="red">解构赋值</font>

  ```js
  document.querySelector('btn').addEventListener('click', async function() {
    const { data: res } = await axios({
      method: 'GET',
      url: '请求的 URL 地址'
  	})
  	console.log(res.data)
  })
  ```

  

- #### <font color="red">基于 axios.get 和 axios.post 发起请求</font>

  ###### 最终写法
  
  ```js
  document.querySelector('btn').addEventListener('click', async function() {
    const { data: res } = await axios.get('URL 地址', {
      params: { id: 1 }
    })
  })
  ```
  
  ```js
  document.querySelector('btn').addEventListener('click', async function() {
    const { data: res } = await axios.post('URL 地址', {/* POST 请求体数据 */})
  })
  ```
  
  