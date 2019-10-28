# JS对象基本用法
## 对象的两种语法
1. 定义：JS对象是无序的数据组合；是键值对的集合。

2. 写法：obj={'key1':'value1','key2':'value2',}

    key是对象的属性名，value是对象的属性值。

3. 语法：有两种方式来访问对象的属性，点操作符或者中括号操作符。
~~~JavaScript
let obj=new Object({'name':'zhang','18age'=18,'33':'haha'})
//等同于 let obj={name:'zhang','18age'=18,'33':'haha'}

obj.name
//"zhang";等同于下面
obj['name']
//"zhang";'name'的引号不能省略

obj['18age']
//"18";这种数字开头的只能用中括号操作符，不能写成 obj.18age

obj[33]
//"haha";这种纯数字的引号可以省略
~~~
* 一般情况下属性名加引号和不加引号是都可以的，效果是一样的，'name'去掉引号效果不变，但是以数字开头的属性名'18age'必须加引号。
* 所有的keys都是一个字符串，即使省略掉了引号也是一个字符串，数字开头的建议都加引号，避免出错。
* 使用中括号操作符时
~~~JavaScript
let a='xxx'
let obj={
    [a]:'byl'
}
console.log(obj)
//{xxx: "byl"}

let a='xxx'
let obj={
    a:'byl'
}
console.log(obj)
//{a: "byl"}
~~~
如果a不加[ ]，属性名会自动变成字符串；a加了[ ]，则会被当做变量求值，值如果不是字符串，就会尽量变成字符串。
* 除了字符串,symbol也能做属性名。
## 如何删除对象的属性
删除属性的唯一方法是使用 delete 操作符；设置属性为 undefined 或者 null 并不能真正的删除属性， 而仅仅是移除了属性和值的关联。
~~~JavaScript
let obj={
    name:'zhang',age:18,gender:'man'
}
~~~
操作如下：
~~~JavaScript
delete obj.name
//ture;成功删除了name的属性名和属性值

obj.age=undefined
//undefined;移除age的属性值

obj.gender=null
//null;让gender属性值成为空值
~~~
属性名引号不能省的要写成 obj[''] ,如下
~~~javascript
    delete obj['18age']
    obj['1e2']=null/undefined
~~~
## 如何查看对象的属性

~~~JavaScript
let obj={
    name:'zhang',age:18,gender:'man'
}
~~~
* 查属性名
~~~javascript
    Object.keys(obj)
~~~
* 查属性值
~~~javascript
    Object.value(obj)
~~~
* 查属性名和属性值
~~~javascript
    Object.entries(obj)
~~~
* 查隐藏属性
~~~javascript
    console.dir(obj)
~~~
## 如何修改或增加对象的属性
依然拿下面代码举例
~~~JavaScript
let obj={
    name:'zhang',age:18,gender:'man'
}
~~~
* 添加自身属性
~~~JavaScript
obj.interests='swimming'
//单个添加属性

Object.assign(obj,{weight:65,height:175,})
//多个添加属性
~~~
* 修改共有属性
~~~JavaScript
obj.toString='xxx'
//修改本对象的toString属性

Object.prototype.toString='yyy'
//修改所有对象的toString属性，也可以用Object.__proto__.toString，但不建议用
~~~
* 增添共有属性
~~~JavaScript
let common={
    name: 'zhang', age: 18, gender: 'man', interests: 'swimming', weight: 65
}
let obj=Object.create(common)
~~~
## 'name' in obj和obj.hasOwnProperty('name') 的区别
运行下面代码
~~~JavaScript
let obj={
    name: 'zhang', age: 18, gender: 'man'
}
~~~
'key' in obj 是判断对象 obj 是否有该属性 'key' ，无论自身属性还是隐藏属性。
~~~JavaScript
'name' in obj
//true
'toString' in obj
//true
~~~
obj.hasOwnProperty('key') 判断是否为自身属性，可与 'key' in obj 配合使用。
~~~JavaScript
obj.hasOwnProperty('age')
//true
obj.hasOwnProperty('toString')
//false
~~~
