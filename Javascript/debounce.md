### 函数防抖
> 函数防抖的概念：其实就是延时执行，当你在N秒内触发该事件 就会重新开始延时 直到你触发的频率时长大于延时时长 事件才会被触发
* 第一步：首次滑入 t是undefined 所以也不会执行clearTimeout() 方法
* 第二步：会判断triggle参数 为true 表明滑入后要立即执行(这种场景也适用于搜索) 
* 第三步：定义变量 let new = !t !t就是true 由于setTimerout是异步执行 那么就会来到调用函数这一步 到这里首次触发成功！
* 场景1：假设你在这一秒内滑出又滑入 那么此时延时器必然也没有走完 所以t为真 会执行clearTimeout()这个方法，再往下!t也就是false了。所以也不会再次调用函数。
* 场景2：假设你超出一秒后再次滑入 那么此时延时器也就走完了 并且让t = null 此时的动作就会和第三步是一样的了
```
  function debounce(fun, delay, triggle) {
    let t;
    return (...args) => {
      t && clearTimeout(t);
      if (triggle) {
        let now = !t;
        t = setTimeout(() => {
          t = null;
        }, delay);
        now && fun.apply(this, args);
      } else {
        t = setTimeout(() => {
          fun.apply(this, args);
          t = null;
        }, delay);
      }
    }
  }
const oBox = document.querySelector('#box');
oBox.addEventListener('mouseover', debounce(handleMouseover, 1000, true))
function handleMouseover() {
  console.log('我进来了')
}
```
### 函数节流
> 函数节流的概念：无论事件触发的有多么的频繁 它总会在一个规定的时间里 执行一次
```
  function throttle(fun, wait) {
    let t = null;
    return (...args) => {
      if (!t) {
        t = setTimeout(() => {
          fun.apply(this, args)
          t = null
        }, wait)
      }
    }
  }
```
