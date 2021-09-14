# BOM

window对象是浏览器的顶级对象，它具有双重角色：

1.它是js访问浏览器窗口的一个接口

2.他是一个全局对象，定义在全局作用域夏的变量、函数都会变成window对象的属性和方法



window下的一个特殊属性`window.name`

## window对象的常见事件

### 窗口加载事件

```javascript
window.onload = function() {}     //只能写一次

window.addEventListener('load', function() {});
```





```javascript
document.addEventListener('DOMContentLoaded', function() {})
```

当DOM加载完成后就触发，不包括样式表，图片等。



### 窗口大小事件

```javascript
window.onresize = function() {}

window.addEventListener('resize', function(){});
```





`window.innerWidth`   获得当前屏幕的宽度

## 定时器

### setTimeout() 定时器

```javascript
window.setTimeout(调用函数, [延迟的毫秒数]);
```



window 可以省略

给不同的定时器起不同的名字，用以区别

