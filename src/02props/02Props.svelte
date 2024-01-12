<script>
    //导出props
    export let answer;

    //默认值
    export let answer1 = "a mystery";
    //如果你的组件含有有一个对象属性，可以利用...语法将它们spread（传播）到一个组件上，而不用逐一指定：
</script>

<p>{answer}</p>
<p>{answer1}</p>

<style>
    p{
        font-size: 50px;
        color: aquamarine;
    }
</style>