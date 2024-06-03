# 什么是jQuery？

一个优秀的 JS 库，封装了JavaScript 的一些方法，使得操作 JavaScript dom 更加方便



# 原生JavaScript操作 jQuery

## 1.导入jQuery包

```html
<script type='text/javascript' src="./js/jquery-3.7.1.js"></script>
```

## 2.使用jQuery函数

```html
<script type='text/javascript' src="./js/jquery-3.7.1.js"></script>
<script type='text/javascript'>
    $(document).ready(function(){
        alert("hello")
    })
</script>
```

### 结果：

```
hello
```

### 解析：

> - $是jQuery的函数名称，document是参数，作用是document对象变成jQuery可以使用的对象
> - ready是jQuery的函数，当页面dom对象加载完成后，会执行ready函数的内容，相当于onload
> - function() 是自定义函数，表示onload（dom对象加载完成）后要执行的代码
> - 这种写法是**标准写法**

# jQuery标准写法的快捷写法

```javascript
$(function(){
	alert("hello")
})
```

这种方法等同于

```javascript
$(document).ready(function(){
    alert("hello")
})
```

以下写法互相等价：

- $(document).ready()
- $()
- jQuery()
- window.jQuery()



# dom对象 和 jQuery对象

> dom 对象就是JavaScript对象，由JavaScript原生方法生成的对象

> jQuery对象就是由jQuery语法创建的对象，jQuery表示的对象都是数组
>
> 例如：var job1 = $("#text1")
> 		其中，job1就是一个jQuery对象，是一个数组

> dom 对象和 jQuery 对象 可以互转
>
> - $(dom对象) -> jQuery对象
> - a[0] -> dom对象
> - a.get(0) -> dom对象



# jQuery基本选择器

jQuery选择器是jQuery的核心，常用的选择器有：

- id 选择器
  - 语法：${"dom对象的id"}
- class 选择器
  - 语法： ${"**.**class名"}
- 标签 选择器
  - 语法：${"标签名称"}
- 所有 选择器
  - 语法：${"*"}
- 组合 选择器
  - 语法：${"#id,.class,标签"}

## 例子

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>第二个例子</title>
		<style type="text/css">
			div{
				background: gray;
				width: 200px;
				height: 100px;
			}
		</style>
		<script type="text/javascript" src="js/jquery-3.7.1.js"></script>
		<script type="text/javascript">
			function fun1(){
				// jQuery选择器选择id
				var obj = $("#one")
				// 改变样式
				obj.css("background","red")
			}
			
			function fun2(){
				// jQuery选择器选择class
				var obj = $(".two")
				obj.css("background","yellow")
			}
			
			function fun3(){
				// jQuery选择器选择 标签
				var obj = $("div")
				obj.css("background","orange")
			}
			
			function fun4(){
				var obj = $("*")
				obj.css("background","blue")
			}
			
			function fun5(){
				var obj = $(".two,span")
				obj.css("background","green")
			}
		</script>
	</head>
	<body>
		<div id="one">我是one</div><br/>
		<div class="two">我是two</div><br/>
		<div>我没有id和class</div><br/>
		<span>span</span><br/>
		<input type="button" value="获取id = one 的元素" onclick="fun1()">
		<input type="button" value="获取class = two 的元素" onclick="fun2()">
		<input type="button" value="获取div的元素" onclick="fun3()">
		<input type="button" value="所有选择器" onclick="fun4()">
		<input type="button" value="组合选择器" onclick="fun5()">
	</body>
</html>
```



# 表单选择器

表单选择器是指：文本框、单选框、复选框、下拉列表 等元素的选择方式，该方法无论是否存在表单 <form>，都可以做出相应的选择
表单选择器是为了更加容易地操作表单，表单选择器是根据元素类型来定义的

```html
<!--表单类型-->
<input type="text"></input>
<input type="password"></input>
<input type="radio"></input>
<input type="checkbox"></input>
<input type="button"></input>
<input type="file"></input>
<input type="submit"></input>
<input type="reset"></input>
```

## 表单选择器语法：

```javascript
$(":type属性值")
- $(":text")：选取所有的单行文本框
- $(":password")：选取所有的密码文本框
- $(":radio")：选取所有的单选框
- $(":checkbox")：选取所有的多选文本框
```

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="js/jquery-3.7.1.js"></script>
		<script type="text/javascript">
			function fun1(){
				var obj = $(":text")
				alert(obj.val());
			}
			
			function fun2(){
				var obj = $(":radio")
				for(let i = 0; i < obj.length;i ++){
					alert(obj[i].value)
				}
			}
		</script>
	</head>
	<body>
		<input type="text" value="type=text"></br>
		<input type="radio" value="man">
		<input type="radio" value="woman"></br>
		<input type="button" onclick="fun1()" value="查看text">
		<input type="button" onclick="fun2()" value="查看radio">
	</body>
</html>
```



# 过滤器

> 对已经找到的dom对象进行过滤，留下需要的对象

在html中定义了dom对象的时候，统一标签将会被设置为不同的dom对象顺序，例如：

```html
<div>1</div>		dom1
<div>2</div>		dom2
<div>3</div>		dom3
```

因此，使用选择器选择时，会同时选中 dom1、dom2、dom3

```javascript
$("div") == [dom1,dom2,dom3]
```

而过滤器可以用于过滤不需要的dom或不满足条件的dom

## 基本过滤器

- first：选择第一个
- last：选择最后一个
- eq：选中某一个索引
- lt：选择小于某个索引
- gt：选择大于某个索引

### first

> 用于保留第一个dom对象

```javascript
$("选择器:first")
```

### last

> 保留最后一个dom对象

```javascript
$("选择器:last")
```

### eq()

> 选择指定的对象

```javascript
$("选择器:eq(数组索引)")
```

### lt()

> 选择小于指定索引的所有对象

```javascript
$("选择器:lt(数组索引)")
```

### gt()

> 选择大于指定索引的所有对象

```javascript
$("选择器:gt(数组索引)")
```

## 表单对象属性过滤器

根据表单中dom对象状态情况来定位dom对象的
比如：

- 启用状态 enabled
- 禁用状态 disable
- 选中状态 checked等

### 选择可用的文本框

```javascript
$(":text:enabled")
```

### 选择不可用的文本框

```javascript
$(":text:disabled")
```

### 选择复选框选中的元素

```javascript
$(":checkbox:checked")
```

### 选择指定下拉列表的被选中的元素

> 选择器 **>** option:selected
> 父对象>子对象

```javascript
var obj = $("select>option:selected")
```

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="js/jquery-3.7.1.js"></script>
		<script type="text/javascript">
			function fun1(){
				var obj = $(":text:enabled")
				alert(obj.val())
			}
			
			function fun2(){
				var obj = $(":checkbox:checked")
				alert(obj.val())
			}
			
			function fun3(){
				var obj = $("select>option:selected")
				alert(obj.val())
			}
		</script>
	</head>
	<body>
		<input type="text" value="text enabled">
		<input type="text" value="text disabled" disabled><br/>
		<input type="checkbox" value="not check">
		<input type="checkbox" value="box is checked" checked>
		<input type="checkbox" value="box is checked" checked><br/>
		<select>
			<option value="not selected">没选中</option>
			<option value="is selected" selected>选中</option>
		</select><br/><br/>
		<input type="button" value="form表单过滤-text" onclick="fun1()">
		<input type="button" value="form表单过滤-checkbox" onclick="fun2()">
		<input type="button" value="form表单过滤-select" onclick="fun3()">
	</body>
</html>
```



# 事件

$(选择器).事件名称(事件处理函数)

- $(选择器)：用来定位 dom 对象的，dom对象可以有多个，表示这些对象均绑定了事件
- 事件名称：就是JavaScript中事件去掉"on"的部分，如onclick() -> click()
- 事件处理函数：是一个function，当事件发生时，会执行其中的内容

例如：给 id 为 btn 的按钮绑定一个单击事件

```javascript
$("#btn").click(function(){
	alert("1");
})
```

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script type="text/javascript" src="js/jquery-3.7.1.js"></script>
		<script type="text/javascript">
			$(function(){
				// 因为input是组件，需要等待dom完全创建后才能点击，所以需要用到jQuery特性
				$("#btn").click(function(){
					alert("1");
				})
			})
		</script>
	</head>
	<body>
		<input type="button" id="btn" value="按下事件">
	</body>
</html>
```





# 函数

## 第一组

### val

操作数组中 dom 对象的 value 属性

- $(选择器).val()：无参调用形式，**读取**数组中的第一个dom对象的value属性值
- $(选择器).val(值)：有参调用形式，**设置**数组中所有dom对象的value属性值

### text

操作数组中所有 dom 对象的【文字显示内容属性】

- $(选择器).text()：读取所有文字显示内容，将得到的内容拼接成一个字符串返回
- $(选择器).text(值)：对所有dom对象的文字内容进行赋值

### attr

对除了 val ,text 之外的属性操作

- $(选择器).attr("属性名")：获取 dom 数组第一个对象的属性值
- $(选择器).attr("属性名","值")：对数组中所有dom对象的属性赋值

## 第二组

### remove

$(选择器).remove()：将数组中所有dom对象及其子对象一并删除

### empty

$(选择器).empty()：将数组中所有dom对象的子对象删除

### append

对数组中所有的dom对象添加子对象

```javascript
$(选择器).append("<div>动态添加</div>")
```

### html

设置或返回被选中元素的内容(innerHTML)

- $(选择器).html()：无参调用，获取dom数组中第一个元素的内容
- $(选择器).html(值)：有参调用，设置dom数组中所有元素的内容

### each

对数组、json、dom数组的遍历，每个元素调用一次函数

- $.each(遍历对象,function(index,element){处理逻辑})
  - index：下标
  - element：数组的每个对象
- jQuery 对象.each(function(index,element){处理逻辑})



# on()

绑定事件，推荐使用该方法，该方法更加灵活通用

语法：$(选择器).on(event,function)
event：事件，一个或多个，多个之间以空格划分
function：可选，规定当事件发生时运行的函数

例如：

```javascript
<input type="button" id="btn">
$("#btn").on("click",function(){处理事件})
```



# AJAX（重点）

> 在没有 jQuery 之前，使用 XMLHttpRequest 做 ajax，有4个步骤（繁琐）

**使用步骤**

1. 创建异步对象
   1. var xmlHttp = new XMLHttpRequest()
2. 绑定事件
   1. xmlHttp.onreadystatechange=function(){获取服务端返回的数据，更新dom}
3. 初始化请求参数
   1. xmlHttp.open(get,url,true)
4. 发送请求 xmlHttp.send()

**属性**

- readyState：ajax 请求过程中的状态变化 ；4:表示从服务端返回数据，并处理完成
- status：网络通信的状态，200：通信成功；404：资源没有找到等

**同步和异步**

- 异步
  - open(get,url,true)：在 send 之后执行其他代码，可以同时执行多个异步请求
- 同步
  - open(get,url,false)：一次只能执行一个异步请求，必须请求处理完成之后，才能执行其他请求处理

> jQuery 简化了 AJAX 的处理，总的来说只用三个函数就可以实现 AJAX 请求的处理

- $.ajax()：jQuery 中实现 ajax 的核心函数，参数是一个json的结构
- $.post()：使用 post 做 ajax 请求
- $.get()：使用 get 做 ajax 请求

$.post() 和 $.get() 他们在内部都是调用的 $.ajax()



