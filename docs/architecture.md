# 整体架构

## 项目文件
- src 项目源码
  - assets 资源文件
  - components 组件
    - blocks 节点块框架
    - views 节点块内容
    - controls 参数控件
    - BaseItem.vue 模板节点块
    - BlockPanel.vue 中部工作区域
    - LeftBar.vue 左侧模板块栏
    - SettingDiloag.vue 参数设置弹窗
    - TagBar.vue 标签（任务）栏
  - router 路由
  - store 状态管理
  - styles 样式文件
  - views 视图页面
    - Home.Vue 主页面
  - App.vue VUE主文件
  - background.js electon自动生成文件
  - main.js 程序入口文件

## 模块

<div align=center>
<img src="_images/module.svg" />
</div>

- **节点块** 简称为**块(Block)** ，用于数据可视化及处理操作。
- **状态管理模式** 用于储存每个块的数据及软件全局信息。
- **用户工作区** 实现用户打开任务、添加模块等基本操作。
- **参数设置** 用于修改节点块的属性及参数。

## 块与其他模块的关系

<div align=center>
<img src="_images/block-connection.svg" />
</div>

块控件通过**状态管理模式**注入块数据，通过**混入(Mixin)** 方式加载逻辑功能，块采用**双向数据流**，能够对注入的数据直接进行修改，每个块可以直接向下级块传输数据。参数控件为**单例模式(Singleton)** ，块通过设置事件打开参数控件。上级工作区通过状态管理模式添加、删除节点块数据。

## 块继承