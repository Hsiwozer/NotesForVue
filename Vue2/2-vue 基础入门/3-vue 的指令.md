# vue 的指令

1. #### 指令的概念

   指令（Directives）是 vue 为开发者提供的模板语法，用于辅助开发者渲染页面的基本结构。

   vue 中的指令按照不同的用途可以分为如下 6 大类：

   - <font color="red">内容渲染</font>指令
   - <font color="red">属性绑定</font>指令
   - <font color="red">事件绑定</font>指令
   - <font color="red">双向绑定</font>指令
   - <font color="red">条件渲染</font>指令
   - <font color="red">列表渲染</font>指令

   

2. #### 内容渲染指令

   内容渲染指令用来辅助开发者渲染 DOM 元素的文本内容。常用的内容渲染指令有如下 3 个：

   - **v-text**

     ```html
     <!-- 把 username 对应的值，渲染到 p 标签的内容中 -->
     <p v-text="username"></p>
     <!-- 默认的文本“性别”会被 gender 覆盖掉 -->
     <p v-text="gender">性别</p>
     ```

     注意：v-text 指令会<font color="red">覆盖元素内默认的值</font>。

   - **{{ }}**

     vue 提供的 {{ }} 语法，专门用来解决 v-text 会覆盖默认文本内容的问题。这种 {{ }} 语法的专业名称是插值表达式（英文名为：Mustache）。

     ```html
     <p>性别:{{ gender }}</p>
     ```

     注意：相对于 v-text 指令来说，<font color="red">插值表达式在开发中更常用一些</font>！因为它不会覆盖元素中默认的文本内容。

   - **v-html**

     v-text 指令和插值表达式<font color="red">只能渲染纯文本内容</font>。如果要把<font color="red">包含 HTML 标签的字符串</font>渲染为页面的 HTML 元素，则需要用到 v-html 这个指令：

     ```html
     <p v-html="info"></p>
     ```

     

3. #### 属性绑定指令

   如果需要为元素的属性动态绑定属性值，则需要用到 <font color="red">**v-bind**</font> 属性绑定指令。用法示例如下：

   ```html
   <div id="app">
       <input type="text" v-bind:placeholder="tips">
   </div>
   
   <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
   <script>
       const vm = new Vue({
           el: '#app',
           data: {
               tips: '请输入用户名'
           }
       })
   </script>
   ```

   ###### ✅ 简写：

   省略 「v-bind」，只写 「：」

   ```html
   <div id="app">
       <input type="text" :placeholder="tips">
   </div>
   
   <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
   <script>
       const vm = new Vue({
           el: '#app',
           data: {
               tips: '请输入用户名'
           }
       })
   </script>
   ```

   

   ###### 补充：使用 Javascript 表达式

   ```html
   {{ number + 1 }}
   
   {{ ok ? 'YES' : 'NO' }}
   
   {{ message.split('').reverse().join('') }}
   
   <div :id="'list-' + id"></div>
   ```

   

4. ####  事件绑定指令

   vue 提供了<font color="red"> **v-on**</font> 事件绑定指令，用来辅助程序员为 DOM 元素绑定事件监听。语法格式如下：

   ```html
   <div id="app">
       <h3>count 的值为：{{ count }}</h3>
       <button v-on:click="addCount">+1</button>
   </div>
   ```

   注意：原生 DOM 对象有 onclick、oninput、onkeyup 等原生事件，替换为 vue 的事件绑定形式后，分别为：v-on:click、v-on:input、v-on:keyup

   通过 v-on 绑定的事件处理函数，需要在 <font color="red">**methods**</font> 节点中进行声明：

   ```js
   const vm = new Vue({
       el: '#app',
       data: {
           count: 0
       },
       // 定义事件处理函数
       methods: {
           addCount() {
               this.count += 1
           }
       }
   })
   ```

   ###### ✅ 简写：

   简写为英文的 **@**

   ```html
   <button @click="addCount">+1</button>
   ```

   

   ##### 事件传参

   在使用 v-on 指令绑定事件时，可以使用 **( )** 进行传参，示例代码如下：

   ```html
   <div id="app">
       <h3>count 的值为：{{ count }}</h3>
       <button v-on:click="addCount(2)">+n</button>
   </div>
   <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
   <script>
       const vm = new Vue({
           el: '#app',
           data: {
               count: 0
           },
           // 定义事件处理函数
           methods: {
               addCount(n) {
                   this.count += n
               }
           }
       })
   </script>
   ```

   

   ##### 事件对象 $event

   在原生的 DOM 事件绑定中，可以在事件处理函数的形参处，接收事件参数对象 event。同理，在 v-on 指令（简写为 @ ）所绑定的事件处理函数中，同样可以接收到事件参数对象 event。

   <font color="red">**$event**</font> 是 vue 提供的特殊变量，用来表示原生的事件参数对象 event。$event 可以解决事件参数对象 event <font color="red">**被覆盖**</font>的问题。示例用法如下：

   ```html
   <div id="app">
       <h3>count 的值为：{{ count }}</h3>
       <button v-on:click="addCount(1, $event)">+N</button>
   </div>
   <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
   <script>
       const vm = new Vue({
           el: '#app',
           data: {
               count: 0
           },
           // 定义事件处理函数
           methods: {
               addCount(n, e) {
                   this.count += n
                   if (this.count % 2 === 0) {
                       e.target.style.background = 'pink'
                   } else {
                       e.target.style.background = ''
                   }
               }
           }
       })
   </script>
   ```

   

   ##### 事件修饰符

   在事件处理函数中调用 <font color="red">event.preventDefault()</font> 或 <font color="red">event.stopPropagation()</font> 是非常常见的需求。因此，vue 提供了事件修饰符的概念，来辅助程序员更方便的<font color="red">对事件的触发进行控制</font>。常用的 5 个事件修饰符如下：

   |            事件修饰符             |                             说明                             |
   | :-------------------------------: | :----------------------------------------------------------: |
   | <font color="red">.prevent</font> | <font color="red">阻止默认行为</font>（例如：阻止 a 连接的跳转、阻止表单的提交等） |
   |  <font color="red">.stop</font>   |            <font color="red">阻止事件冒泡</font>             |
   |             .capture              |               以捕获模式触发当前的事件处理函数               |
   |               .once               |                     绑定的事件只触发1次                      |
   |               .self               |     只有在 event.target 是当前元素自身时触发事件处理函数     |

   ```html
   <a href="http://www.baidu.com" @click.prevent="show">跳转到百度首页</a>
   ```

   

   ##### 按键修饰符

   在监听<font color="red">键盘事件</font>时，我们经常需要<font color="red">判断详细的按键</font>。此时，可以为键盘相关的事件添加按键修饰符，例如：

   ```html
   <input type="text" @keyup.enter="submit" @keyup.esc="clearInput">
   ```

   

5. #### 双向绑定指令

   vue 提供了<font color="red"> **v-model**</font> 双向数据绑定指令，用来辅助开发者在<font color="red">不操作 DOM 的前提下，快速获取**表单**的数据</font>。

   多用在：input 输入框，textarea，select 等表单元素。

   ```html
   <div id="app">
       <p>用户名：{{ username }}</p>
       <input type="text" v-model="username">
   </div>
   
   <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
   <script>
       const vm = new Vue({
           el: '#app',
           data: {
               username: 'zhangsan'
           }
       })
   </script>
   ```

   

   ##### v-model 指令的修饰符

   为了方便对用户输入的内容进行处理，vue 为 v-model 指令提供了 3 个修饰符，分别是：

   | **修饰符** |             **作用**              |            **示例**            |
   | :--------: | :-------------------------------: | :----------------------------: |
   |  .number   |  自动将用户的输入值转为数值类型   | <input v-model.number="age" /> |
   |   .trim    |  自动过滤用户输入的首尾空白字符   |  <input v-model.trim="msg" />  |
   |   .lazy    | 在 “change” 时而非 “input” 时更新 |  <input v-model.lazy="msg" />  |

   

6. ####  条件渲染指令

   条件渲染指令用来辅助开发者<font color="red">按需控制 DOM 的显示与隐藏</font>。条件渲染指令有如下两个，分别是：

   - <font color="red">**v-if**</font>

     v-if 可以单独使用，或配合 <font color="red">**v-else**</font> 指令一起使用; <font color="red">**v-else-if**</font> 指令，顾名思义，充当 v-if 的“else-if 块”，可以连续使用：

     ```html
     <div id="app">
         <div v-if="type === 'A'">优秀</div>
         <div v-else-if="type === 'B'">良好</div>
         <div v-else-if="type === 'C'">一般</div>
         <div v-else>差</div>
     </div>
     <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
     <script>
         const vm = new Vue({
             el: '#app',
             data: {
                 type: 'A'
             }
         })
     </script>
     ```

     

   - <font color="red">**v-show**</font>

   ```html
   <div id="app">
       <p v-if="flag">被 v-if 控制的元素</p>
       <p v-show="flag">被 v-show 控制的元素</p>
   </div>
   
   <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
   <script>
       const vm = new Vue({
           el: '#app',
           data: {
               flag: true
           }
       })
   </script>
   ```

   

   ##### v-if 和 v-show 的区别

   - 实现原理不同

     - v-if 指令会<font color="red">动态地创建或移除 DOM 元素</font>，从而控制元素在页面上的显示与隐藏；
     - v-show 指令会动态为元素<font color="red">添加或移除 style="display: none;" 样式</font>，从而控制元素的显示与隐藏；

   - 性能消耗不同

     v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此：

     - 如果需要<font color="red">非常频繁地切换</font>，则使用 v-show 较好
     - 如果在<font color="red">运行时条件很少改变</font>，则使用 v-if 较好

   

7. ####  列表渲染指令

   vue 提供了 <font color="red">**v-for**</font> 列表渲染指令，用来辅助开发者<font color="red">基于一个数组来循环渲染一个列表结构</font>。v-for 指令需要使用 <font color="red">item in items</font> 形式的特殊语法，其中：

   - items 是待循环的数组
   - item 是被循环的每一项

   ```html
   data: {
   	list: [
   		{ id: 1, name: 'zs' }
   		{ id: 2, name: 'ls' }
   	]
   }
   //-------------------------------------
   <ul>
   	<li v-for="item in list">姓名是：{{ item.name }}</li>
   </ul>
   ```

   v-for 指令还支持一个可选的第二个参数，即当前项的<font color="red">索引</font>。语法格式为 (item, index) in items，示例代码如下：

   ```html
   data: {
   	list: [
   		{ id: 1, name: 'zs' }
   		{ id: 2, name: 'ls' }
   	]
   }
   //-------------------------------------
   <ul>
   	<li v-for="(item, index) in list">索引是：{{ index }}，姓名是：{{ item.name }}</li>
   </ul>
   ```

   

   ##### <font color="red">使用 key 维护列表的状态</font>

   当列表的数据变化时，默认情况下，vue 会尽可能的复用已存在的 DOM 元素，从而提升渲染的性能。但这种默认的性能优化策略，会导致有状态的列表无法被正确更新。

   为了给 vue 一个提示，以便它能跟踪每个节点的身份，从而在保证有状态的列表被正确更新的前提下，提升渲染的性能。此时，需要为每项提供一个唯一的 <font color="red">**key**</font> 属性：

   ```html
   <ul>
     <li v-for="item in items" :key="item.id">
     	<input type="checkbox" />
       姓名：{{ item.name }}
     </li>
   </ul>
   ```

   

   ##### key 的注意事项

   - key 的值只能是<font color="red">字符串或数字类型</font>
   - key 的值必须具有<font color="red">唯一性</font>（即：key 的值不能重复）
   - 建议把数据项 <font color="red">id 属性的值作为 key 的值</font>（因为 id 属性的值具有唯一性）
   - 使用 index 的值当作 key 的值没有任何意义（因为 index 的值不具有唯一性）
   - 建议<font color="red">使用 v-for 指令时一定要指定 key 的值</font>（既提升性能、又防止列表状态紊乱）