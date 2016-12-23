# chapter 5
# 引用类型
```
var colors = ['red','blue','green'];
colors[2] = 'black';
colors[4] = 'brown';
console.log(colors[2]);
console.log(colors[3]);
console.log(colors.length);
```
在设置数组的值时，方括号内的索引值如果小于数组的长度，则原来的值被替换；如果方括号的内索引值大于等于数组的长度，那么数组的长度自动增加到索引值+1。

**数组的长度length并不是只读的！！！**

```
var colors = ['red','blue','green'];
colors.length = 2;
colors.length = 3;
console.log(colors[2]);//undefined
```
这段代码啥意思呢？
也就是说：当你设置数组的length小于数组的项数时，多出来的项会被扔掉，再也找不回来了！


----------


```
var colors = ['red','blue','green'];
colors.length = 4;
console.log(colors[4]);//undefined
```
这段代码又是啥意思呢？
也就是说：当你设置数组的length大于数组的项数时，会自动增加数组的长度至设定值，但是多出来的项仍为undefined。


----------
**我们也可以利用数组的长度来方便地在数组末尾添加新项**

``` 
var colors = ['red','blue','green'];
colors[colors.length] = 'black';
colors[colors.length] = 'yellow';

console.log(colors);
//['red','blue','green','black','yellow']
```
