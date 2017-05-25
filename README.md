前端知识学习回顾
------------------------
* 用js获取和设置cookie
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
>
>
>
