<script>
 import Reactivity from "./01reactivity/01Reactivity.svelte";
 import Props from "./02props/02Props.svelte";
 import Logic from "./03logic/03Logic.svelte";
 import EventTest from "./04event/04Event.svelte";

 import Bind from "./05bind/index.svelte";

 let propsTest = {
     answer: "Svelte",
     answer1: "Test"
 }
</script>

<!--<Reactivity />-->

<!--
<Props answer="Hello World"/>
&lt;!&ndash;如果你的组件含有有一个对象属性，可以利用...语法将它们spread（传播）到一个组件上，而不用逐一指定：&ndash;&gt;
<Props {...propsTest}/>-->

<!--<Logic />-->

<!--<EventTest />-->

<Bind />