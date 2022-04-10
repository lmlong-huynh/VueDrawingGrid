<template>
  <div class="app">
    <drawing-grid :color="color"/>
    <drawing-grid-color-picker @color="color = $event"/>
  </div>
</template>

<script>
import DrawingGrid from './components/DrawingGrid';
import DrawingGridColorPicker from './components/DrawingGridColorPicker';
export default {
  name: 'App',
  components: { DrawingGrid, DrawingGridColorPicker },data() {
    return {
      color: 'black'
    }
  },
};
</script>

<style lang="scss">
</style>
