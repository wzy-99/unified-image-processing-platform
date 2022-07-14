# 任务配置文件

任务配置文件是具有规范格式的Json文件，其内容包含了各级块和任务的名称等。

## 字段
任务配置文件包含`name`、`blockList`三个字段。

### name: `String` required
任务的名称

### blockList: `Array[Object]` required
任务的所有块

**注意** require 表明该字段是必须的

---
## 任务块
每个块必包含`id`、`type`、`pos`、`prop`字段，可能包含`param`字段。

### id: `Int` require
块的全局唯一标识

### type: `String` require
块的控件类型，用于构建vue组件。

```html
<!-- BlockPanel.vue -->
<!-- component 为Vue模板组件，提供将type属性传入is，实现组件的实例化 -->
<component
    v-for="(block, index) in tag.blockList"
    :is="block.type"
    :index="index"
    :tagIndex="tagIndex"
/>
```
### pos: `Object{x: Int, y: Int, w: Int, h: Int, z: Int}` require
块的布局, 其中`x`为块的横坐标，`y`为块的纵坐标，`w`为块的宽度，`h`为块的高度，`z`为块的[层级](https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index)。

### prop: `Object` require
块的属性，如块的下一级、块的服务器地址等。

### pram: `Object`
块向服务器发送的参数，如模型的置信率阈值参数等。

**注意** require 表明该字段是必须的

## 示例

```json
{
    "name": "图像测试",
    "temp": {},
    "blockList": [
        {
            "id": 1,
            "type": "image-read-block",
            "pos": {
                "x": 0,
                "y": 0,
                "w": 400,
                "h": 200,
                "z": 10
            },
            "prop": {
                "input": {
                    "name": "输入文件",
                    "type": "file-list",
                    "value": [],
                    "extra": {
                        "fileType": "image/*"
                    }
                },
                "next": {
                    "name": "下一级",
                    "type": "node-select",
                    "value": [
                        2
                    ]
                }
            },
            "temp": {}
        },
        {
            "id": 2,
            "type": "http-request-block",
            "pos": {
                "x": 0,
                "y": 200,
                "w": 400,
                "h": 200,
                "z": 10
            },
            "prop": {
                "autoStart": {
                    "name": "自动运行",
                    "type": "el-checkbox",
                    "value": true
                },
                "next": {
                    "name": "下一级",
                    "type": "node-select",
                    "value": [
                        3, 4
                    ]
                },
                "address": {
                    "name": "服务器地址",
                    "type": "el-input",
                    "value": "http://127.0.0.1:7777"
                },
                "batchSize": {
                    "name": "一次发送量",
                    "type": "el-input-number",
                    "value": 1,
                    "extra": {
                        "clearable": true
                    }
                }
            },
            "param": {
                "height": {
                    "name": "图像高度",
                    "type": "el-input",
                    "value": 256,
                    "extra": {
                        "clearable": true
                    }
                },
                "width": {
                    "name": "图像宽度",
                    "type": "el-input",
                    "value": 256
                }
            },
            "temp": {}
        },
        {
            "id": 3,
            "type": "image-visual-block",
            "pos": {
                "x": 400,
                "y": 200,
                "w": 400,
                "h": 200,
                "z": 11
            },
            "prop": {},
            "temp": {}
        },
        {
            "id": 4,
            "type": "image-roi-block",
            "pos": {
                "x": 0,
                "y": 400,
                "w": 400,
                "h": 200,
                "z": 10
            },
            "prop": {
                "next": {
                    "name": "下一级",
                    "type": "node-select",
                    "value": [
                        5
                    ]
                },
                "supportAll": {
                    "name": "对所有感标签兴趣",
                    "type": "el-checkbox",
                    "value": true
                },
                "ROILabels": {
                    "name": "感兴趣的标签",
                    "type": "el-select",
                    "value": []
                }
            },
            "temp": {}
        },
        {
            "id": 5,
            "type": "image-visual-block",
            "pos": {
                "x": 400,
                "y": 400,
                "w": 400,
                "h": 200,
                "z": 11
            },
            "prop": {},
            "temp": {}
        }
    ]
}
```