# HTTP服务器请求块

## pos
> 参考[pos](taskconfig.md#pos-objectx-int-y-int-w-int-h-int-z-int-require)。

## props
> 参考[属性](taskconfig.md#属性（参数）)。

### autoStart: `Bool` *require*
当收到上级数据包时是否自动向服务器发送。

**示例**
```json
"autoStart": {
    "name": "自动运行",
    "type": "el-checkbox",
    "value": true
}
```

### address: `String` *require*
服务器地址。

**示例**
```json
"address": {
    "name": "服务器地址",
    "type": "el-input",
    "value": "http://127.0.0.1:7777"
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