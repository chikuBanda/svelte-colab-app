<script>
    import { count } from "../stores/mystore";
    const increment = () => {
        count.update((n) => n + 1)
    }
</script>
<button on:click={increment}>+</button>