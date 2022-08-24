# props 验证之自定义验证函数

##### 在封装组件时，可以为 prop 属性指定自定义的验证函数，从而对 prop 属性的值进行更加精确的控制。

```js
export default {
  props: {
    // 通过“配置对象”的形式，来定义 porpA 属性的”验证规则“
    propA: {
      // 通过 validator 函数，对 propA 属性的值进行校验，”属性的值“可以通过形参 value 进行接收
      validator (value) {
        // propA 属性的值，必须匹配下列字符串中的一个
        // validator 函数的返回值为 true 表示验证通过，false 表示验证失败
        return ['success', 'warning', 'danger'].indexOf(value) !=== -1
      }
    },
  },
}
```

