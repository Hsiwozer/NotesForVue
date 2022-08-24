# Promise

1. #### 回调地狱

   <font color="red">多层回调函数的相互嵌套</font>，就形成了回调地狱。

2. #### Promise 基本概念

   - ##### Promise 是一个<font color="red">构造函数</font>

     - 可以创建 Promise 实例 `const p = new Promise()`
     - new 出来的 Promise 实例对象，代表一个<font color="purple">异步操作</font>

   - ##### <font color="red">Promise.prototype</font> 上包含一个 <font color="red">.then()</font> 方法

     - 每一次 new Promise() 构造函数得到的实例对象都可以<font color="purple">通过原型链的方式</font>访问到 .then() 方法。例如 p.then()

   - ##### .then() 方法用来<font color="red">预先指定成功和失败的回调函数</font>

     - p.then(<font color="purple">成功的回调函数</font>, <font color="purple">失败的回调函数</font>)
     - p.then(<font color="purple">result</font> => {}, <font color="purple">error</font> => {})
     - 调用 .then() 方法时，成功的回调函数是必选的、失败的回调函数是可选的

     

3. #### <font color="red">基于回调函数</font>按顺序读取文件内容

   ```js
   fs.readFile('./files/1.txt', 'utf8', (err1, r1) => {
     if (err1) return console.log(err1.message)
     console.log(r1)
     fs.readFile('./files/2.txt', 'utf8', (err2, r2) => {
     	if (err2) return console.log(err2.message)
     	console.log(r2)
     	fs.readFile('./files/3.txt', 'utf8', (err3, r3) => {
     		if (err3) return console.log(err3.message)
     		console.log(r3)
   		})
   	})
   })
   ```

   产生了回调地狱问题！

   

4. #### <font color="red">基于 then-fs</font> 读取文件内容

   由于 node.js 官方提供的 fs 模块仅支持以回调函数的方式读取文件，不支持 Promise 的调用方式。因此，需要先运行如下的命令，安装 then-fs 这个第三方包，从而支持我们基于 Promise 的方式读取文件的内容：`npm install then-fs`

   - ##### then-fs 的基本使用

     调用 then-fs 提供的 readFile() 方法，可以异步地读取文件的内容，<font color="red">它的返回值是 Promise 的实例对象</font>。因此可以调用 .then() 方法为每个 promise 异步操作指定成功和失败之后的回调函数。示例代码如下：

     ```js
     import thenFs from 'then-fs'
     // 注意：.then() 方法中的失败回调是可选的，可以被省略
     thenFs.readFile('./files/1.txt', 'utf8').then(r1 => { console.log(r1) }, err1 => { console.log(err1.message) })
     thenFs.readFile('./files/1.txt', 'utf8').then(r2 => { console.log(r2) }, err2 => { console.log(err2.message) })
     thenFs.readFile('./files/1.txt', 'utf8').then(r3 => { console.log(r3) }, err3 => { console.log(err3.message) })
     ```

     

   - ##### .then() 方法的特性

     如果上一个 .then() 方法中返回了一个新的 Promise 实例对象，则可以通过下一个. then() 继续进行处理。通过.then() 方法的链式调用，就解决了回调地狱的问题。

     ```js
     import thenFs from 'then-fs'
     thenFs.readFile('./files/1.txt', 'utf8')
       .then(r1 => {
       	console.log(r1)
       	return thenFs.readFile('./files/1.txt', 'utf8')
     	})
       .then(r2 => {
       	console.log(r2)
       	return thenFs.readFile('./files/1.txt', 'utf8')
     	})
       .then(r3 => {
       	console.log(r3) 
     	})
     ```

     

   - ##### 通过 .catch 捕获错误

     在 promise 的链式操作中如果发生了错误，可以使用 Promise.prototype.catch 方法进行捕获和处理：

     ```js
     import thenFs from 'then-fs'
     thenFs.readFile('./files/11.txt', 'utf8')	// 文件不存在导致读取错误，后面 3 个 .then 都不执行
       .then(r1 => {
       	console.log(r1)
       	return thenFs.readFile('./files/1.txt', 'utf8')
     	})
       .then(r2 => {
       	console.log(r2)
       	return thenFs.readFile('./files/1.txt', 'utf8')
     	})
       .then(r3 => {
       	console.log(r3) 
     	})
     	.catch(err => {	// 捕获第 1 行发生的错误，并输出错误的信息
       	console.log(err.message)
     })
     ```

     如果不希望前面的错误导致后续的.then 无法正常执行，则可以将.catch 的调用提前：

     ```js
     import thenFs from 'then-fs'
     thenFs.readFile('./files/11.txt', 'utf8')
     	.catch(err => {
       	console.log(err.message)
     	})
       .then(r1 => {
       	console.log(r1)
       	return thenFs.readFile('./files/1.txt', 'utf8')
     	})
       .then(r2 => {
       	console.log(r2)
       	return thenFs.readFile('./files/1.txt', 'utf8')
     	})
       .then(r3 => {
       	console.log(r3) 
     	})
     ```

     

   - ##### <font color="red">Promise.all()</font> 方法

     promise.all() 方法会发起并行的 Promise 异步操作，等<font color="red">所有的异步操作全部结束后</font>才会执行下一步的 .then 操作（等待机制）。

     ```js
     // 定义 1 个数组，存放 3 个读文件的异步操作
     const promiseArr = [
       thenFs.readFile('./files/1.txt', 'utf8'),
       thenFs.readFile('./files/2.txt', 'utf8'),
       thenFs.readFile('./files/3.txt', 'utf8'),
     ]
     // 将 Promise 的数组，作为 Promise.all() 的参数
     Promise.all(promiseArr)
     	.then(([r1, r2, r3]) => {
       	console.log(r1, r2, r3)
     	})
     	.catch(err => {
       	console.log(err.message)
     	})
     ```

     

   - ##### <font color="red">Promise.race()</font> 方法

     promise.race(）方法会发起并行的 promise 异步操作，只要<font color="red">任何一个异步操作完成</font>，就立即执行下一步的.then 操作（赛跑机制）。

     ```js
     // 定义 1 个数组，存放 3 个读文件的异步操作
     const promiseArr = [
       thenFs.readFile('./files/1.txt', 'utf8'),
       thenFs.readFile('./files/2.txt', 'utf8'),
       thenFs.readFile('./files/3.txt', 'utf8'),
     ]
     // 将 Promise 的数组，作为 Promise.all() 的参数
     Promise.rece(promiseArr)
     	.then((result) => {
       	console.log(result)
     	})
     	.catch(err => {
       	console.log(err.message)
     	})
     ```

     

5. #### <font color="red">基于 Promise</font> 封装读文件的方法

   方法的封装要求：方法名要定义为 <font color="red">getFile</font>；方法接收一个形参 <font color="red">fpath</font>，表示要读取的文件的路径；方法的<font color="red">返回值</font>为 Promise 实例对象。

   - ##### getFile 方法的基本定义

     ```js
     function getFile(fpath) {
       return new Promise()
     }
     ```

     注意：new Promise() 只是创建了一个形式上的异步操作。

     

   - ##### 创建具体的异步操作

     如果想要创建具体的异步操作，则需要在 new Promise(）构造函数期间，传递一个 function 函数，将具体的异步操作定义到  function 函数内部。

     ```js
     function getFile(fpath) {
       return new Promise(() => {
         fs.readFile(fpath, 'utf8', (err, dataStr) => {})
       })
     }
     ```

     

   - ##### 获取 .then 的两个实参

     通过 .then() 指定的成功和失败的回调函数，可以在 function 的形参中进行接收。

     ```js
     function getFile(fpath) {
       return new Promise((resolve, reject) => {
         fs.readFile(fpath, 'utf8', (err, dataStr) => {})
       })
     }
     getFile('./files/1.txt').then(成功的回调函数, 失败的回调函数)
     ```

     

   - ##### 调用 resolve 和 reject 回调函数

     Promise 异步操作的结果，可以调用 resolve 或 reject 回调函数进行处理。

     ```js
     function getFile(fpath) {
       return new Promise((resolve, reject) => {
         fs.readFile(fpath, 'utf8', (err, dataStr) => {
           if(err) return reject(err)	// 如果读取失败，则调用“失败的回调函数”
           resolve(dataStr)	// 如果读取成功，则调用“成功的回调函数”
         })
       })
     }
     getFile('./files/1.txt').then(成功的回调函数, 失败的回调函数)
     ```