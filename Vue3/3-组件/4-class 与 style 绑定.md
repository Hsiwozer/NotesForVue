# class 与 style 绑定

1. #### 动态绑定 HTML 的 class

   可以通过<font color="red">三元表达式</font>，动态的为元素绑定 class 的类名。

   ```vue
   <h3 class="thin" :class="isItalic ? 'italic' : ''">MyDeep 组件</h3>
   <button @click="isItalic=!isItalic">Toogle Italic</button>
   
   data() {
   	return { isItalic: true }
   }
   
   .thin {
   	font-weight: 200;
   }
   
   .italic {
   	font-style: italic;
   }
   ```

   

2. #### 以<font color="red">数组语法</font>绑定 HTML 的 class

   如果元素需要动态绑定多个 class 的类名，此时可以使用数组的语法格式：

   ```vue
   <h3 class="thin" :class="[isItalic ? 'italic' : '', isDelete: false, ? 'delete' : '']">MyDeep 组件</h3>
   
   <button @click="isItalic=!isItalic">Toogle Italic</button>
   <button @click="isDelete=!isDelete">Toogle Delete</button>
   
   data() {
   	return { 
   		isItalic: true,
   		isDelete: false,
   	}
   }
   ```

   

3. #### 以<font color="red">对象语法</font>绑定 HTML 的 class

   使用<font color="red">数组语法</font>动态绑定 class 会<font color="red">导致模板结构臃肿</font>的问题。此时可以使用对象语法进行简化：

   ```vue
   <h3 class="thin" :class="classObj">MyDeep 组件</h3>
   
   <button @click="classObj.isItalic=!classObj.isItalic">Toogle Italic</button>
   <button @click="classObj.isDelete=!classObj.isDelete">Toogle Delete</button>
   
   data() {
   	return { 
   		classObj: {
   			isItalic: true,
   			isDelete: false,
   		}
   	}
   }
   ```

   

4. #### 以<font color="red">对象语法</font>绑定内联的 style

   style 的对象语法十分直观——看着非常像CSS，但其实是一个 Javascript 对象。CSS property 名可以用驼峰式 (camelcase) 或短横线分隔（kebab-case，记得用引号括起来）来命名：

   ```vue
   <div :style="{color: active, fontSize: fsize + 'px', 'background-color': bgcolor}">
   	黑马程序员
   </div>
   <button @click="fsize += 1">字号 +1</button>
   <button @click="fsize 1= 1">字号 -1</button>
   
   data() {
   	return {
   		active: 'red',
   		fsize: 30,
   		bgcolor: 'pink',
   	}
   }
   ```

   