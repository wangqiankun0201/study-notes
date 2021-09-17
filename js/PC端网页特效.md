# PC端网页特效

## 元素偏移量offset系列

* 获得带有定位的父元素的位置
* 获得元素自身的大小
* 返回的数值不带单位

| offset系列属性       | 作用                                             |
| -------------------- | ------------------------------------------------ |
| element.offsetParent | 返回作为该元素带有定位的父级元素，没有则返回body |
| element.offsetTop    | 返回元素相对于带有定位的父元素的偏移             |
| element.offsetLeft   | 返回元素相对于带有定位的父元素的左边框的偏移     |
| element.offsetWidth  | 返回自身包括padding、边框、内容区的宽度          |
| element.offsetHeight | 返回自身包括padding、边框、内容区的宽度          |

### offset与style的区别

| offset                                        | style                                   |
| --------------------------------------------- | --------------------------------------- |
| offset可以得到任意样式表中的样式值            | style只能得到行内样式表的样式值         |
| offset获得的数值,没有单位                     | style.width获得的带有单位的字符串       |
| offsetWidth包含padding+border+width           | style.width不包含padding和border的值    |
| offsetWidth等属性是只读属性，只能获取不能赋值 | style.width是读写属性，可以获取可以赋值 |
| ==想要获取元素大小位置用offset==              | ==想要修改元素值，用style==             |



## 元素可视区client系列

获得该元素的边框大小，元素大小

| client系列属性       | 作用                                                        |
| -------------------- | ----------------------------------------------------------- |
| element.clientTop    | 返回元素上边框大小                                          |
| element.clientLeft   | 返回元素做边框的大小                                        |
| element.clientWidth  | 返回自身包括padding、内容区、不含边框，返回数值不带单位     |
| element.clientHeight | 返回自身包括padding、内容区宽度、不含边框，返回数值不带单位 |

 ## 立即执行函数

不需要调用，自己就能够执行的函数



### 写法

`(funtion() {})();`或者`(function() {}());`



立即执行函数最大的作用就是==独立创建了一个作用域==

## 元素滚动scroll系列

| scroll系列属性       | 作用                                         |
| -------------------- | -------------------------------------------- |
| element.scrollTop    | 返回被卷去的上侧距离，返回数值不带单位       |
| element.scrollLeft   | 返回被卷去的左侧距离，返回数值不带单位       |
| element.scrollWidth  | 返回自身实际宽度，不含边框，返回数值不带单位 |
| element.scrollHeight | 返回自身实际高度，不含边框，返回数值不带单位 |





`window.pageYOffset`=>  页面被卷去的头部

`window.pageXOffset`=> 页面被卷去的左侧

## 三大系列总结

1.`offset系列`经常用于获得元素位置，`offsetTop`,`offsetLeft`

2.`client系列`经常用于获取元素大小 `clientWidth`,`clientHeight`

3.`scroll系列`经常用于获取滚动距离 `scrollTop`,`scrollLeft`

4.==页面滚动距离通过`windwo.pageYoffset`获取==

## 动画

==核心原理==：通过定时器`setInterval()`不断移动盒子的位置

==动画里面必须加定位==

### 动画函数封装

注意函数需要传递2个参数，==动画对象==和==移动距离==



不同`var`声明，采用`obj.timer`对象的属性来定义



如果是按钮控制的定时器，多次点击可能会出现越来越快的bug，解决方法是`clearInterval()`清除之前的定时器，只保留一个定时器



### 缓动动画封装

缓动动画就是让元素运动速度有所变化

原理就是随着时间移动距离变化

==核心算法==：(目标值-现在的位置)/10 作为每次移动的距离步长



动画在多个目标中间移动

判断步长是正是负

1. 正的向上取`Math.ceil()`
2. 负的向下取`Math.floor()`

==三元表达式实现==







### 节流阀

利用回调函数改变当前事件的执行状态

flag=true,false



### 逻辑中断应用



```js
if(callback){
    callback()
}
==
callback && callback();
```



### 返回顶部

`window.scroll(x,y)`

