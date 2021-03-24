[Vue官方文档](https://cn.vuejs.org/)

1. PC端 UI库

  [ElementUi库](https://element.eleme.cn/#/zh-CN/component/popover#events) 高效快速上手的ui库

  [Vuetify库](https://vuetifyjs.com/zh-Hans/components/lists/) 组件非常零碎 上手稍微会有些困难

  [AntDesignVue库](https://www.antdv.com/components/layout-cn/) 和Element有很多类似的地方，但又觉得比element用着好一些

2. Mobile端 UI库

  [Vant库](https://youzan.github.io/vant/#/zh-CN/)

### 组件之间参数传递

> #### 兄弟组件之间传参
1. 新建 <font style="color: red">eventBus.js</font> 事件中转站 引入Vue 抛出一个vue实例 这个实例身上有 $emit 和 $on 事件发射和事件监听

``` Javascript
import Vue from 'vue'

const vim = new Vue()

export default vim
```

2. 兄弟组件 <font style="color: #42b983">brother1.vue</font>

``` Vue
<template>
  <button @click="handleEvent">点击我触发兄弟组件2</button>
</template>
<script>
import eventBus from './eventBus.js'
export default {
  methods: {
    handleEvent() {
      eventBus.$emit('handleBrother', { data: '我是要传递数据' })
    }
  }
}
</script>
```
3. 兄弟组件 <font style="color: #42b983">brother2.vue</font>

``` Vue
<template>
  <div class="brother2">{{ brother1 }}</div>
</template>
<script>
import eventBus from './eventBus.js'
export default {
  data() {
    return {
      brother1: ''
    }
  },
  methods: {
    handleEvent() {
      eventBus.$on('handleBrother', e => {
        this.brother1 = e
        console.log(e)
      })
    }
  }
}
</script>
```

