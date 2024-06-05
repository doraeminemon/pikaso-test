<script setup>
import HelloWorld from './components/HelloWorld.vue'
import Pikaso, { ShapeModel } from 'pikaso';
import { onMounted, ref } from 'vue';
import { History } from './scripts/History';

const editor = ref()

onMounted(() => {
  const container = window.document.querySelector('#canvas-container')
  const settings = {
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
  }
  const pikaso = new Pikaso(settings)
  editor.value = pikaso
  pikaso.shapes.circle.insert({
    radius: 100,
    x: 250,
    y: 250,
    fill: 'tomato',
  })
  pikaso.board.history = new History(settings, pikaso.events)
})

const genRanHex = size => [...Array(size)].map(() => Math.floor(Math.random() * 16).toString(16)).join('');

const addShape = () => {
  const hex = `#${genRanHex(6)}`
  const newShape =  editor.value.shapes.circle.insert({
    radius: 100,
    x: 250,
    y: 250,
    fill: hex
  })
  newShape.node.attrs.extra = { fill: hex }
  editor.value.board.history.create(editor.value.board.stage, [newShape.node])
}

const undo = () => editor.value.board.history.undo()
const redo = () => editor.value.board.history.redo()

</script>

<template>
  <div id="canvas-container" class="canvas-container">
  </div>
  <button @click="undo">Undo</button>
  <button @click="addShape">Add Shape</button>
  <button @click="redo">Redo</button>
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
