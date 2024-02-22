<script lang="ts">
    import { onMount } from 'svelte';
    import chikuImage from '$lib/assets/img/chiku.jpeg'
    import androidImage from '$lib/assets/img/androidparty.png'
    import shapeCirle from '$lib/assets/img/circle.jpg'
    import shapeRect from '$lib/assets/img/rectangle.jpg'
    import Konva from 'konva';

    let addingvar = 0;
    let name: string = 'chiku banda'
    let selectedElement: string = ''

    let stage: Konva.Stage

    let layer: Konva.Layer

    let circle: Konva.Circle

    onMount(() => {
      // Access window.innerWidth and window.innerHeight only on the client side
      let width = window.innerWidth;
      let height = window.innerHeight;

      stage = new Konva.Stage({
        container: 'canvas-container',
        width: 1000,
        height: 1000
      })

      layer = new Konva.Layer()

      circle = new Konva.Circle({
        x: stage.width() / 2,
        y: stage.height() / 2,
        radius: 70,
        fill: 'red',
        stroke: 'black',
        strokeWidth: 4
      })

      layer.add(circle)

      stage.add(layer)

      stage.draw()

      document.getElementById("chiku_image")
        ?.addEventListener('dragstart', () => {
          selectedElement = "chiku_image"
        })

      document.getElementById("android_image")
        ?.addEventListener('dragstart', () => {
          selectedElement = "android_image"
        })

      document.getElementById("shape_circle")
        ?.addEventListener('dragstart', () => {
          selectedElement = "shape_circle"
        })

      document.getElementById("canvas-container")
        ?.addEventListener("dragover", (e) => {
          e.preventDefault()
        })

      document.addEventListener('drop', (e) => {
        e.preventDefault()

        stage.setPointersPositions(e)

        console.log('selectedElement', selectedElement)

        if (selectedElement === 'chiku_image') {
          Konva.Image.fromURL(chikuImage, (image) => {
            layer.add(image)
            
            if (stage.getPointerPosition() !== null) {
              // @ts-ignore
              image.position(stage.getPointerPosition())
              image.draggable(true)           
            }
          })
        }

        if (selectedElement === 'shape_circle') {
          const circle = new Konva.Circle({
            x: stage.width() / 2,
            y: stage.height() / 2,
            radius: 70,
            fill: 'blue',
            stroke: 'black',
            strokeWidth: 4,
          })

          layer.add(circle)
          if (stage.getPointerPosition() !== null) {
            // @ts-ignore
            circle.position(stage.getPointerPosition())
            circle.draggable(true)
          }
        }
      })

      console.log('My name is', name)
    });

    const addCircle = () => {
      if (selectedElement === 'shape_circle') {
        const circle = new Konva.Circle({
          x: stage.width() / 2,
          y: stage.height() / 2,
          radius: 70,
          fill: 'blue',
          stroke: 'black',
          strokeWidth: 4,
        })

        layer.add(circle)
        if (stage.getPointerPosition() !== null) {
          // @ts-ignore
          circle.position(stage.getPointerPosition())
          circle.draggable(true)
        }
      }

    }
</script>
  
<p class="mb-2 text-3xl font-bold underline bg-sky-900 text-stone-100">Hello tailwind {addingvar}</p>
<img id="chiku_image" src={chikuImage} width="100" draggable="true" alt="" />
<img id="android_image" src={androidImage} width="100" draggable="true" alt="" />
<button id="shape_circle" draggable="true" on:click={addCircle} class="bg-transparent border-0"><img src={shapeCirle} width="100" draggable="true" alt="" /></button>
<div id="canvas-container" class="bg-sky-300">

</div>
