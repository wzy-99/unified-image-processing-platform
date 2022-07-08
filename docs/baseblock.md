# 基础块控件

基础块控件实现了块的**整体布局**，并实现了`拖拽`、`调整大小`、`设置参数`等基本功能。

---
## 组件

### 设置按键

用于设置块的属性与参数。  

当点击时，弹窗设置窗口，用于选中块参数及属性的设置。

---
## 事件

### 拖拽

块控件在拖拽中触发`dragging`事件，事件参数为：拖动后的横坐标`x`、拖动后的纵坐标`y`（像素）。

### 调整大小

块控件在调整大小中触发`resizing`事件，事件参数为：调整后的横坐标`x`、拖动后的纵坐标`y`、调整后的宽度`w`、调整后的纵坐标`h`（像素）。

### 设置

点击块控件的设置按钮时触发`setting`事件，无事件参数。

---
# 基础块混入

## 控件属性选项

### tagIndex
  整数，当前tag在数组中的索引

**示例**
```js
  tags = [tag1, tag2]
  tag1 = [block1, block2, block3]
  tag2 = [block3, block4, block5]
  // if current block is block2
  // then tagIndex = 0
``` 

### index
  整数，当前block在数组中的索引

**示例**
```js
  tags = [tag1, tag2]
  tag1 = [block1, block2, block3]
  tag2 = [block3, block4, block5]
  // if current block is block5
  // then index = 3
```

### name
字符串，当前block的名称  

**示例**
```js
  name = "baseblock"
```

### tag
对象，当前tag数据对象

**示例**
```js
  tag = {name:"", blockList:[]}
```

### block
对象，当前block数据对象

**示例**
```js
  block = {id:"", type:"", pos:{}, prop:{}, temp:{}, ...}
```

### buffer
数组，缓冲区

### isTopBlock
布尔，是否为最外层block

## 功能选项

### nextID
下一级块ID

### isTopBlock
  是否是应用块

### content
  content槽对象