<script setup>
import HelloWorld from './components/HelloWorld.vue'
import Pikaso, { ShapeModel } from 'pikaso';
import { onMounted, ref } from 'vue';

const editor = ref()

onMounted(() => {
  const container = window.document.querySelector('#canvas-container')
  const pikaso = new Pikaso({
    container,
    width: 500,
    height: 500,
    transformer: {
      borderDash: [15, 10],
      borderStroke: '#FF0000',
      borderStrokeWidth: 2,
      anchorSize: 15,
      anchorFill: 'white',
      anchorStroke: '#FF0000',
      anchorStrokeWidth: 1,
      anchorCornerRadius: 30
    },
    selection: {
      transformer: {
        borderDash: [15, 10],
        borderStroke: '#FF0000',
        borderStrokeWidth: 2,
        anchorSize: 15,
        anchorFill: 'white',
        anchorStroke: '#FF0000',
        anchorStrokeWidth: 1,
        anchorCornerRadius: 30
      }
    }
  })
  editor.value = pikaso
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
<style>
.pikaso {
  left: 0px !important;
  transform: none !important;
}
</style>
