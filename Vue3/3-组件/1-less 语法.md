# less 语法

#### 让 style 中支持 less 语法

如果希望使用 less 语法编写组件的style 样式，可以按照如下两个步骤进行配置：

- 运行 `npm i less -D` 命令安装依赖包，从而提供 less 语法的编译支持
- 在 `<style>` 标签上添加 `lang="less"` 属性，即可使用 less 语法编写组件的样式