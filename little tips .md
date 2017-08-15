>实现文本框 focus 的时候自动选中的功能  
>  
<input type = "text"   @focus = "$event.target.select()"> 当input框被选中的时候，被点击到的内容被选中到
>$event: 表示选中事件   $event.target: 表示事件被作用到得目标对象   $event.target.select() focus 事件被选中的目标对象被选中
>  
