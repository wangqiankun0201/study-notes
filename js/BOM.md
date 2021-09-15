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

### clearTimeout() 清除定时器



```js
clearTimeout(timer)
```



### setInterval()定时器

```js
setInterval(回调函数,[间隔的毫秒数]);
```



### clearInterval() 清除定时器

`var timer = null;`

## this指向问题

==一般情况下this的最终指向的是那个调用它的对象==

1. 在全局作用域或者普通函数中，this指向全局对象``window`，定时器中的this指向`window`

2. 在方法中谁调用指向谁

3. 构造函数中this指向构造函数的实例


## js执行机制
由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，所以这种机制称为==事件循环==
![js执行机制](../../../Typora图片/js执行机制.PNG)





## location 对象

URL：统一资源定位符

### location 对象的属性

|       属性        |               返回值               |
| :---------------: | :--------------------------------: |
|   location.href   |         返回或设置整个URL          |
|   location.host   |            返回主机域名            |
|   location.port   |    返回端口号，未写返回空字符串    |
| location.pathname |              返回路径              |
|  location.search  |              返回参数              |
|   location.hash   | 返回片段 #后面内容 常见于链接 锚点 |

### location 对象的方法

| 方法               | 返回值                                                       |
| ------------------ | ------------------------------------------------------------ |
| location.assign()  | 同href，称为重定向页面，记录历史，可以后退                   |
| location.replace() | 替换当前页面，因为不记录历史，所以不能后退页面               |
| location.reload()  | 重新加载页面，相当于刷新按钮或者f5 如果参数为true强制刷新ctrl+f5 |

## navigator对象

userAgent

## history对象

|   方法    |              作用               |
| :-------: | :-----------------------------: |
|  back()   |              后退               |
| forward() |              前进               |
| go(参数)  | 1:前进一个页面  -1:后退一个页面 |

