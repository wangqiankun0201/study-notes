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

