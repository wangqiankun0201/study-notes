# DOM

## DOM 树

文档：一个页面就是一个文档，DOM中使用document表示

元素：页面中的所有标签都是元素，DOM中使用element表示

节点：网页中的所有内容都是节点（标签、属性、文本、注释），DOM中使用node表示



==DOM把以上内容都看做是对象==



## 获取元素

### 根据ID获取

`document.getElementById()`



`console.dir() ` 打印我们返回的元素对象，更好地查看属性和方法



### 根据标签名获取

`document.getElementsByTagName()` 以伪数组的形式存储

`element.getElementByTagName()`指定一个父元素，获取父元素内部的子元素

==父元素必须是单个对象==

```js
var ol = document.getElementByTagName('ol');
var lis = ol[0].getElementByTagName('li');
```



### 根据类名获取

`document.getElementByClassName()`   伪数组

### 厉害的选择器

`document.querySelector()`  返回指定选择器的第一个元素对象



`document.querySelectorAll()`  返回指定选择器的所有元素对象



### 获取body和html

`document.body`

`document.documentElement`

## 事件

事件三要素：==事件源==，==事件类型==，==事件处理程序==

`this`指向当前事件的调用者

一个按钮两种效果，可以利用`flag`

`onfocus`   获得焦点

`onblur`  失去焦点

### 排他思想

[干掉所有人，留下我自己][干掉所有人，留下我自己]

## 操作元素

### 改变元素内容

`element.innerText`  去除空格和换行

`element.innerHTML`  保留空格和换行

### 改变元素属性

`element.属性`

==表单元素属性：==

表单里面的值是通过`value`修改的      `element.value`

表单被禁用：`element.disabled = true `

切换表单类型：`element.type`



###  样式属性操作

`element.style.属性=""`      ==属性采取驼峰命名法==

产生的是行内样式



`element.className`  会直接更改类名，会覆盖之前的，如果想保留之前的类名，可以采用多类名选择器

#### 获取属性值

`element.getAttribute('属性')`    获取元素属性    可以获取自定义属性

`element.属性`     只可以获取内置属性

#### 设置属性值

`element.属性 = '值'`    设置内置属性

`element.setAttribute('属性','值')`      针对自定义属性

#### 移出属性

`element.removeAttribute('属性')`



==自定义属性解决tab选项卡==   



#### H5新增的获取自定义属性的方法

`data-属性`    标准

`element.dataset.属性`  ==  `element.dataset['属性'] `     只能获取`data-`开头的

==例外：==

data-list-name    ->   `element.dataset.listName`   驼峰   ==   `element.dataset['listName']`

## 节点操作

`nodeType`  节点类型

|   节点   | nodeType |
| :------: | :------: |
| 元素节点 |    1     |
| 属性节点 |    2     |
| 文本节点 |    3     |

`nodeName`  节点名称

`nodeValue`   节点值

### 节点层级

#### 1.父级节点

`node.parentNode`

#### 2.子节点

`parentNode.childNodes`       包含元素节点和文本节点

==如果只想获得元素节点，需要专门处理==

`parentNode.childNodes[i].nodeType == 1`     获取元素节点



`parentNode.children`    获取所有子元素节点



`parentNode.firstChild`   获取第一个子节点，不管是文本节点还是元素节点

`parentNode.lastChild`  获取最后一个子节点，不管是文本节点还是元素节点





`parentNode.firstElementChild`    返回第一个子元素节点

`parentNode.lastElementChild`   返回最后一个子元素节点

#### 3.兄弟节点

`node.nextSibling`     返回当前元素的下一个兄弟节点，包括文本节点和元素节点

`node.previousSibling`  返回当前元素的上一个兄弟节点，包括文本节点和元素节点



`node.nextElementSibling`   返回当前元素下一个兄弟元素节点

`node.previoudElementSibling`   返回当前元素上一个兄弟元素节点



### 创建节点

`document.createElement('tagName')`     动态创建元素节点



### 添加节点

`node.appendChild(child)`       后面追加元素



`node.insertBefore(child,指定元素)`    在指定节点前面添加节点

### 删除节点

`node.removeChild(child)`



`<a href = 'javascript:;'></a>`      ==阻止链接跳转==



### 复制节点

`node.cloneNode()`    返回该方法节点的一个副本

[如果括号为空或者false，则是浅拷贝，只克隆节点本身，不克隆里面的子节点][如果括号为空，则是浅拷贝，只克隆节点本身，不克隆里面的节点]



[加上true可以为深拷贝][]

### 三种动态创建元素的区别

`document.write()` 是直接将内容写入页面的内容流，==但是文档流执行完毕，则它会导致页面全部重绘==

`innerHTMl`  是将内容写入某个DOM节点，不会导致页面全部重绘，创建多个元素效率更高(不要拼接字符串,采取数组拼接),结构稍微复杂



`createElement()`  创建多个元素效率稍微低一点点，但是结构更清晰

 









 



​     
