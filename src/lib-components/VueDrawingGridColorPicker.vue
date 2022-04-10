<template>
  <div class="vue-drawing-grid-color-picker">
    <button
      style="
        width: 38px;
        height: 38px;
        border-radius: 100px;
        padding: 0;
        min-width: 0;
      "
      v-for="c in colors"
      :key="c.name"
      @click="$emit('color', c.value)"
    >
      <div
        style="
          height: 22px;
          width: 22px;
          border-radius: 50%;
          display: inline-block;
        "
        :style="`background:${c.value}`"
      ></div>
    </button>
  </div>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'VueDrawingGridColorPicker',
  props: {
    colors: {
      type: Array,
      default: () => [
        {
          name: 'Black',
          value: '#000000',
        },
        {
          name: 'Red',
          value: '#C62828',
        },
        {
          name: 'Pink',
          value: '#AD1457',
        },
        {
          name: 'Purple',
          value: '#6A1B9A',
        },
        {
          name: 'Blue',
          value: '#1565C0',
        },
        {
          name: 'Cyan',
          value: '#00838F',
        },
        {
          name: 'Green',
          value: '#2E7D32',
        },
        {
          name: 'Yellow',
          value: '#F9A825',
        },
        {
          name: 'Orange',
          value: '#EF6C00',
        },
        {
          name: 'Brown',
          value: '#4E342E',
        },
        {
          name: 'Gray',
          value: '#424242',
        },
      ],
    },
  },
});
</script>

<style scoped>
</style>
