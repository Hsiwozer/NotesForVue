# Vuex 的核心概念

1. #### State

   State 提供唯一的公共数据源，<font color="red">所有共享的数据</font>都要统一放到 Store 的 State 中进行<font color="red">存储</font>。

   ```js
   const store = new Vuex.Store({
     state: { count: 0 }
   })
   ```

   ##### 组件访问 State 中数据的两种方式：

   ```vue
   // 方式一
   <h3>当前最新的 count 值为：{{ $store.state.count }}</h3>
   
   // 方式二
   // 1. 从 vuex 中按需导入 mapState 函数
   import { mapState } from 'vuex'
   // 2. 将全局数据映射为当前组件的计算属性
   computed: {
   	...mapState(['count'])
   }
   //3. 使用数据
   <h3>当前最新的 count 值为：{{ count }}</h3>
   ```

   

2. #### Mutation

   Mutation 用于<font color="red">变更 Store 中的数据</font>。

   - 只能通过 Mutation 变更 Store 中的数据，不可以直接操作 Store 中的数据。
   - 通过这种方式虽然操作起来较为繁琐，但是可以集中监控所有数据的变化。

   ```js
   // 定义 Mutation
   mutations: {
     add(state) {
       state.count++
     }
   }
   
   // 触发 Mutation
   methods: {
     handler1() {
       this.$store.commit('add')
     }
   }
   ```

   ##### 当然，可以在触发 Mutation 时携带参数：

   ```js
   mutations: {
     addN(state, step) {
       state.count += step
     }
   }
   
   methods: {
     handler1() {
       this.$store.commit('add', 2)
     }
   }
   ```

   ##### 触发 Mutation 的两种方式：

   ```
   handler1() {
       this.$store.commit('add', 2)
     }// 方式一
   this.$store.commit()
   
   // 方式二
   // 1. 从 vuex 中按需导入 mapMutations 函数
   import { mapMutations } from 'vuex'
   // 2. 将全局数据映射为当前组件的 methods 方法
   // 3. 使用函数
   methods: {
   	...mapMutations(['add', 'addN']),
   	handler1() {
       this.add()
     },
     handler3() {
       this.addN(3)
     }
   }
   
   // *或者直接在标签中使用函数
   <button @click="add">+1</button>
   <button @click="addN(3)">+N</button>
   ```

   ###### 注意：Mutation 中不能执行异步操作！

3. #### Action

   Action 用于<font color="red">处理异步任务</font>。

   ```js
   // 定义 Action
   mutations: {
     add(state) {
       state.count++
     }
   },
   actions: {
     addAsync(context) {
       setTimeout(() => {
         context.commit('add')
       }, 1000)
     }
   }
   
   // 触发 Action
   methods: {
     handle() {
       this.$store.dispatch('addAsync')
     }
   }
   ```

   ##### 当然，可以在触发 Action 时携带参数：

   ```js
   mutations: {
     add(state, step) {
       state.count += step
     }
   },
   actions: {
     addAsync(context, step) {
       setTimeout(() => {
         context.commit('add', step)
       }, 1000)
     }
   }
   
   methods: {
     handle() {
       this.$store.dispatch('addAsync', 5)
     }
   }
   ```

   ##### 触发 Action 的两种方式：

   ```
   // 方式一
   this.$store.dispatch()
   
   // 方式二
   // 1. 从 vuex 中按需导入 mapActions 函数
   import { mapActions } from 'vuex'
   // 2. 将全局数据映射为当前组件的 methods 方法
   // 3. 使用函数
   methods: {
   	...mapActions(['addAsync', 'addNAsync']),
   	handlerAsync1() {
       this.addAsync()
     },
     handlerAsync2() {
       this.addNAsync(5)
     }
   }
   
   // *或者直接在标签中使用函数
   <button @click="addAsync">+1</button>
   <button @click="addNAsync(3)">+N</button>
   ```

   

4. #### Getter

   Getter 用于对 Store 中的数据进行<font color="red">加工处理</font>形成新的数据。

   - 类似于 vue 中的计算属性。
   - Store 中的数据发生变化时，Getter 中的数据也会跟着发生变化。

   ```js
   // 定义 Getter
   state: {
     count: 0
   },
   getters: {
     showNum: state => {
       return '当前最新的数据是' + state.count
     }
   }
   
   // 使用 getters 的两种方式
   // 方式一
   <h3>{{ this.$store.getters.showNum }}</h3>
   
   // 方式二
   import { mapGetters } from 'vuex'
   computed: {
     ...mapGetters(['showNum'])
   }
   <h3>{{ showNum }}</h3>
   ```

   

5. #### Module

   