### create-react-app  --全局安装环境

## cd 进入demo  执行 npm start 打开网页

let --es6声明变量的方式
	1.拥有块级作用域（只要在大括号内声明就会形成作用域）
	2.同一个作用于下不允许重复声明相同变量
	3.变量声明不提升,会警告；
	4.在 let 作用域内声明之前使用变量就会报错
const --es6声明变量的方式（用来声明常量的，声明的常量不允许被修改）
	特点同上^
*****
解构赋值（方便获取对象，数组，字符串的各项） --例子：

```
	--function fun({name}){
		console.log(name)
	}
	var  obj = {
		name:'zzt',
		age:12
	}
	fun(name)  输出->//zzt
```

字符串模板 --例子：

```
var ueername = 'zzt'
var age = 10
```
所有带变量的字符串的字符串都要用反引号套起来，变量用${}括起来

```
var c = `my name is ${username},my age is ${age}`
```

Arrows 箭头函数 --例子：
```
let [a,b]=[1,2]
function add(a,b){
   console.log(a+b)
}
let add = (a,b) => console.log(a+b)
```
//箭头左边的 参数除了一个之外 必须使用小括号，当只有一个参数的时候可省略小括号
//箭头右边 要做的事 当要做的事不止一句的时候，必须加上大括号；
//当只有一句的时候可以省略大括号，但是同时这句话会被当做该函数的返回值；
//当需要写函数的返回值的时候，需要在需要在大括号最后面添加 return
add(a,b)

1.箭头函数体内的this对象，就是定义时所在的对象，而不是调用时所在的对象。
2.不可以当做构造函数，也就是说不可以使用new命令，否则会报错。
3.不可以使用arguments对象，如果要使用，用rest代替。


es6 函数参数
//参数的默认值,直接在函数声明的时候在小括号内部给参数赋值，相当于给了参数默认值    -->
```
function fun （x=0，y=0）{
		return x*y
}
var z = fun()
console.log(z)
```

es6 函数参数的集合
...rest --学名为剩余参数（rest可更改，通常用rest表示）
```
let sum = (...rest) => console.log(rest)
sum(1,2,3,4,5,6,7,8,9) --->返回一个数组
```

Spread 扩展操作符  ...  ---非常重要！！！
对象的扩展（很多）以及数组的扩展。。
```
var arr = [1,2,3]
var arr1 = [4,5,6]
//var newarr = arr.concat(arr1)
var newarr = [...arr,...arr1]
```

例子2：

```
let arr = [1,2,3]
let arr1 = [...arr,4,5]
```
怎么拷贝新数组？！  ------

```
let arr = [1,2,3]
let arr1 = [...arr,4]
-->//arr = [1,2,3]  arr1 = [1,2,3,4]
```

对象的拷贝 -----
```
let obj = {
 name:'lijinlai',
 age:12
}
let obj1 = {...obj}
```


es6创建构造函数的写法

```
class Person{
  constructor(name){
    this.name = name
  }
  say(){
    console.log('hello')
  }
}
let people = new Person('li')
console.log(people)
people.say()
```

//class 内部只能写方法，并且方法之间不能加逗号
//constructor 函数 当执行 new + class名 的时候就会默认执行

//快捷键//ctrl+shift+K 删除当前行


构造函数的继承 -----

//之前的构造函数的继承
```
  function Person(firstname){
    this.firstname = firstname
  }
  Person.prototype.say = function(){
    console.log('hello')
  }
  var people = new Person('li')

  function Son(name){
    this.name = name
  }
  var son = new Son('li')
  console.log(son.firstname)
  son.say()
```


es6 写法

```
 class Person{
   constructor(name){
     this.name = name
   }
   say(){
     console.log('hello')
   }
 }
 let people = new Person('li')
 console.log(people)
 people.say()
 class Son extends Person{
   constructor(){
     super()
   }
   jump(){
     console.log('jump')
   }
 }
 let son = new Son()
 son.say()
 son.jump()
```

super() 的作用：处理this指向的  如果继承的话，子类constructor，内部必须添加super()，向 super 内部传参相当于向继承的父类传参；

```
  object.assgin()
  object.assgin(obj,obj1,.....) --把后面的所有对象合并到前面
  let obj= {
   name:'李丽'，
   age:12
  }
  let obj1 = object.assgin({},obj,{tall:180})  --相当于拷贝
  obj1.name = 'zzt'
  console.log(obj1,obj)
```


数组的一些方法 ----  :
filter-过滤

```
let objArr = [
 {name;'liu',age:11}
 {name;'liu',age:12}
 {name;'liu',age:15}
]
let newArr = objArr.filter(function(item){
 return item.age < 15
})
let newArr = objArr.filter(itemm =>item.age < 15)
console.log(newArr)
```

findIndex()  //找符合条件的索引值
```
 let arr = [1,2,3,4]
 let num = arr.findIndex( item => item === 3)
 console.log(arr[num])
```
map 通过原数组生成一个新的数组
```
 let arr = [1,2,3,4]
 let newArr = arr.map(item => item * item)
 console.log(newArr);
```
find 找寻符合条件的元素
```
 let arr = [{name:'li',age:12},{name:'zhang',age:12},{name:'li',age:13},{name:'li',age:15}]
 let obj = arr.find(item => item.name ==='zhang')
 console.log(obj);
```
sort  排序
```
 let arr = [1,23,5,6,33,67,13,11]
 arr.sort((a,b) => a-b)
 console.log(arr);
```
reduce 累加器或者叫多项数据连接

Objest.keys() 可以获取包含所有属性值的数组
```
 let obj = {
   name:'sunny',
   age:12,
   say(){
     console.log(this.name);
   }
 }
 ```
拿到一个包括obj对象所有属性值的数值   for in语句(以前的方法)
```
 for( let i in obj){
   console.log(obj[i]);
 }
es6 方法：
let arr = Object.keys(obj)
console.log(arr);
```

module.exportx = XXX  模块导出



直接引入全部的js   require('地址')


es6 导出方式：1.命名导出  2.默认导出
注意：模块导入必须写在当前模块的最顶端！

1.命名导出 ---
  需要导出的文件中填写 export{命名}；
  需要导入的文件中填写 import {a} from '导出的文件地址'
！！！命名导出的话 导入的变量名和到出的必须一致！！！
如果想更换名字的话： import {a as b} from '导出的文件地址'
 as 表示重命名的意思
如果想把导出的东西全部导入的话 则 ：import * as 变量 from '导出的文件地址'

2.默认导出 ---
  //需要导出的文件中填写  export default  
  //默认导出只能导出一个 不使用大括号
  //需要导入的文件中填写  import b from '导出的文件地址'
  //其中 b 为命名，可随意～
