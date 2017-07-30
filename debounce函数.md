这个函数用于防止一个动作被调用多次，使用的思路是：在动作发生一段时间之后调用函数，如果在这段时间之内，重复调用函数，那么时间重新计算
```
html
<input type="text" v-model="inputText" >

vue

data () {
  return {
    last: null,
    inputText: ''
  }
}
watch : {
  inputText: function (value) {
    if (value) this.debounce(this.fn,2000)
  }
},
methods: {
 /** 
 *@decription: debounce函数，用于防止弹动的操作
 *@param{function} 之后执行的函数
 *@delay: 延迟时间 
 **/
  debounce (fn,delay) {
    clearTimeout(this.last);
    this.last = setTimeout(
      function () {
      // 使用apply的时候，调用 fn的时候将this绑定到this上
        fn.apply(this,arguments)
      },delay)
  }
}
```
这个函数的目的是防止按钮点击的时候调用多次函数
>对于call () 函数和 apply()函数
>
call apply 函数用于将改变this的绑定值

obj.call(thisObj)  将obj 的this值绑定在thisObj 上或者说： thisObj 继承了obj的属性和方法
