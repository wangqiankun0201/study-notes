# ECMAScript

## 数据类型

js的变量数据类型只有在运行程序过程中，根据等号右边的值来确定

js是动态语言，变量的数据类型是可以变化的

### 简单数据类型

#### 1.Number

1.八进制：我们在程序前面加0，表示八进制

2.十六进制：数字前面加0x，表示十六进制

infinity：无穷大

-infinity：无穷小

NaN：非数值

==isNaN()==:这个方法·用来判断非数字，并且返回一个值，如果是数字返回false，如果不是数字返回true

#### 2.Boolean

true当1看

false当0看

#### 3.String



#### 4.Undefined

和字符串想见最后是undefinedString

和数字相加是NaN

#### 5.Null

和数字相加就是原先的数字



==(typeof num)== 检测数据类型

#### 6.数据类型转换

##### 1.转换为字符串

|        方式        |      案例      |
| :----------------: | :------------: |
|     toString()     | num.toString() |
|  String()强制转换  |  String(num)   |
| 加号拼接(隐式转换) |     num+""     |

##### 2.转换为数字型

|        方式        |       案例       |
| :----------------: | :--------------: |
|  parseInt(string)  |  parseInt('78')  |
| parseFloat(string) | parseFloat('78') |
|  Number()强制转换  |   Number('78')   |
| js隐式转换(- * /)  |      '12'-0      |

##### 3.转换为Boolen型

Boolen("")

代表空，否定的值都会被转换为false，其余都会转换为true

“”，0，NaN，null，undefined





## arguments

存储所有传递过来的实参

==只有函数才有arguments==

伪数组：

1.具有数组的length属性

2.按照索引的方式进行存储

3.他没有真正数组的一些方法
