# chapter 4
# 变量、作用域和内存问题

### 动态的属性
基本数据类型：Undefined、Null、Boolean、Number和String。
引用类型：值保存在内存中的对象。
```
var person = new Object();
person.name = 'Wang';
console.log(person.name);//Wang
```
上述代码创建一个对象，然后将其保存在变量person中，然后我们为该对象添加了一个名为name的属性，并将字符串’Wang‘赋给这个属性。

但是，我们不能给基本数据类型的值添加任何属性。
```
var name = 'Wang';
name.age = 21;
console.log(name.age);//undefined
```
### 传递参数

```
function setName(obj){
	obj.name = 'mark';
	obj = new Object();//这个obj是局部变量，不能影响全局变量
	obj.name = 'Alice';
	alert(obj.name)//Alice
}
var person = new Object();
setName(person);
alert(person.name);//mark
```
在内部重写obj的name属性时，其实修改的是局部对象，原始引用未被改变。

### 作用域链
> 当代码在一个环境中执行时，会创建变量对象的的一个作用域链（scope chain）。作用域链的用途，是保证对执行环境有权访问的所有变量和函数的有序访问。作用域链的前端，始终都是当前执行的代码所在环境的变量对象。如果这个环境是一个函数，则将其活动对象作为变量对象。

> ```
var color  = "blue";
function changeColor(){
	var anotherColor = "red";
	function swapColor(){
		var tempColor = anothorColor;
		anothorColor = color;
		color = tempColor;
		//这里可以访问到color,anothorColortempColor
	}
	//这里可以访问到color,anothorColor
}
//这里只能访问到color
> ```

### 没有块级作用域
> Q：什么叫块级作用域？
> A：任何一对花括号和圆括号中的语句集都属于一个快，在这之中定义的所有变量在代码块外都是不可见的（局部变量）,我们称之为块级作用域。
> Q：什么叫函数作用域？
> A：定义在函数中的参数和变量在函数外部是不可见的。



JS不像Java，C，C++那样有块级作用域，但JS有函数作用域
**也就是说呢，JS除了认得函数的花括号外其他的花括号都不认！**
再解释一下，也就是说除了函数的花括号内定义的变量，其他花括号和圆括号内的参数和变量在代码块外都是可以访问的。
eg.

```
function test(){
	for(var i = 0;i<5;i++){
		console.log(i);//0,1,2,3,4
		var j = 99;
	}
	consolo.log(i);//5
	console.log(j);//99
}
```
按理说上面代码中的for语句外输出的应该是undefined，但是奈何JS不把for语句的圆括号内的代码集当做一个独立的作用域，所以for语句外可以访问for语句内的变量。