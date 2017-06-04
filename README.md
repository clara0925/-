前端知识学习回顾
------------------------
* 简单的js运动
```javascript
function objmove(obj, json, fn) {
   clearInterval(obj.timer);

   obj.timer = setInterval(function() {
      var flag = true;
      for (var attr in json) {
         var oattr = 0;
         if (attr == "opacity") {
            oattr = Math.round(parseFloat(getStyle(obj, attr)) * 100);
         } else {
            oattr = parseInt(getStyle(obj, attr));
         }

         var speed = (json[attr] - oattr) / 10;

         speed = speed > 0 ? Math.ceil(speed) : Math.floor(speed);
         if (oattr != json[attr]) {
            flag = false;
         }

         if (attr == "opacity") {
            obj.style.filter = "alpha(" + attr + ":" + (oattr + speed) + ")";
            obj.style[attr] = (oattr + speed) / 100;
         } else {
            obj.style[attr] = oattr + speed + "px";
         }
      }
      if (flag) {
         clearInterval(obj.timer);
         if (fn) {
            fn(obj);
         }
      }
   }, 30);
}

function getStyle(obj, attr) {
   if (obj.currentStyle) {
      return obj.currentStyle[attr];
   } else {
      return getComputedStyle(obj, false)[attr];
   }
}
```

* 用js获取和设置cookie
```javascript
function setCookie(name, value, expires, path, domain, secure) {
    var cookieText = encodeURIComponent(name) + '=' + encodeURIComponent(value);
    if (expires instanceof Date) {
        cookieText += '; expires=' + expires;
    }
    if (path) {
        cookieText += '; expires=' + expires;
    }
    if (domain) {
        cookieText += '; domain=' + domain;
    }
    if (secure) {
        cookieText += '; secure';
    }
    document.cookie = cookieText;
}

//获取cookie
function getCookie(name) {
    var cookieName = encodeURIComponent(name) + '=';
    var cookieStart = document.cookie.indexOf(cookieName);
    var cookieValue = null;
    if (cookieStart > -1) {
        var cookieEnd = document.cookie.indexOf(';', cookieStart);
        if (cookieEnd == -1) {
            cookieEnd = document.cookie.length;
        }
      cookieValue = decodeURIComponent(document.cookie.substring(cookieStart + cookieName.length, cookieEnd));
    }
    return cookieValue;
}

//删除cookie
function unsetCookie(name) {
    document.cookie = name + "= ; expires=" + new Date(0);
}
```
 
* 三种定义变量的方式：var/const/let
 
>其中`const`用来定义一个常量，常量可以看作是不能重复赋值的变量。
>`let`可以像var一样作为变量声明，用在for或者for/in的循环当中，作为var的替代方案，作用域限定在块级；用let定义一个在表达式内部作用域中的变量，这个变量仅在表达式内有效。
>


* 真的很无聊到把console.log变模糊。。。
```javascript
var blurLog = console.log;
console.log = function() {
    blurLog.call(console, '%c' + [].slice.call(arguments).join(' '),
        'color:transparent;text-shadow:0 0 2px rgba(0,0,0,.5);');
};
```
