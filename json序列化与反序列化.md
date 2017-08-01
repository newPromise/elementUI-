### JSON 实现序列化与反序列化
_ _ _
#### 为什么要使用序列化：
对象形式
```
var person = {
  name: '张宁宁',
  age: 22
}
```
json形式：

```
{
"name": "张宁宁",
"age": 22
}
```
那么我们为什么要使用序列化呢？

>我们常见的json形式是我们前端向后台传送数据的时候，后台接收到的是json数据的格式，因此我们通过使用JSON.stringfy 的方法将对象转化为json字符串的格式
为什么要转化呢？
>

序列化和反序列化，我们可以理解为数据的编码和解码的过程，上面我们说的前台向后端传递数据的时候，我们要进行转化，因为前端使用的是js,然而后端是用的是java，  
这种跨语言的传递数据，我们想通过一种数据的格式，对于不同的语言都能够接受数据，这种形式就是json
不仅如此，例如我们使用storage存储数据到本地的时候，我们也要接受json的形式：

#### 两种方法：

1，JSON.stringify () 
代码如下：

```
let person = {
  name: '张宁宁',
  age: 22
}

JSON.stringify(person)
// {"name": "张宁宁","age": 22}
```
>注意，使用这个方法的时候要注意,对于对象的属性为函数和 undefined 的是无法进行转换的
>

````
let obj = {
  a: 'a',
  b: function () {},
  c: undefined
}

JSON.stringify(obj)
// {"a": "a"}
````
对于 undefined 和 函数属性，使用 JSON.stringfiy 是无法进行转化的，因此我们需要定义改变这个方法的 参数
>  
JSON.stringify(value,replace,space)
value:要进行格式化的值

replace: 用来定义要进行替代的函数

space：定位符

>使用 toString 的方法可以让函数输出function,其实，使用  JSON.stringify()的方法使用的是方式和 toString 是类似的，不同的是，使用JSON方法可以将对象转化为字符串的形式，但是对于 对象中的属性方法，undefined 值，那么使用 JSON.stringify 就不尽人意、了
>
当我们要试图将对象中的属性方法和undefined转换为字符串的格式，我们使用toString 方法：
```
k: key 传入属性的键
v: value 传入属性的值
const replace = function (k,v) {
if (typeof v ===  'function') {
   return Function.prototype.toString.call(v)
} else  if ( v === 'undefined') {
   return 'undefined'
}
  return v;
}
let person = {
  name: 'zhangning',
  age: 12,
  fn: function () {
    return 2;
  },
  homne: undefined
}
console.log(JSON.stringify(person,replace))
```
