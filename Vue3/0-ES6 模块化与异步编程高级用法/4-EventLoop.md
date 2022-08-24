# EventLoop

1. #### Javascript 是单线程的语言

   Javascript 是一门单线程执行的编程语言。也就是说，同一时间只能做一件事情。

   单线程执行任务队列的问题：如果前一个任务非常耗时，则后续的任务就不得不一直等待，从而导致<font color="red">程序假死</font>的问题。

2. #### 同步任务和异步任务

   为了防止某个<font color="red">耗时任务</font>导致<font color="red">程序假死</font>的问题，Javascript 把待执行的任务分为了两类：

   - ##### 同步任务 (synchronous)

     - 又叫做<font color="red">非耗时任务</font>，指的是在主线程上排队执行的那些任务
     - 只有前一个任务执行完毕，才能执行后一个任务

   - ##### 异步任务 (asynchronous)

     - 又叫做<font color="red">耗时任务</font>，异步任务由 Javascript <font color="red">委托给</font><font color="red">宿主环境</font>进行执行
     - 当异步任务执行完成后，会<font color="red">通知 Javascript 主线程</font>执行异步任务的<font color="red">回调函数</font>

3. #### 同步任务和异步任务的执行过程

   - 同步任务由 Javascript 主线程次序执行
   - 异步任务委托给宿主环境执行
   - 已完成的异步任务对应的回调函数，会被加入到任务队列中等待执行
   - Javascript 主线程的执行栈被清空后，会读取任务队列中的回调函数，次序执行
   - Javascript 主线程不断重复上面的第 4 步

4. #### EventLoop 的基本概念

   <font color="red">Javascript 主线程从 “任务队列〞 中读取异步任务的回调函数，放到执行栈中依次执行。</font>这个过程是循环不断的，所以整个的这种运行机制又称为 EventLoop（事件循环）。