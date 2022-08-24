# ref 引用

1. #### **什么是** **ref** **引用**

   ref 用来辅助开发者在<font color="red">不依赖于 jQuery 的情况下</font>，获取 DOM 元素或组件的引用。

   每个 vue 的组件实例上，都包含一个 <font color="red">$refs 对象</font>，里面存储着对应的 DOM 元素或组件的引用。

   默认情况下，<font color="red">组件的 $refs 指向一个空对象</font>。

2. #### **使用** **ref** **引用** **DOM** **元素**

   如果想要使用 ref 引用页面上的 DOM 元素，则可以按照如下的方式进行操作：

   ```vue
   <h1 ref="myh1">App 根组件</h1>
   <button @click="changeColor">更改字体颜色</button>
   
   methods: {
       changeColor() {
           this.$refs.myh1.style.color = "red";
       },
   },
   ```

   

3. #### **使用** **ref** **引用组件实例**

   如果想要使用 ref 引用页面上的组件实例，则可以按照如下的方式进行操作：

   ```vue
   <Left ref="comLeft"></Left>
   
   onReset() {
       this.$refs.comLeft.count = 0;
   },
   ```

   

4. ####  this.$nextTick(cb) **方法**

   组件的 $nextTick(cb) 方法，会把 cb 回调推迟到下一个 DOM 更新周期之后执行。通俗的理解是：等组件的DOM 更新完成之后，再执行 cb 回调函数。从而能保证 cb 回调函数可以操作到最新的 DOM 元素。

   ```vue
   <input type="text" v-if="inputVisible" ref="iptRef" />
   <button v-else @click="showInput">展示 input 输入框</button>
   
   methods: {
   	showInput() {
   		this.inputVisible = true;
   		// 把对 input 文本框的操作，推迟到下次 DOM 更新之后，否则页面上根本不存在文本框元素
   		this.$nextTick(() => {
   			this.$refs.iptRef.focus()
   		})
   	}
   }
   ```