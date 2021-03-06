> #### 输入一个值，返回其数据类型
```javascript
function type(para) {
    return Object.prototype.toString.call(para)
}
```
> #### 输入一个值，返回其数据类型
```javascript
function isIn(data, prot) {
    return Object.prototype.hasOwnProperty.call(data, prot)
}
```
> #### 数组去重
```javascript
function unique1(arr) {
    return [...new Set(arr)]
}

function unique2(arr) {
    var obj = {};
    return arr.filter(ele => {
        if (!obj[ele]) {
            obj[ele] = true;
            return true;
        }
    })
}
```
> #### 字符串去重
```javascript
String.prototype.unique = function () {
    var obj = {},
        str = '',
        len = this.length;
    for (var i = 0; i < len; i++) {
        if (!obj[this[i]]) {
            str += this[i];
            obj[this[i]] = true;
        }
    }
    return str;
}

###### //去除连续的字符串 
function uniq(str) {
    return str.replace(/(\w)\1+/g, '$1')
}
```
> #### 找出字符串中第一次只出现一次的字母
```javascript
String.prototype.firstAppear = function () {
    var obj = {},
        len = this.length;
    for (var i = 0; i < len; i++) {
        if (obj[this[i]]) {
            obj[this[i]]++;
        } else {
            obj[this[i]] = 1;
        }
    }
    for (var prop in obj) {
       if (obj[prop] == 1) {
         return prop;
       }
    }
}
```
> #### 返回当前的时间（年月日时分秒）
```javascript
function getDateTime() {
    var date = new Date(),
        year = date.getFullYear(),
        month = date.getMonth() + 1,
        day = date.getDate(),
        hour = date.getHours() + 1,
        minute = date.getMinutes(),
        second = date.getSeconds();
        month = checkTime(month);
        day = checkTime(day);
        hour = checkTime(hour);
        minute = checkTime(minute);
        second = checkTime(second);
     function checkTime(i) {
        if (i < 10) {
                i = "0" + i;
       }
      return i;
    }
    return "" + year + "年" + month + "月" + day + "日" + hour + "时" + minute + "分" + second + "秒"
}
```
> #### 检验字符串是否是回文
```javascript
function isPalina(str) {
    if (Object.prototype.toString.call(str) !== '[object String]') {
        return false;
    }
    var len = str.length;
    for (var i = 0; i < len / 2; i++) {
        if (str[i] != str[len - 1 - i]) {
            return false;
        }
    }
    return true;
}
```
> #### 验证邮箱的正则表达式
```javascript
function isAvailableEmail(sEmail) {
    var reg = /^([\w+\.])+@\w+([.]\w+)+$/
    return reg.test(sEmail)
}
```

> #### 获取地址栏参数 并转换成对象（也可以传递url）
```javascript
function getUrlParams(url) {
  const _url = url || window.localtion.href
  const _urlParams = _url.match(/([?&])(.+?=[^&]+)/igm);
  const objParams = _urlParams ? _urlParams.reduce((a, b) => {
    const value = b.slice(1).split('=');
    a[value[0]] = value[1]
    return a
  }, {}) : {}
  return objParams
}
```
