> #### 1. 输入一个值，返回其数据类型
```Javascript
function type(para) {
    return Object.prototype.toString.call(para)
}
```
> #### 2. 数组去重
```Javascript
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
> #### 3. 字符串去重
```Javascript
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
> #### 4. 找出字符串中第一次只出现一次的字母
```Javascript
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
> #### 5. 返回当前的时间（年月日时分秒）
```Javascript
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
> #### 6. 检验字符串是否是回文
```Javascript
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
> #### 7. 验证邮箱的正则表达式
```Javascript
function isAvailableEmail(sEmail) {
    var reg = /^([\w+\.])+@\w+([.]\w+)+$/
    return reg.test(sEmail)
}
```
