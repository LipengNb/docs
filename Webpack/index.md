### 1. 模块化相关规范
> node.js中通过babel体验ES6模块化
1. npm install -D @babel/core @babel/cli @babel/preset-env @babel/node
2. npm install -S @babel/polyfill
3. 项目根目录创建文件 babel.config.js
4. babel.config.js 文件内容如下代码

``` javascript
  const presets = [
    ["@babel/env", {
      targets: {
        edge: "17",
        firefox: "60",
        chrome: "67",
        safari: "11.1"
      }
    }]
  ]

  module.exports = { presets }
``` 
5. 通过 npx babel-node index.js 执行代码

> ES6模块化的基本语法
1. 默认导出 与 默认导入
* 默认导出的语法 export default 默认导出的成员

``` javascript

let a = 10
let c = 20
function show () {}

// 外界访问不到变量 因为没有被暴露出去
let d = 30

// 将本模块中的私有成员暴露出去，供其他模块使用
export default {
  a,
  c,
  show
}
```
* 默认导入语法 import 接收名称 from '模块标识符'

``` javascript
// 导入模块成员
import m1 from './m1.js'

console.log(m1)
// 打印输出的结果为
{ a: 10, c: 20, show: [Function: show] }
```