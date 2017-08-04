```
<template>
    <div>
        <p>我是一段文字</p>
        <button v-debounce="{methods:active,args: [2,3,5,6]}">点击按钮</button>
    </div>
</template>
<script type="text/javascript">
    export default {
        name: 'direction',
        data () {
            return {
            };
        },
        directives: {
            debounce: {
                bind: function (el, binding) {
                    var value = binding.value;
                    el.callBackFn = function () {
                        value.methods.call(this, ...value.args);
                    };
                    el.timer = function () {
                        el.timeOut = setTimeout(el.callBackFn, 3000);
                    };
                    el.addEventListener('click', function () {
                        clearTimeout(el.timeOut);
                        el.timer();
                    });
                }
            }
        },
        methods: {
            active (a, b, c, d) {
                console.log(a);
                console.log('yes');
            }
        }
    };
</script>
<style type="text/stylus">

</style>

```


```
import Vue from 'vue';
/** 防抖指令 **/
Vue.directive('debounce', {
    bind: (el, binding) => {
        let value = binding.value;
        el.callBackFn = function () {
            value.methods.call(this, ...value.args);
        };
        el.timer = function () {
            el.timeOut = setTimeout(el.callBackFn, 2000);
        };
        el.addEventListener('click', function () {
            clearTimeout(el.timeOut);
            el.timer();
        });
    }
});
Vue.directive('linkClick', {
    bind: (el, binding) => {
        console.log('yes');
        let value = binding.value;
        console.log(value.activeClass);
        el.addEventListener('click', function () {
            el.className = value.activeClass;
        });
    }
});
```

如何引入：

```
<button v-debounce="{methods:action,args: [2,3,4,5]}">点击事件</button>
        <p v-linkClick="{activeClass:'active'}">这是一个链接</p>
    </div>
</template>
<script>
    import { debounce, linkClick } from '../assets/js/directive';
    export default {
        name: 'index',
        derectives: {
            debounce,
            linkClick
        },
        methods: {
            action (a, b, c, d) {
                console.log(a, b, c, d);
                console.log('yes');
            }
        }
```
