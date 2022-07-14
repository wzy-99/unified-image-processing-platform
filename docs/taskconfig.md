# 任务配置文件

任务配置文件是具有规范格式的Json文件，其内容包含了各级块和任务的名称等。

## 字段
任务配置文件包含`name`、`blockList`字段。

### name: `String` *require*
任务的名称。

### blockList: `Array[Object]` *require*
任务的所有块，详见[任务块](#任务块)。

**注意** *require* 表明该字段是必须的

---
## 任务块
每个块必包含`id`、`type`、`pos`、`prop`字段，可能包含`param`字段。

### id: `Int` *require*
块的全局唯一标识。

### type: `String` *require*
块的控件类型，用于构建vue组件。  

### pos: `Object{x: Int, y: Int, w: Int, h: Int, z: Int}` *require*
块的布局, 其中`x`为块的横坐标，`y`为块的纵坐标，`w`为块的宽度，`h`为块的高度，`z`为块的[层级](https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index)。

### prop: `Object` *require*
块的属性，如块的下一级、块的服务器地址等，详见[属性](#属性（参数）)。

### pram: `Object`
块向服务器发送的参数，如模型的置信率阈值参数等，详见[参数](#属性（参数）)。

## 属性（参数）
属性（参数）包含`name`、`type`、`value`、`extra`字段。

### name: `String` *require*
属性（参数）的名称。

### type: `String` *require*
属性（参数）的控件类型。

### value: `Object | Number | String | Array` *require*
属性（参数）的值。

### extra: `Object`
属性（参数）的控件的额外设置，如参数上限、参数下限、是否检查等。

## 示例
```json
{
    "name": "图像测试",
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
        }
    ]
}
```