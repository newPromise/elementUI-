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
