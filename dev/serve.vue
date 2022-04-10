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
      data: { '0-0': { y: 0, x: 0, color: 'red', size: 20 } },
    };
  },
  watch: {
    data:{
     deep:true,
     handler(newValue) {
      console.log(newValue)
    }
    }
  },
});
</script>
<template>
  <div class="app">
    <vue-drawing-grid
      :color="color"
      v-model:modelValue="data"
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
