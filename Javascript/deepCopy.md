### 深拷贝
> 递归深拷贝
```javascript
function deepCopy(target) {
  let result;
  if (typeof target === 'object') {
    if (Array.isArray(target)) {
      result = []
      for (const i in target) {
        result.push(deepCopy(target[i]))
      }
    } else if (target === null) {
      result = null
    } else if (target.constructor === RegExp) {
      result = target
    } else {
      result = {}
      for (const i in target) {
        result[i] = deepCopy(target[i])
      }
    }
  } else {
    result = target
  }
  return result
}

const copyObj = deepCopy(target)


```
> 简单粗暴深拷贝（适合纯JSON数据的拷贝）
```javascript
const copyObj = JSON.parse(JSON.stringify(target))

```

### 浅拷贝
> 通过Object.assign()（只能拷贝一层对象 如果对象内属性还有嵌套对象 修改一个会影响到被拷贝的对象哦~）
```javascript
const copyObj = Object.assign({}, target)

```
> 通过遍历进行拷贝
```javascript
function shallowCopy(obj) {
  let result = {}
  if (typeof obj === 'object') {
    for (const i in obj) {
      result[i] = obj[i]
    }
  }
  return result
}

```