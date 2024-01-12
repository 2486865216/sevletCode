<script>
    let user = {
        loggedIn: false
    }

    function toggle() {
        user.loggedIn = !user.loggedIn;
    }

    let x = 7;

    let cats = [
        { id: 'J---aiyznGQ', name: 'Keyboard Cat' },
        { id: 'z_AbfPXTKms', name: 'Maru' },
        { id: 'OUtn3pvWmpg', name: 'Henri The Existential Cat' }
    ];

    //为each添加key
    import Thing from './03Thing.svelte';

    let things = [
        { id: 1, color: '#0d0887' },
        { id: 2, color: '#6a00a8' },
        { id: 3, color: '#b12a90' },
        { id: 4, color: '#e16462' },
        { id: 5, color: '#fca636' }
    ];

    function handleClick() {
        things = things.slice(1);
    }

    //await
    let promise = getRandomNumber();

    async function getRandomNumber() {
        // const res = await fetch(`tutorial/random-number`);
        const res = await fetch(`/index.html`);
        const text = await res.text();

        if (res.ok) {
            return text;
        } else {
            throw new Error(text);
        }
    }

    function handlePromise() {
        promise = getRandomNumber();
    }
</script>

<!--if-->
{#if user.loggedIn}
    <button on:click={toggle}>log out</button>
{/if}

{#if !user.loggedIn}
    <button on:click={toggle}>log in</button>
{/if}

<!--if else-->
{#if user.loggedIn}
    <button on:click={toggle}>log out</button>
{:else}
    <button on:click={toggle}>log in</button>
{/if}

<!--if else if-->
{#if x > 10}
    <p>{x} is greater than 10</p>
{:else if 5 > x}
    <p>{x} is less than 5</p>
{:else}
    <p>{x} is between 5 and 10</p>
{/if}

<!--each-->
<!--表达式 cats是一个数组，遇到数组或类似于数组的对象 (即具有length 属性)。你都可以通过 each [...iterable]遍历迭代该对象。-->
<h1>The Famous Cats of YouTube</h1>
<ul>
    {#each cats as cat}
        <li>
            <a target="_blank" href="https://www.youtube.com/watch?v={cat.id}">
                {cat.name}
            </a>
        </li>
    {/each}
</ul>
<!--你也可以将index 作为第二个参数(key)，类似于：-->
<ul>
    {#each cats as cat,i}
        <li>
            <a target="_blank" href="https://www.youtube.com/watch?v={cat.id}">
                {i + 1}:{cat.name}
            </a>
        </li>
    {/each}
</ul>
<!--如果你希望代码更加健壮，你可以使用each cats as { id, name }来解构，用cat.id 和 cat.name 来代替 id 和 name。-->
<ul>
    {#each cats as {id, name}, i}
        <li>
            <a target="_blank" href="https://www.youtube.com/watch?v={id}">
                {i + 1}:{name}
            </a>
        </li>
    {/each}
</ul>

<!--尝试多次点击'Remove first thing' 按钮，这时<Thing> 组件是从尾端开始被移除，这显然不是我们想要的，我们希望是从上至下依次开始删除组件。-->
<!--(thing.id) 告诉 Svelte 什么地方需要改变。-->
<!--Svelte只会对比数量，然后从尾部开始删除旧的-->
<button on:click={handleClick}>
    Remove first thing
</button>

<!--
{#each things as thing}
    <Thing current={thing.color}/>
{/each}
-->

{#each things as thing (thing.id)}
    <Thing current={thing.color}/>
{/each}

<!--await-->
<button on:click={handlePromise}>
    generate random number
</button>

{#await promise}
    <p>...waiting</p>
{:then number}
    <p>The number is {number}</p>
{:catch error}
    <p style="color: red">{error.message}</p>
{/await}

<!--如果你的知道你的 promise 返回错误，则可以忽略 catch 块。如果在请求完成之前不想程序执行任何操作，也可以忽略第一个块。-->
{#await promise then value}
    <p>the value is {value}</p>
{/await}