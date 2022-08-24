# vue 组件

1. #### **什么是组件化开发**

   组件化开发指的是：根据<font color="red">封装</font>的思想，<font color="red">把页面上可重用的 UI 结构封装为组件</font>，从而方便项目的开发和维护。

2. #### **vue** **中的组件化开发**

   vue 是一个支持组件化开发的前端框架。

   vue 中规定：组件的后缀名是 .vue。之前接触到的 App.vue 文件本质上就是一个 vue 的组件。

3. ####  **vue** **组件的三个组成部分**

   每个 .vue 组件都由 3 部分构成，分别是：

   - <font color="red">template</font> -> 组件的<font color="red">模板结构</font>

     - vue 规定：每个组件对应的模板结构，需要定义到 `<template>` 节点中。
     - template 是 vue 提供的容器标签，只起到包裹性质的作用，它不会被渲染为真正的 DOM 元素
     - template 中只能包含唯一的根节点（<u>仅 v2 中，v3 中无此限制</u>）

   - <font color="red">script</font> -> 组件的 <font color="red">JavaScript 行为</font>

     - vue 规定：开发者可以在 `<script>` 节点中封装组件的 JavaScript 业务逻辑。
     - vue 规定：.vue 组件中的 data 必须是一个函数，不能直接指向一个数据对象。

   - <font color="red">style</font> -> 组件的<font color="red">样式</font>

     - vue 规定：组件内的 `<style>` 节点是可选的，开发者可以在 `<style>` 节点中编写样式美化当前组件的 UI 结构。

     - **让** **style** **中支持** **less** **语法**：在 `<style>` 标签上添加 lang="less" 属性，即可使用 less 语法编写组件的样式

       ```vue
       <style lang="less">
       .test-box {
           background-color: pink;
           h3 {
               color: red;
           }
       }
       </style>
       ```

       

   其中，<font color="red">**每个组件中必须包含 template 模板结构**</font>，而 script 行为和 style 样式是可选的组成部分。

   ```vue
   <template>
       <div class="test-box">
           <h3>这是自定义的 Test.vue --- {{ username }}</h3>
       </div>
   </template>
   
   <script>
   // 默认导出，固定写法
   export default {
       data() {
           return { username: "admin" };
       },
   };
   </script>
   
   <style>
   .test-box {
       background-color: pink;
   }
   </style>
   ```

   

4. ####  组件之间的父子关系

   - ##### 使用组件的三个步骤

     ###### 均在父组件（App.vue）中完成

     - 步骤1：使用 import 语法导入需要的组件

       ```js
       import Left from "@/components/Left";
       import Right from "@/components/Right";
       ```

       

     - 步骤2：使用 components 节点注册组件

       ######  **通过** **components** 注册的是私有子组件

       ```js
       export default {
           components: {
               Left,
               Right,
           },
       };
       ```

       

     - 步骤3：以标签形式使用刚才注册的组件

       ```html
       <Left></Left>
       <Right></Right>
       ```

       

   - ##### 注册全局组件

     在 vue 项目的 **main.js** 入口文件中，通过 Vue.component() 方法，可以注册全局组件。

     ```js
     import Count from "@/components/Count.vue";
     Vue.component("MyCount", Count);
     ```

     

5. #### 组件的 props

   props 是组件的自定义属性，在封装通用组件的时候，合理地使用 props 可以极大的提高组件的复用性！

   ```js
   export default {
       // props 是自定义属性，允许使用者通过自定义属性，为当前组件指定初始值
       props: ["init"],
       data() {
           return {};
       },
   };
   ```

   - ##### props 是只读的

     vue 规定：组件中封装的自定义属性是只读的，程序员不能直接修改 props 的值，否则会直接报错。

     要想修改 props 的值，可以把 props 的值转存到 data 中，因为 data 中的数据都是可读可写的！

     ```js
     props: ["init"],
     data() {
         return {
             count: this.init,
         };
     },
     ```

     

   - ##### **props** **的** **default** 默认值

     在声明自定义属性时，可以通过 default 来定义属性的默认值。

     ```js
     props: {
         init: {
             // 如果外界使用 count 时，没有传入 init 值，则 default 生效
             default: 6,
         },
     },
     ```

     

   - ##### **props** **的** **type** 值类型

     在声明自定义属性时，可以通过 type 来定义属性的值类型。

     ```js
     props: {
         init: {
             default: 6,
             type: Number,
         },
     },
     ```

     

   - ##### **props** **的** **required** 必填项

     在声明自定义属性时，可以通过 required 选项，将属性设置为必填项，强制用户必须传递属性的值。

     ```js
     props: {
         init: {
             default: 6,
             type: Number,
             required: true,
         },
     },
     ```

     

6. ####  **组件之间的样式冲突问题**

   默认情况下，写在 .vue 组件中的样式会<font color="red">全局生效</font>，因此很容易造成<font color="red">多个组件之间的样式冲突问题</font>。

   导致组件之间样式冲突的根本原因是：

   - 单页面应用程序中，所有组件的 DOM 结构，都是基于<font color="red">唯一的 index.html 页面</font>进行呈现的
   - 每个组件中的样式，都会影响<font color="red">整个 index.html 页面中的 DOM 元素</font>

   

   ##### 🔧解决方案

   - **style** **节点的** **scoped** **属性**

     为了提高开发效率和开发体验，vue 为 style 节点提供了 scoped 属性，从而防止组件之间的样式冲突问题：

     ```vue
     <style scoped>
       /* style 节点的 scoped 属性，用来自动为每个组件分配唯一的“自定义属性”，
       	并自动为当前组件的 DOM 标签和 style 样式应用这个自定义属性，防止组件的样式冲突问题*/
       .container {
         border: 1px solid red;
       }
     </style>
     ```

     

   - **/deep/** **样式穿透**

     如果给当前组件的 style 节点添加了 scoped 属性，则当前组件的样式<font color="red">对其子组件是不生效的</font>。如果想让某些样式对子组件生效，可以使用 /deep/ 深度选择器。

     ```vue
     <style scoped>
       /deep/ .container {
         border: 1px solid red;
       }
     </style>
     ```

     

