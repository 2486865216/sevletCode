<!--作为一般规则，Svelte 中的数据流是自上而下的——父组件可以在子组件上设置 props，组件可以在元素上设置属性，但反之则不然。

有时打破这条规则很有用。以此组件中的元素为例 — 我们可以添加一个将值设置为 的事件处理程序，但这有点...样板。正如我们将看到的，使用其他表单元素时情况会变得更糟。

相反，我们可以使用指令：bind:value。这意味着不仅对属兔的值的更改将更新输入值，而且对输入值的更改也会更新-->
<script>
    let name = "world"

    //在DOM中，一切皆字符串，意味着每次使用数字之前要强制转换, bind:value会帮你转换
    let a = 1;
    let b = 2;

    //我们不仅可以使用input.value，也可以将复选状态绑定input.checked将复选框的状态绑定：
    let yes = true;

    //bind:group
    import BindGroup from "./BindGroup.svelte";

    //文本域
    import {marked} from "marked";
    let value = `Some words are *italic*, some are **bold**`;

    //contenteditable绑定
    let html = "<p>Write some text!</p>";
</script>

<input bind:value={name}>

<h1>Hello {name}</h1>

<label>
    <input type=number bind:value={a} min=0 max=10>
    <input type=range bind:value={a} min=0 max=10>
</label>

<label>
    <input type=number bind:value={b} min=0 max=10>
    <input type=range bind:value={b} min=0 max=10>
</label>

<p>{a} + {b} = {a + b}</p>

<!--我们不仅可以使用input.value，也可以将复选状态绑定input.checked将复选框的状态绑定：-->
<label>
    <input type=checkbox bind:checked={yes}>
    Yes! Send me regular email spam
</label>

{#if yes}
    <p>Thank you. We will bombard your inbox and sell your personal details.</p>
{:else}
    <p>You must opt in to continue. If you're not paying, you're the product.</p>
{/if}

<button disabled={!yes}>
    Subscribe
</button>

<BindGroup />

<!--文本域-->
<style>
    textarea { width: 100%; height: 200px; }

    /*contenteditable绑定*/
    [contenteditable] {
        padding: 0.5em;
        border: 1px solid #eee;
        border-radius: 4px;
    }
</style>
<!--如果值与变量名相同，我们也可以使用简写形式：-->
<textarea bind:value></textarea>

{@html marked(value)}

<!--contenteditable绑定-->
<div contenteditable="true" bind:innerHTML={html}></div>

<pre>{@html html}</pre>