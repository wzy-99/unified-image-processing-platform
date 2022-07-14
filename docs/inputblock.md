# 输入块控件
所有输入类型块的继承控件。

---
## 父级控件
- [BaseBlock](baseblock.md)

---
## 混入
- [BaseMixin](baseblock.md#basemixin)
- [InputMixin](inputblock.md#inputmixin)

---
## 组件

### 启动按键

用于开始处理输入。  

当点击时，触发[`start`](#start)事件。

### 停止按键

用于停止处理输入。

当点击时，触发[`stop`](#stop)事件。

---
## 事件

### start

当启动按键被点击时触发，无事件参数。

### stop

当停止按键被点击时触发，无事件参数。

---
# InputMixin

### isRunning: `Bool`
是否正在处理输入

### files: `Array[Object]`
输入文件列表

### readFileAsync(file: `File`) -> `ArrayBuffer`
同步读取文件，参数file为[File](https://developer.mozilla.org/zh-CN/docs/Web/API/File)类型对象。

**示例**
```js
let contentBuffer = await this.readFileAsync(file.raw) // file.raw为File类型
```