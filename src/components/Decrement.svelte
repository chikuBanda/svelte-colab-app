<script>
    import { count } from "../stores/mystore";
    const decrement = () => {
        count.update((n) => n - 1)
    }
</script>
<button on:click={decrement}>-</button>