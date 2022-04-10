<template>
  <div class="drawing-grid-color-picker">
    <button v-for="c in colors" :key="c.name" @click="$emit('color', c.value)">
      <div class="dot" :style="`background:${c.value}`"></div>
    </button>
  </div>
</template>

<script>
export default {
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
};
</script>

<style lang="scss" scoped>
.drawing-grid-color-picker {
  button {
    width: 38px;
    height: 38px;
    border-radius: 100px;
    padding: 0;
    min-width: 0;

    .dot {
      height: 22px;
      width: 22px;
      border-radius: 50%;
      display: inline-block;
    }
  }
}
</style>
