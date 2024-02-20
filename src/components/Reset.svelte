<script>
    import { count } from "../stores/mystore";
    const reset = () => {
        count.set(0)
    }
</script>
<button on:click={reset}>Reset</button>