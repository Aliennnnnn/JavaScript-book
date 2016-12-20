@(JS高级程序设计)

- `<noscript>`元素会在浏览器不支持脚本或者脚本被禁用时显示`<noscript></noscript>`中的内容。


----------


-  在函数内部使用隐式声明
```
function test(){
	message = 100;//全局变量
}
test();
alert(message);//100
```
这里的message省略了`var`操作符，所以message就成了全局变量。这样，只要调用过一次`test()`函数，这个变量就有了定义，不会被销毁。


----------
- 在函数内部使用显式声明
```
function test(){
	var message = 100;//局部变量
}
test();
alert(message);//错误
```
函数内部定义了一个名为message的局部变量，这个变量会在函数退出后被立即销毁。


----------
- 函数的参数是以数组的形式传入函数内部的，所以
```
function howManyArgs(){
	alert(arguements.length);
}

howManyArgs('string',2);  //2
howManyArgs();  		  //0
howManyArgs(11);  		  //1
```
arguements就是传入的参数(数组)。
```
function args(){
	alert(arguements[0]+arguements[1]);
}
args('Hello,','World!');//Hello,World!
```


