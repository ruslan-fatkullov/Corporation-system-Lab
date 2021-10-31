<template>
  <div id="main">
    <Graph/>
    <Dialog/>
  </div>
</template>

<script>

import Graph from './components/Graph.vue'
import Dialog from './components/Dialog.vue'

export default {
  name: 'main',
  components: {
    Graph,
    Dialog
  },
}
</script>

<style>

</style>
