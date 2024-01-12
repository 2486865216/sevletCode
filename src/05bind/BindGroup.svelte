<!--如果你需要绑定更多值，则可以使用bind:group 将 value 属性放在一起使用。 在bind:group中，同一组的单选框值是互斥的，同一组的复选框会形成一个数组。-->
<script>
    let scoops = 1;
    let flavours = ['Mint choc chip'];

    let menu = [
        'Cookies and cream',
        'Mint choc chip',
        'Raspberry ripple'
    ]

    function join (flavours) {
        if (flavours.length === 1) return flavours[0];
        return `${flavours.slice(0, -1).join(", ")} and ${flavours[flavours.length - 1]}`;
    }
</script>

<h1>size</h1>

<label>
    <input type="radio" bind:group={scoops} value="1">
    One scoop
</label>

<label>
    <input type="radio" bind:group={scoops} value="2">
    Two scoop
</label>

<label>
    <input type="radio" bind:group={scoops} value="3">
    Three scoop
</label>

<h1>Flavours</h1>

{#each menu as flavour}
    <label>
        <input type="checkbox" bind:group={flavours} value={flavour}>
        {flavour}
    </label>
{/each}

{#if flavours.length === 0}
    <p>Please select at least one flavour</p>
{:else if flavours.length > scoops}
    <p>Can't order more flavours than scoops!</p>
{:else}
    <p>
        You ordered {scoops} {scoops === 1 ? 'scoop' : 'scoops'}
        of {join(flavours)}
    </p>
{/if}

