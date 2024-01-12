<script>
    let src = "../favicon.png";

    let string = "Hello World And <strong>Svelte</strong>";

    let count = 0;

    const click = () => {
        count++;
    }

    //反应式声明
    $: doubled = count * 2;

    //反应式语句
    $: console.log(`the count is ${count}`);

    $: {
        // console.log(`the count is ${count}`);
        // alert(`I SAID THE COUNT IS ${count}`);
    }

    $: if (count >= 10) {
        alert("count >= 10");
    }

    //更新数据和对象
    //由于 Svelte 的反应性是由赋值语句触发的，因此使用数组的诸如 push 和 splice 之类的方法就不会触发自动更新。例如，点击按钮就不会执行任何操作。
    //一个简单的经验法则是：被更新的变量的名称必须出现在赋值语句的左侧。
    let numbers = [];
    function addNumber() {
        numbers.push(numbers.length + 1);
        numbers = numbers;
    }

    function addNumber1() {
        numbers = [...numbers, numbers.length + 1];
    }
</script>

<!--<img src="{src}" alt="icon">-->
<!--同名元素缩写-->
<img {src} alt="icon">

<!--样式作用域被限定在当前组件中-->
<style>
    p {
        font-size: 50px;
        color: aqua;
    }
</style>

<p>Hello World</p>

<!--@html解析字符串中的html-->
<p>{string}</p>
<p>{@html string}</p>

<!--响应式-->
<button on:click={click}>
    click {count} {count === 1 ? "time" : "times"}
</button>

<!--反应式声明-->
<p>{count} doubled is {doubled}</p>