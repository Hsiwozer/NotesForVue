# npm 装包失败分析与解决

1. 在导入Vue项目使用 ' npm i ' 安装node_moduels的时候，终端出现错误如下：

   ![image-20220817144724167](./images/image-20220817144724167.png)

   ⚠️ <font color="red"> **问题定位：**</font>**Cannot read properties of null (reading 'pickAlgorithm')**

   🧰 <font color="green">**解决方法：**</font>在终端输入： `npm cache clear --force`，然后重新运行 `npm i` 命令