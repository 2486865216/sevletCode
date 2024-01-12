<script>
    import Inner from "./04Inner.svelte";

    // import {createEventDispatcher} from "svelte";
    // const dispatch = createEventDispatcher();

    //组件之间的事件不会冒泡，要手动转发
    /*function forward(event) {
        dispatch("message", event.detail)
    }*/
</script>

<!--<Inner on:message={forward}/>-->

<!--但这样书写似乎有些臃肿，因此 Svelte 设立了一个简写属性 。 没有赋予特定的值的情况下意味着转发所有事件：-->
<Inner on:message />