# 如何开发块

> 以ImageReadBlock.vue为例。



## 步骤

1. 引入上级组件

```js
import FileList from "@/components/controls/FileList";

export default {
  components: {
    "input-block": InputBlock, // 上级InputBlock控件
  },
}
```

2. 引入混入

[混入](https://cn.vuejs.org/v2/guide/mixins.html)用于实现功能的复用。

```js
import BaseMixin from "@/components/blocks/BaseMixin.js";
import InputMixin from "@/components/blocks/InputMixin.js";

export default {
  mixins: [...BaseMixin, ...InputMixin], // ...为展开运算符
}
```

3. 开发界面

```html
<template>
<!-- 首先引入上级组件input-block -->
<input-block :index="index" :tagIndex="tagIndex" @start="start" @stop="stop">
    <!-- 上级控件提供了content内容槽，因此可以在content内自定义控件 -->
    <template v-slot:content> 
    <!-- 添加自定义控件 file-list 文件列表 -->
    <file-list v-model="files" :drag="false"> </file-list>
    </template>
</input-block>
</template>
```

4. 实现相应的逻辑

```js
export default {
    methods: {
        // 实现开始方法
        async start() {
            this.isRunning = true
            // 自动清除下级内容
            if (this.autoClear) {
                this.cleanNext()
            }
            for (const file of this.files) {
                let contentBuffer = await this.readFileAsync(file.raw) 
                let pack = this.newPack(contentBuffer, "imageFile")
                await this.post(pack)
            }
            this.isRunning = false
        },
    },
}
```

# 如何开发混入

> 以InputMixin.js为例

混入分为两部分，一部分是基础**属性的开发**(InputPropertyMixin)，一部分是子级应用块**功能的开发**(InputFunctionMixin)。

## 步骤

1. 开发混入基础属性

  混入基础属性由基础性的**计算属性**、**数据**组成。

  混入基础属性是父级块InputBlock和子级块ImageReadBlock都需要用到的属性，如isRunning属性表示当前块是否正在运行，父级块InputBlock需要此数据来控制界面的运行/暂停按钮。

```js
var InputPropertyMixin = {
  computed: {
    isRunning: { // 是否正在运行
      get() {
        return this.block.temp.isRunning
      }, 
      set(val) {
        this.block.temp.isRunning = val
      },
    }, 
    files() { // 当前文件列表
      return this.block.prop.input.value || []
    }
  },
}
```

2. 开发混入的功能

  混入的功能由功能性计算属性、数据及方法组成。

  混入的功能是父级块InputBlock不需要的，而子级块ImageReadBlock需要的，如readFileAsync同步读取文件方法，父级块InputBlock并不需要调用，父级块的本质是可复用的控件，所有的功能都有子级块完成。

```js
var InputFunctionMixin = {
  methods: {
    readFileAsync(file) {
      return new Promise((resolve, reject) => {
        let reader = new FileReader();
        reader.onload = () => {
          resolve(reader.result);
        };
        reader.onerror = reject;
        reader.readAsArrayBuffer(file);
      })
    },
  },
  created() {
    if (this.block.temp.isRunning === undefined) {
      this.$set(this.block.temp, 'isRunning', false)
    } 
  },
}

```

2. 导出

```js
export { BasePropertyMixin, BaseFunctionMixin } // 分别导出
export default [BasePropertyMixin, BaseFunctionMixin] // 整体导出
```

引入方式
```js
// 单独引入
import {BasePropertyMixin} from "@/components/blocks/BaseMixin"
// 整体引入
import InputMixin from "@/components/blocks/InputMixin.js";
```

## 减少冗余

采用基础属性与功能分离的开发模式，能够较少父级块的功能冗余，避免父级块注册不必要的方法，从而提高程序整体效率。