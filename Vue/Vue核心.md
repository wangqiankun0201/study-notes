# Vue核心



## 初始Vue

想让Vue工作，就必须创建一个Vue实例，且要传入一个配置对象；

```vue
new Vue({
	el:'#root',//el用于指定当前Vue实例为哪个容器服务，值通常为css选择器字符串。
	data:{//data中用于存储数据，数据供el所指定的容器去使用
	name:'小猪佩奇'
}
})
```

root容器里的代码被称为【Vue模板】；



Vue实例和容器是一一对应的；



一旦data中的数据发生改变，那么页面中用到该数据的地方也会自动更新；



## 模板语法

### 插值语法

功能：用于解析标签体内容。

写法：`{{xxx}}`中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性；



### 指令语法

功能：用于解析标签。

写法：`v-bind:href="xxx" `



## 数据绑定

### 单向数据绑定

`v-bind:`:数据只能从data流向页面，简写`:`



### 双向数据绑定

`v-model:`数据不仅能从data流向页面，还能从页面流向data。



备注：

​	1、双向数据绑定一般应用在表单元素上。

​	2、`v-model:value`可以简写为`v-model`,因为v-model默认收集的就是value值



## el和data的两种写法

### el的两种写法

1.new Vue时配置el属性。

```vue
new Vue({
	el:"#root",
	data:{
	name:'小猪佩奇'
}
})
```



2.先创建Vue实例，随后通过`vm.$mount('#root')`指定el的值。

```vue
const vm = new Vue({
	data:{
	name:'小猪佩奇'
}
})

vm.$mount('#root');
```



### data的两种写法

1.对象式

```vue
new Vue({
	el:'#root',
	data:{
	name:'小猪佩奇	'
}
})
```

2.函数式

```vue
new Vue({
	el:'#root',
	data(){
	return {
	name:'小猪佩奇'
}
}
})
```



由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this就不是Vue实例了。



## MVVM模型

M：模型（Model）：data中的数据

V：视图（View）：模板代码

VM：视图模型（ViewModel）：Vue实例



1.data中的所有属性，最后都出现在了vm身上。

2.vm身上的所有属性及Vue原型上的所有属性，在Vue模板中都可以直接使用。





## 数据代理

### 回顾Object.defineProperty方法

```js
Object.defineProperty(person,'age',{
    value:18,
    enumerable:true,//控制属性是否可以枚举，默认值是false
    writabel:true,//控制属性是否可以被修改，默认值是false
    configurable:true//控制属性是否可以被删除，默认值是false
    
    
    //控制属性是否可以被删除，默认值是false
    get(){
    return numver
}


	//当有人修改person的age属性时，set函数(setter)就会被调用，且会收到修改的具体值
	set(value){
        number = value;
    }
})
```






### Vue中的数据代理

数据代理：通过一个对象，代理对另一个对象属性的操作。



Vue中通过vm对象代理data对象中属性的操作



基本原理：

​	通过`Object.defineProperty`方法把data对象中所有属性添加到vm上。

​	为每一个添加到vm上的属性都指定一个getter/setter。

​	在getter/setter内部去操作data中国对应的属性。





## 事件处理

### 事件的基本使用

1.使用`v-on:xxx`或者`@xxx`绑定事件，其中xxx为事件名。

2.事件的回调函数需要配置在methods对象中，最终会在vm上。

3.methods配置的函数，不要用箭头函数！否则this就不是vm了。

4.methods配置的函数，都是Vue管理的函数，this指向vm或组件实例对象。

5.`@click=demo`和`@click = demo($event)`效果一致，但后者可以传参。



### 事件修饰符

`prevent`阻止默认事件。

`stop`阻止事件冒泡。

`once`事件只触发一次。

`capture`使用事件的捕获模式。

`self`只有event.target是当前操作的元素时才触发事件。

`passive`事件的默认行为立即执行，无须等待事件回调执行完毕。



### 键盘事件

​				回车 => enter

​              删除 => delete (捕获“删除”和“退格”键)

​              退出 => esc

​              空格 => space

​              换行 => tab (特殊，必须配合keydown去使用)

​              上 => up

​              下 => down

​              左 => left

​              右 => right



## 计算属性

完整形式

```vue
computed:{
	fullname:{
	//get有什么作用？当有人读取fullName时，get就会被调用，且返回值就作为fullName的值
	//get什么时候调用？1.初次读取fullName时。2.所依赖的数据发生变化时。
	get(){
	return this.firstName + '-' + this.lastName;
}
//set什么时候调用? 当fullName被修改时。
	set(value){
	const arr = value.split('-');
	this.firstName = arr[0];
	this.lastName = arr[1];
}
}
}
```

简写形式

```vue
computed:{
	fullName(){
	return this.firstName + '-' + this.lastName;
}
}
```

## 监视属性

监视属性watch：

1.当被监视的属性变化时，回调函数自动调用，进行相关操作。

### 监视的两种写法

1、new Vue时穿入watch配置

```vue
watch:{
	isHot:{
	immediate:true, //初始化时让handler调用一下
	//handler什么时候调用？当isHot发生改变时。
	handler(newVal,oldVal){
		console.log('isHot被修改了',newVal,oldVal);
}
}
}
```

2、通过vm.$watch监视

```vue
vm.$watch('isHot',{
	immediate:true,
	handler(newVal,oldVal){
	console.log('isHot被修改了',newVal,oldVal);
}
})
```



### 深度监视



(1).Vue中的watch默认不监测对象内部值的改变（一层）。 (2).配置deep:true可以监测对象内部值改变（多层）。

```vue
watch:{
	number:{
	deep:true,
	handler(newVal,oldVal){
	console.log('number被修改了',newVal,oldVal);
}
}
}
```

```vue
watch:{
	isHot(newVal,oldVal){
	console.log('isHot被修改了',newVal,oldVal);
}
}
```





### computed和watch之间的区别：

1.computed能完成的功能，watch都可以完成。

 2.watch能完成的功能，computed不一定能完成，例如：watch可以进行异步操作。

两个重要的小原则：

1.所被Vue管理的函数，最好写成普通函数，这样this的指向才是vm 或 组件实例对象。

2.所有不被Vue所管理的函数（定时器的回调函数、ajax的回调函数等、Promise的回调函数），最好写成箭头函数， 这样this的指向才是vm 或 组件实例对象。





## 绑定样式

### class样式

`:class="xxx"`,xxx可以是字符串、对象、数组。



字符串写法适用于：类名不确定，要动态获取。

 对象写法适用于：要绑定多个样式，个数不确定，名字也不确定。

 数组写法适用于：要绑定多个样式，个数确定，名字也确定，但不确定用不用。

## 条件渲染

### v-if

(1).v-if="表达式" 

(2).v-else-if="表达式"

(3).v-else

适用于：切换频率较低的场景。

特点：不展示的DOM元素直接被移除。

注意：v-if可以和:v-else-if、v-else一起使用，但要求结构不能被“打断”。



### v-show

v-show="表达式"

适用于：切换频率较高的场景。

特点：不展示的DOM元素未被移除，仅仅是使用样式隐藏掉



## 列表渲染

### v-for

v-for="(item, index) in xxx" :key="yyy"

可遍历：数组、对象、字符串（用的很少）、指定次数（用的很少）

### key的原理

1.虚拟DOM中key的作用：

key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】, 随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下：

​                    

2.对比规则：

 (1).旧虚拟DOM中找到了与新虚拟DOM相同的key：

①.若虚拟DOM中内容没变, 直接使用之前的真实DOM！

②.若虚拟DOM中内容变了, 则生成新的真实DOM，随后替换掉页面中之前的真实DOM。



(2).旧虚拟DOM中未找到与新虚拟DOM相同的key

创建新的真实DOM，随后渲染到到页面。

​                        

3.用index作为key可能会引发的问题：

（1）若对数据进行：逆序添加、逆序删除等破坏顺序操作:

 会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。



（2）如果结构中还包含输入类的DOM：会产生错误DOM更新 ==> 界面有问题。



### 列表过滤

1.监视属性实现

```vue
watch:{
	keyWord:{
		immediate:true,
		handler(val){
		this.filPerons = this.persons.filter((p)=>{
				return p.name.indexOf(val) !== -1
	     })
	}
			}
		}
```

2.计算属性实现

```vue
computed:{
	filPerons(){
		return this.persons.filter((p)=>{
		      return p.name.indexOf(this.keyWord) !== -1
		})
	}
}
```

### 列表排序

```
computed:{
	filPerons(){
	const arr = this.persons.filter((p)=>{
		return p.name.indexOf(this.keyWord) !== -1
		})
	//判断一下是否需要排序
	if(this.sortType){
		arr.sort((p1,p2)=>{
			return this.sortType === 1 ? p2.age-p1.age : p1.age-p2.age
		})
	}
		return arr
   }
}
```

## 数据监测

Vue监视数据的原理：

1.vue会监视data中所有层次的数据。



2.如何监测对象中的数据？

 通过setter实现监视，且要在new Vue时就传入要监测的数据。

​              (1).对象中后追加的属性，Vue默认不做响应式处理

​              (2).如需给后添加的属性做响应式，请使用如下API：

​                          Vue.set(target，propertyName/index，value) 或 

​                          vm.$set(target，propertyName/index，value)



3.如何监测数组中的数据？

通过包裹数组更新元素的方法实现，本质就是做了两件事：

​                (1).调用原生对应的方法对数组进行更新。

​                (2).重新解析模板，进而更新页面。



4.在Vue修改数组中的某个元素一定要用如下方法：

​              1.使用这些API:push()、pop()、shift()、unshift()、splice()、sort()、reverse()

​              2.Vue.set() 或 vm.$set()

​        

特别注意：Vue.set() 和 vm.$set() 不能给vm 或 vm的根数据对象 添加属性！！！


## 收集表单数据

​          若：<input type="text"/>，则v-model收集的是value值，用户输入的就是value值。

​          若：<input type="radio"/>，则v-model收集的是value值，且要给标签配置value值。

​          若：<input type="checkbox"/>

​              1.没有配置input的value属性，那么收集的就是checked（勾选 or 未勾选，是布尔值）

​              2.配置input的value属性:

​                  (1)v-model的初始值是非数组，那么收集的就是checked（勾选 or 未勾选，是布尔值）

​                  (2)v-model的初始值是数组，那么收集的的就是value组成的数组

​          备注：v-model的三个修饰符：

​                  lazy：失去焦点再收集数据

​                  number：输入字符串转为有效的数字

​                  trim：输入首尾空格过滤

## 过滤器

​        定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。

​        语法：

​            1.注册过滤器：Vue.filter(name,callback) 或 new Vue{filters:{}}

​            2.使用过滤器：{{ xxx | 过滤器名}}  或  v-bind:属性 = "xxx | 过滤器名"

​        备注：

​            1.过滤器也可以接收额外参数、多个过滤器也可以串联

​            2.并没有改变原本的数据, 是产生新的对应的数据





## 内置指令

我们学过的指令：

​            v-bind  : 单向绑定解析表达式, 可简写为 :xxx

​            v-model : 双向数据绑定

​            v-for  : 遍历数组/对象/字符串

​            v-on   : 绑定事件监听, 可简写为@

​            v-if   : 条件渲染（动态控制节点是否存存在）

​            v-else  : 条件渲染（动态控制节点是否存存在）

​            v-show  : 条件渲染 (动态控制节点是否展示)

### v-text

​            1.作用：向其所在的节点中渲染文本内容。

​            2.与插值语法的区别：v-text会替换掉节点中的内容，{{xx}}则不会。

### v-html

​            1.作用：向指定节点中渲染包含html结构的内容。

​            2.与插值语法的区别：

​                  (1).v-html会替换掉节点中所有的内容，{{xx}}则不会。

​                  (2).v-html可以识别html结构。

### v-cloak

v-cloak指令（没有值）：

​            1.本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性。

​            2.使用css配合v-cloak可以解决网速慢时页面展示出{{xxx}}的问题。

### v-once

​            1.v-once所在节点在初次动态渲染后，就视为静态内容了。

​            2.以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能。



### v-pre

​          1.跳过其所在节点的编译过程。

​          2.可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译。



## 自定义指令

一、定义语法

（1）局部指令

```vue
directives:{
				//big函数何时会被调用？1.指令与元素成功绑定时（一上来）。2.指令所在的模板被重新解析时。
				/* 'big-number'(element,binding){
					// console.log('big')
					element.innerText = binding.value * 10
				}, */
				big(element,binding){
					console.log('big',this) //注意此处的this是window
					// console.log('big')
					element.innerText = binding.value * 10
				},
				fbind:{
					//指令与元素成功绑定时（一上来）
					bind(element,binding){
						element.value = binding.value
					},
					//指令所在元素被插入页面时
					inserted(element,binding){
						element.focus()
					},
					//指令所在的模板被重新解析时
					update(element,binding){
						element.value = binding.value
					}
				}
			}
```

(2)全局指令

```vue
Vue.directive('fbind',{
			//指令与元素成功绑定时（一上来）
			bind(element,binding){
				element.value = binding.value
			},
			//指令所在元素被插入页面时
			inserted(element,binding){
				element.focus()
			},
			//指令所在的模板被重新解析时
			update(element,binding){
				element.value = binding.value
			}
		}) 
```

二、配置对象中常用的3个回调：

​                  (1).bind：指令与元素成功绑定时调用。

​                  (2).inserted：指令所在元素被插入页面时调用。

​                  (3).update：指令所在模板结构被重新解析时调用。



三、备注：

​                  1.指令定义时不加v-，但使用时要加v-；

​                  2.指令名如果是多个单词，要使用kebab-case命名方式，不要用camelCase命名

## 生命周期

生命周期：

​            1.又名：生命周期回调函数、生命周期函数、生命周期钩子。

​            2.是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数。

​            3.生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的。

​            4.生命周期函数中的this指向是vm 或 组件实例对象。![生命周期](../尚硅谷Vue技术全家桶（天禹老师主讲）/资料（含课件）/资料（含课件）/02_原理图/生命周期.png)

常用的生命周期钩子：

​            1.mounted: 发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】。

​            2.beforeDestroy: 清除定时器、解绑自定义事件、取消订阅消息等【收尾工作】。



 关于销毁Vue实例

​            1.销毁后借助Vue开发者工具看不到任何信息。

​            2.销毁后自定义事件会失效，但原生DOM事件依然有效。

​            3.一般不会在beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了。
