### Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式

[Vuex官方文档](https://vuex.vuejs.org/zh/)

>  我的目录结构
```
store 文件夹
  modules 模块文件夹 
    settings.js
  getter.js 计算文件
  index.js  入口文件
```

index.js
```Javascript
import Vue from 'vue'
import Vuex from 'vuex'
import getters from './getters'
import settings from './modules/settings'
Vue.use(Vuex)

export default new Vuex.Store({
  getters,
  modules: {
    settings
  }
})
```
settings.js
```Javascript
import { getItem, setItem } from '@/utils/storage'
const state = {
  dark: getItem('dark') || false
}

const mutations = {
  SET_DARK(state, bool) {
    state.dark = bool
    setItem('dark', bool)
  }
}

const actions = {

}

export default {
  namespaced: true,
  state,
  mutations,
  actions
}

```