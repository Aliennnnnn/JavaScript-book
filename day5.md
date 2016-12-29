# Chapter 5.4
## RegExp类型
### RegExp
创造一个正则表达式：

```
var expression = / pattern / flags;
```
**其中的模式（pattern）部分可以是任何正则表达式，每个正则表达式都可带有一个或多个标志（flags），用以标明正则表达式的行为。**
- g：全局模式（global），将模式应用于所有字符串，而非在发现第一个匹配项时立即停止。
- i：表示不区分大小写。
- m：表示多行模式（multiline），即在一行文本结束后自动跳到下一行继续匹配。

```
var pattern1 = /at/g;
var pattern2 = /at/gi;
var pattern3 = /\.at/gi;

var pattern4 = /[bc]at/i;
var pattern5 = /\[bc\]at/i;

console.log(pattern.test('cat'));
```
`RegExpObject.test(string)`
检测一个字符串是否匹配某个模式。

若字符串中有下面这些元字符串，则必须转义。
`( [ { \ ^ $ | ? * + . } ] )`


另一个创建正则表达式的方法是使用`RegExp()`构造函数，它接受两个参数：第一个是要匹配的字符串模式（pattern），第二个是可选的标志（flags）
```
var pattern1 = /[bc]at/i;
var pattern2 = new RegExp("[bc]at","i");
//上面两个语句都代表匹配第一个"bat"或者cat
```


----------
### RegExp实例方法
RegExp对象的主要方法是`exec()`，向该方法内传入一个字符串，然后返回一个数组！！什么数组呢，就是包含第一个匹配项信息的数组，而且这个数组包含两个额外的属性：index和input。下面具体解释。

```
var text = 'mom and dad and baby';
var pattern = /mom( and dad( and baby)?)?/gi;

var matches = patterns.exec(text);

console.log(matches.index)//0
console.log(matches.input)//'mom and dad and baby'
console.log(matches[0])//' mom and dad and baby'
console.log(matches[1])//' and dad and baby'
console.log(matches[2])//' and baby'
```

**这样应该就很容易理解了，matches就是那个包含第一个匹配信息的数组，它的index方法表示第一次出现的位置，input方法表示应用正则表达式的字符串。matches[2]表示最里面的那个匹配项**


## Function类型
### 没有重载
**名字相同的两个函数，后面的那个函数会覆盖前面的那个函数。**

### 函数属性和方法
每个函数都包含两个属性：`length`和`prototype`。
length代表函数接收的命名参数

```
var sayHi(){
	console.log('hi');
}
var sayName(name){
	console.log(name);
}
var sum(num1,num2){
	console.log(num1+num2);
}

console.log(sayHi.length);//0
console.log(sayName.length);//1
console.log(sum.length);//2
```

prototype：原型，具体第六章讨论。

### apply()和call()
每个函数都包含两个非继承而来的方法：`apply()`和`call()`。
> **两个方法的用途都是在特定的作用域中调用函数，实际上等于设置函数体内this对象的值.**

`call()`方法和`apply()`方法作用相同，区别仅在与接收参数的方式不同。

- `apply()`：第一个参数是在其中运行函数的作用域，第二个是参数数组，但是第二个参数可以是数组实例，也可以是arguments对象。

```
function sum(num1,num2){
	return num1+num2;
}
function callSum1(num1,num2){
	return sum.apply(this,arguments);
}//传入arguments对象
function callSum2(num1,num2){
	return sum.apply(this,[num1,num2]);
}//传入数组
console.log(callSum1(10,55));//65
console.log(callSum2(10,55));//65
```


- 而`call()`方法第二个参数和`apply()`不同，它必须把传递给函数的参数逐个列举出来。

```
function sum(num1,num2){
	return num1 + num2;
}
function callSum(num1,num2){
	return sum.call(this,sum1,sum2);
}
console.log(callSum(10,55));//65
```
**也就是说，`call()`方法不能像`apply()`方法一样把要传递的参数存进一个数组传递进去，它必须把所有参数依次列举出来。**


----------
**然而这两个函数真正强大的地方在于能够扩充函数赖以运行的作用域。**

```
window.color = 'red';
var a = {color: "blue"};

function sayColor(){
	alert(this.color);
}

sayColor();				//red
sayColor.call(this);	//red
sayColor.call(window);	//red
sayColor.call(a);		//blue
```


----------


咳咳：划**重点**了，目前我对`apply()`和`call()`方法的其中一个理解就是：
**这两个方法可以改变this的指向，让一个没有某个方法的A函数可以用过改变B函数中的那个方法中this的指向来调用这个方法。**
比如：
```
function Animal(){
   	this.name = 'animallll';
   	this.showName = function(){
   	alert(this.name);
  }
}

function Cat(){
   	this.name = 'Catttt';
}

var animal = new Animal();
var cat = new Cat();

animal.showName.apply(cat);//Catttt
```
这段代码中`cat`并没有`showName`方法，但是可以通过修改`animal`中`showName`this的指向来使用该方法。

**特别注明，修改的是调用`call()`和`apply()`方法的实例中的this指向，指向`call()`或者`apply()`中第一个参数**


----------

```
function cat(){
	
}
cat.prototype = {
	food:'fish',
	say:function(){
		alert('I love'+ this.food);
	}
}
var blackCat = new cat();
blackCat.say();
```

> call 和 apply 都是为了改变某个函数运行时的 context 即上下文而存在的，换句话说，就是为了改变函数体内部 this 的指向。因为 JavaScript 的函数存在「定义时上下文」和「运行时上下文」以及「上下文是可以改变的」这样的概念。


