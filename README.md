### 准备工作
全局安装 [docsify-cli](https://www.npmjs.com/package/docsify-cli) 工具，并创建文档项目目录
```
npm i docsify-cli -g
mkdir my-docs
cd my-docs
```
### 初始化项目
```
docsify init ./docs
```
成功后会生成一个 docs 的文件夹，并且里面有三个文件
* <font color=#ff502c>index.html</font> 入口文件。后面我们的配置很多都是在这里配置
* <font color=#ff502c>README.md</font> 会做为主页内容渲染
* <font color=#ff502c>.nojekyll</font> 用于阻止 <font color=#ff502c>GitHub Pages</font> 忽略掉下划线开头的文件

### 启动项目
```
docsify serve docs
```
通过运行 <font color=#ff502c>docsify serve</font> 启动一个本地服务器，可以方便地实时预览效果。默认访问地址 http://localhost:3000 。下面的内容时间上是 README.md 中的内容
