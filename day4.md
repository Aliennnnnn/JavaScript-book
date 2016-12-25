##
### 检测数组
讨论这个话题之前我们先要彻底搞明白`instanceof`。
**instance:实例**
eg.
  ` a instance of b ? alert('true') : alert('false');` 
  三元运算符，可以这么简单地理解`instanceof`。用来判断一个变量是否是某个对象的实例。如果a是b的一个实例，那么返回true，否则返回false；
```
var arr = [];
console.log(arr instanceoff Array)
//true
```


----------
### 转换方法
`valueOf()`：返回最适合该对象类型的原始值
`toString()`：将该对象的原始值以字符串形式返回
```
var colors = ['red','blue','green'];
alert(colors.toString());//red,blue,green
alert(colors.valueOf());//red,blue,green
alert(colors);//red,blue,green
```

`join()`方法，传入一个值作为数组项之间的分隔符，如果不传入或者传入undefined字符串，则默认使用逗号作为分隔符。

```
var colors = ['red','blue','green'];
console.log(colors);
console.log(colors.join());
console.log(colors.join('||'));
console.log(colors.join('undefined'));
```
上述代码依次返回
red,blue,green
red,blue,green
red||blue||green
red,blue,green


----------

`push()`：在数组末尾添加任意个项
`pop()`：删除数组最后一项并返回删除的项
```
var colors = ['red','blue'];
colors.push('black','green');

var item = colors.pop();
console.log(item);//'green'
```
`shift()`：删除数组的第一项并返回被删除的项
`unshift()`：在数组的前端添加任意个项


----------
### 重排序方法
`sort()`：调用`toString()`方法，比较字符串，即使数组中的每一项都是数值，默认按升序排列数组项。



```
var arr =['apple','Apple','Orange','Banana'];
console.log(arr.sort());
//'Apple','Banana','Orange','apple'

```
**可以看出sort是按ASCII码来排序的**
```
var arr = [11,1,15,5];
console.log(arr.sort());
//1,11,15,5
```
**即使数组中全都是数值也会调用`toString()`方法先转换成字符串再按照ASCII码进行比较。**

很明显这个是不符合我们平时大多数使用场景的，想要让数组中的数值按照其本身大小进行排序也很简单：
- 降序排列
```
var arr = [1,2,5,4,9,15]; 
function sortNumber(a,b){
	return b - a;
} 
console.log(arr.sort(sortNumber));
//15,9,5,4,2,1
```
- 升序排列
```
var arr = [1,2,5,4,9,15]; 
function sortNumber(a,b){
	return a - b;
} 
console.log(arr.sort(sortNumber));
//1,2,4,5,9,15
```


----------
### 操作方法
`concat()`：连接两个或者多个数组，该方法不会改变现有的数组，而回返回被连接数组的一个副本。

```
var arr =['apple','Apple','Orange','Banana'];
var arr1 = [1,2,3];
var arr2 = [4,5,6];
var arrT = arr.concat(arr1,arr2);
console.log(arrT);
//'Apple','Banana','Orange','apple',1,2,3,4,5,6
```

`slice()`：slice意为“切下；划分”，由字面意思很容易理解这个方法，就是把原有的数组切片，返回切下的数组元素。

`arrayObject.slice(start,end)`
**start，end都是数组元素的下标**

start：必需，规定从何处开始选取，如果为负数就代表从数组尾部开始算起，-1代表最后一个元素，以此类推。
end：可选，规定从何处结束，不指定该参数的话默认到数组结尾的所有元素。
**该方法返回一个新的数组，并不会改变原数组**
```
var arr = [1,2,3,4,5];
var arrT = arr.slice(1,3);
var arrT2 = arr.slice(-3,-1);
console.log(arrT);	//2,3
console.log(arrT2);	//3,4
```

`splice()`：最强大的数组方法。可以删除、插入、替换数组元素。

**`splice()`方法不同于`slice()`和`concat()`方法，它会改变原来的数组。**

- 删除：`splice(0,2)`删除前两项，第一个参数代表从第几项开始，第二个参数代表要删除几项。
**删除时返回值为被删除的值**
```
var arr = ['blue','red','green','purple'];
var arrT = arr.splice(0,2);
console.log(arr);//'green','purple'
console.log(arrT);//'blue','red'

```

- 插入：可以向任意位置插入任意个项。`splice(1,0,'red')`：在第二项的后面删除零个元素然后插入’red‘。
**插入时第二个参数必须为0，代表不删除任何元素，仅插入**

- 替换：`splice(1,1,'hello')`,将第二项的后面一项替换成’hello‘


----------
### 位置方法
`indexOf()`返回要查找的元素在数组或字符串中首次出现的位置。
`object.indexOf(searchValue,start)`;

```
var numbers = [4,2,5,7,3,2];
console.log(numbers.indexOf(2));//1
console.log(numbers.indexOf(2,2));//5


var str = 'Hello world,welcome to the universe.';
console.log(str.indexOf("welcom"));
//13
```
----------
### 迭代方法
**传入迭代方法中的函数会接收三个参数：item,index,array.即数组项的值，该项在数组中的位置和数组对象本身**

`filter()`：对数组中的每一项运行给定函数，返回该函数会返回true的项组成的数组。

```
var numbers = [2,3,1,6,3,9,7];
console.log(numbers.filter(
	function(item,index,array){
		return (item>2);//3,6,3,9,7
	}
))
```


----------
## 5.3 Date类型

    getTime()
    getFullYear()
    getMonth()
    getDate()
    getDay()
    getHours()
    getMinutes()
    getSeconds()
