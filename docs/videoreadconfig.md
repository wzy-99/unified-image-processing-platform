# 视频读取块

## pos
> 参考[pos](taskconfig.md#pos-objectx-int-y-int-w-int-h-int-z-int-require)。

## props
> 参考[属性](taskconfig.md#属性（参数）)。

### input: `Array[Object]` *require*
输入列表。

**示例**
```json
"input": {
    "name": "输入文件",
    "type": "file-list",
    "value": [],
    "extra": {
        "fileType": "video/*"
    }
}
```

### next: `Array[Int]` *require*
下一级ID列表。

**示例**
```json
"next": {
    "name": "下一级",
    "type": "node-select",
    "value": [
        2
    ]
}
```