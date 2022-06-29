# 基础块

Baseblock 是所有块的基类，其实现了拖拽、调整大小等基本功能，实现发送、接收、清除等方法，提供块数据、块接收区、下级块ID等属性，包括拖拽、调整大小、设置等事件。

## 属性

### tagIndex
  当前block所在tag的索引

### index
  当前block在tag中的索引

### name
  名称

### tag
  tag数据实例

### block
  block数据实例

### bufferMaxLength
  最大接收区长度，默认为100

### nextID
  下一级块ID

### isTopBlock
  是否是应用块

### content
  content槽对象

## 方法

## 事件

### dragging
拖拽事件
- 新横坐标x
- 新纵坐标y

### resizing
拖拽事件
- 新横坐标x
- 新纵坐标y
- 新宽度w
- 新高度h

### setting
设置事件