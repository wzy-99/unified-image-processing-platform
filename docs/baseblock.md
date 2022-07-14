# 基础块控件

基础块控件实现了块的**整体布局**，并实现了`拖拽`、`调整大小`、`设置参数`等基本功能。

---
## 混入
- [BaseMixin](#basemixin)

---
## 组件

### 设置按键

用于设置块的属性与参数。  

当点击时，触发[`setting`](#setting)事件，并弹出设置窗口，用于选中块参数及属性的设置。

---
## 事件

### dragging

块控件在拖拽中触发`dragging`事件，事件参数为：拖动后的横坐标`x`、拖动后的纵坐标`y`（像素）。

### resizing

块控件在调整大小中触发`resizing`事件，事件参数为：调整后的横坐标`x`、拖动后的纵坐标`y`、调整后的宽度`w`、调整后的纵坐标`h`（像素）。

### setting

点击块控件的设置按钮时触发`setting`事件，无事件参数。

---
# BaseMixin

### tagIndex: `Int`
当前tag在数组中的索引

**示例**
```js
  tags = [tag1, tag2]
  tag1 = [block1, block2, block3]
  tag2 = [block3, block4, block5]
  // if current block is block2
  // then tagIndex = 0
``` 

### index: `Int`
当前block在数组中的索引

**示例**
```js
  tags = [tag1, tag2]
  tag1 = [block1, block2, block3]
  tag2 = [block3, block4, block5]
  // if current block is block5
  // then index = 3
```

### name: `String`
当前block的名称  

**示例**
```js
  name = "baseblock"
```

### tag: `Object`
当前tag数据对象

**示例**
```js
  tag = {name:"", blockList:[]}
```

### block: `Object`
当前block数据对象

**示例**
```js
  block = {id:"", type:"", pos:{}, prop:{}, temp:{}, ...}
```

### buffer: `Array[Object]`
缓冲区，用于储存接收的数据

---
### cycleBuffer: `Bool`
是否采用环形缓冲区。当采用环形缓冲区，缓冲区数据填满后自动释放最早的一个数据包。

### autoClear: `Bool`
是否允许上级块自动清除此块的清除缓冲区。

### nextID: `Array[Int]`
下一级块ID

**示例**
```js
  nextID = [2, 3]
```

### content: `Object`
content具名槽中的Vue对象

### cleanNext(ids: `Array[Int]`) -> `void`
请求下一级块清空的缓冲区。参数ids为下一级块的ID数组，ids缺省情况下为此块所有直接下级块的ID。

**示例**
```js
  cleanNext() // 清空所有直接下级块的缓冲区
  cleanNext([2, 3]) // 清空ID为2和ID为3的块的缓冲区
```

### clear() -> `void`

清空缓冲区`buffer`

### process() -> `void`

用于处理数据的虚函数，需要子级实现

### async recv(pack: `Object`) -> `void`

接收一个数据包，如果缓冲区已满，根据情况进行等待或释放。

### post(pack: `Array[Object]`, ids: `Array[Int]`) -> `void`

发送一个数据给下一级。参数pack为数据包，ids为下一级块的ID数组，ids缺省情况下为此块所有直接下级块的ID

### newPack(data: `Object`, type: `String`, result: `Array`, id: `Int`) -> `Object`

生成一个新的包。参数data为包数据，type为数据类型，result为处理结果，result缺省情况下为一个空数组，id为全局标识，id缺省情况下自动生成