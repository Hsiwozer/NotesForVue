# async 和 await

1. #### 什么是 async 和 await

   async / await是 ES8 (ECMAScript 2017）引入的新语法，用来简化 Promise 异步操作。在 async / await 出现之前，开发者只能通过链式 .then() 的方式处理 Promise 异步操作。

2. #### 基本使用

   ```js
   import thenFs from 'then-fs'
   async function getAllFile() {
     const r1 = await thenFs.readFile('./files/1.txt', 'utf8')
     console.log(r1)
     const r2 = await thenFs.readFile('./files/2.txt', 'utf8')
     console.log(r2)
     const r3 = await thenFs.readFile('./files/3.txt', 'utf8')
     console.log(r3)
   }
   getAllFile()
   ```

   

3. #### 使用的注意事项

   - 如果在 function 中使用了await，则 function 必须被 async 修饰
   - 在 async 方法中，第一个 await 之前的代码会同步执行，await 之后的代码会异步执行

