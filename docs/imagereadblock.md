# 图像读取控件

图像读取控件实现图像读取功能。

---
## 父级控件
- [InputBlock](inputblock.md)

---
## 混入
- [BaseMixin](baseblock.md#basemixin)
- [InputMixin](inputblock.md#inputmixin)

---
## 组件

### 文件列表 
[FileList](filelist.md) 用于显示当前选择的文件。

---
## 监听
- [`start`](inputblock.md#start) 事件   
  绑定 [`start()`](#async-start-gt-void) 回调函数
- [`stop`](inputblock.md#stop) 事件

---
## 方法

### async start() -> `void`
开始读取图像，并发送给下一级。
