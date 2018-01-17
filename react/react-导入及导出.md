react安装 ： 命令行执行 apm install react ,然后重启 atom .

单页面应用
所有的 css 都是全局的，尽量所有命名不重复！
react 组件内部有一个默认的参数叫 props 作用是接收父组件传过来的参数
如果时函数组件的话 函数的第一个参数默认就是 props；
如果是 es6 class 组件的话 组件内部使用 this.props 获取 props


 在src中新建一个index.js文件 把其他的都删了
 这一步的意思是是JSX可以展示为js语法
```
 import React from 'react'
```
 这一步是使用ReactDom这个
 ```
 import ReactDom from 'react-dom'
 ```

举例1
 ```
ReactDom.render(<h1>hello world</h1>,document.getElementById('root'))
```

 // JSX 语法  可以在js内写html
 //1.严格区分大小写
 //2.标签必须是闭合的 单闭合标签 必须在后面 加上 /> 就可以了
 //3.一个JSX 节点必须包裹在一个闭合标签内
 //4.JSX 内部嵌套 js语法 使用大括号内部必须是一个值

另一种写法
```
	import React from 'react'
	import ReactDom from 'react-dom'
```
	举例1
  ```
	let ele = <h1>hello world</h1>
  ```
	举例2
  ```
	let ele = <input type="text"/>
  ```
	举例3
  ```
	let ele = <div> <h1>1</h1>
		        <h2>2</h2>
		  </div>
  ```
	举例4
  ```
	let a = 10
	const test =true
	let ele = <div>
	{test ? <span>{a}</span>:<h1>100</h1>}
	<h2>11</h2>
	</div>
	ReactDom.render(ele,document.getElementById('root'))
  ```

```
jsx 语法注释 使用 //单行注释  使用/**/是多行注释 和 js类似

JSX 中的注释方法：讲要注释的 JSX 用大括号包起来，然后用双斜杠（//）注释，或者用斜杠* 方法注释（/* xxx */）；
```
