<script>
    import {createEventDispatcher} from "svelte";

    const dispatch = createEventDispatcher();

    function sayHello () {
        //分发自定义事件, message:自定义事件key, {}:自定义事件返回的数据,使用event.detail对象调用
        dispatch("message", {
            text: "Hello!"
        })
    }
</script>

<button on:click={sayHello}>
    Click me say Hello
</button>