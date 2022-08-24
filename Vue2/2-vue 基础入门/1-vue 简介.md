# vue 简介

#### [官方文档 vue.js https://cn.vuejs.org](https://cn.vuejs.org)

1. #### 什么是 vue？

   一套用于<font color="red">构建用户界面</font>的前端<font color="red">框架</font>。

2. #### 两个特性

   - ##### <font color="red">数据驱动视图</font>

     在使用了 vue 的页面中，vue 会**监听数据的变化**，从而**自动**重新渲染页面的结构。

     注意：数据驱动视图是单向的数据绑定！

   - ##### <font color="red">双向数据绑定</font>

     在**填写表单**时，双向数据绑定可以辅助开发者在**不操作 DOM** 的前提下，自动把用户填写的内容**同步到**数据源中。因此，开发者不需要手动操作 DOM 元素，来获取表单元素最新的值。

3. #### MVVM

   MVVM 是 vue 实现数据驱动视图和双向数据绑定的核心原理。MVVM 指的是 Model、View 和 ViewModel，它把每个 HTML 页面都拆分成了这三个部分。

   在MVVM 概念中：

   - <font color="red">**Model**</font> 表示当前页面渲染时所依赖的数据源。
   - <font color="red">**View**</font> 表示当前页面所渲染的 DOM 结构。
   - <font color="red">**ViewModel**</font> 表示 vue 的实例，它是 MVVM 的核心。

   **工作原理：** ViewModel 作为 MVVM 的核心，是它把当前页面的数据源（Model）和页面的结构（View）连接在了一起。当数据源发生变化时，会被 ViewModel 监听到，VM 会根据最新的数据源自动更新页面的结构；当表单元素的值发生变化时，也会被 VM 监听到，VM 会把变化过后最新的值自动同步到 Model 数据源中。