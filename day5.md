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