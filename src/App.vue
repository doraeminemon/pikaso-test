<script setup>
import HelloWorld from './components/HelloWorld.vue'
import Pikaso, { ShapeModel } from 'pikaso';
import { onMounted, ref } from 'vue';

const editor = ref(null)

onMounted(() => {
  const container = window.document.querySelector('#canvas-container')
  const pikaso = new Pikaso({
    container,
    width: 500,
    height: 500,
  })
  editor.value = pikaso
  // pikaso.board.background.overlay.node.setAttrs(
  //   {
  //     fill: "transparent",
  //     fillLinearGradientColorStops: [0, "red", .5, "green", 1, "blue"],
  //     fillLinearGradientStartPoint: { x: 0, y: 0 },
  //     fillLinearGradientEndPoint: { x: 90, y: 50 }
  //   }
  // )
  pikaso.shapes.circle.insert({
    radius: 100,
    x: 250,
    y: 250,
    fill: 'tomato'
  })
  pikaso.board.history.undo = (() => {
    console.log('undo')
  })
})

</script>

<template>
  <div id="canvas-container" class="canvas-container">
  </div>
  <HelloWorld msg="Vite + Vue" />
</template>
<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
#canvas-container {
  border: solid 1px red;
  position: relative;
}
</style>
