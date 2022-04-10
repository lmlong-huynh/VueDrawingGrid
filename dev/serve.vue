<script>
import { defineComponent } from 'vue';
// Uncomment import and local "components" registration if library is not registered globally.
import { VueDrawingGrid, VueDrawingGridColorPicker } from '@/entry.esm';
export default defineComponent({
  name: 'ServeDev',
  components: { VueDrawingGrid, VueDrawingGridColorPicker },
  data() {
    return {
      color: 'red',
    };
  },
});
</script>
<template>
  <div class="app">
    <vue-drawing-grid
      :color="color"
      :data="{ '0-0': { y: 0, x: 0, color: 'red', size: 20 } }"
    />
    <vue-drawing-grid-color-picker @color="color = $event" />
  </div>
</template>

<style lang="scss" scoped>
.app {
  display: flex;
  justify-content: center;
}
</style>
