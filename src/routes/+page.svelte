<script lang="ts">
    import { onMount } from 'svelte';
    import { Layer, Stage, Rect } from 'svelte-konva'

    let addingvar = 0;
    let width: number;
    let height: number;
    let name: string = 'chiku banda'

    onMount(() => {
        // Access window.innerWidth and window.innerHeight only on the client side
        width = window.innerWidth;
        height = window.innerHeight;

      console.log('My name is', name)
    });
</script>
  
<p class="text-3xl font-bold underline bg-sky-900">Hello tailwind {addingvar}</p>
<Stage config={{ width: width, height: height }}>
    <Layer>
        <Rect config={{ x: 100, y: 100, width: 400, height: 200, fill: 'blue', draggable: true }} />
    </Layer>
</Stage>
