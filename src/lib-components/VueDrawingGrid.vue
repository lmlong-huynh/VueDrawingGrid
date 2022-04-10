<template>
  <canvas
    id="canvas"
    :width="gridSize"
    :height="gridSize"
    @click="onClick($event)"
  ></canvas>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'VueDrawingGrid',
  props: {
    modelValue: {
      type: Object,
      default: null,
      // { "y-x": {y: string, x:string, size: number, color: string} }
    },
    mode: {
      type: String,
      default: 'Draw', // Draw, Delete
    },
    gridSize: {
      type: Number,
      default: 1000,
    },
    gridColor: {
      type: String,
      default: '#d9d9d9',
    },
    cellSize: {
      type: Number,
      default: 20,
    },
    color: {
      type: String,
      default: '#FF9595',
    },
  },
  data() {
    return {
      canvas: null,
      ctx: null,
      isBusy: false,
    };
  },
  computed: {
    cells: {
      get() {
        return this.modelValue;
      },
      set(newValue) {
        console.log('cells', newValue);
        this.$emit('update:modelValue', newValue);
      },
    },
    hasError: function () {
      return this.errors.length > 0;
    },
  },

  watch: {
    data: {
      deep: true,
      handler(newValue) {
        this.cells = newValue;
        this.fillGrid(this.cells);
      },
    },
  },
  mounted() {
    this.generateCanvas();
    this.generateGrid(this.gridSize, this.gridSize, this.cellSize);
    this.calculateGridSizes(this.gridSize, this.cellSize);

    if (this.modelValue != null) this.mergeData(this.modelValue);
    this.fillGrid(this.cells);
  },
  methods: {
    onClick(event) {
      if (this.isBusy) return;
      this.isBusy = true;
      const rect = this.canvas.getBoundingClientRect();
      const x = event.clientX - rect.left;
      const y = event.clientY - rect.top;
      const cell = this.getCell(x, y);
      if (this.mode === 'Draw') this.fillCell(cell, this.color);
      else this.clearCell(cell);
      this.isBusy = false;
    },
    clearCell(cell) {
      this.ctx.clearRect(
        cell.x * cell.size,
        cell.y * cell.size,
        cell.size,
        cell.size
      );
    },
    fillCell(cell, color) {
      this.clearCell(cell);
      this.ctx.fillStyle = color;
      this.ctx.fillRect(
        cell.x * cell.size,
        cell.y * cell.size,
        cell.size,
        cell.size
      );

      this.updateData({ ...cell, color: color });
    },
    generateCanvas() {
      this.canvas = document.getElementById('canvas');
      this.ctx = this.canvas.getContext('2d');
    },
    generateGrid(width, height, cellSize) {
      this.ctx.beginPath();
      for (var x = 0; x <= width; x += cellSize) {
        this.ctx.moveTo(x, 0);
        this.ctx.lineTo(x, height);
      }
      this.ctx.strokeStyle = this.gridColor;
      this.ctx.lineWidth = 1;
      this.ctx.stroke();
      this.ctx.beginPath();
      for (var y = 0; y <= height; y += cellSize) {
        this.ctx.moveTo(0, y);
        this.ctx.lineTo(width, y);
      }
      this.ctx.lineWidth = 1;
      this.ctx.stroke();
    },
    getCellId(x, y) {
      return `${Math.floor(y / this.cellSize)}-${Math.floor(
        x / this.cellSize
      )}`;
    },
    getCell(x, y) {
      return this.cells[this.getCellId(x, y)];
    },
    calculateGridSizes(gridSize, cellSize) {
      let xNodes, yNodes;
      if (!this.xNodes) {
        xNodes = Math.floor(gridSize / cellSize);
      }

      if (!this.yNodes) {
        yNodes = Math.floor(gridSize / cellSize);
      }

      for (let y = 0; y < yNodes; y++) {
        for (let x = 0; x < xNodes; x++) {
          this.cells[`${y}-${x}`] = {
            y,
            x,
            size: cellSize,
            color: null,
          };
        }
      }
    },
    fillGrid(cells) {
      Object.values(cells).forEach((p) => {
        if (p.color == null) return;
        this.fillCell(p, p.color);
      });
    },
    updateData(cell) {
      this.cells[this.getCellId(cell.x, cell.y)] = cell;

      this.$emit('update', this.cells);
      this.$emit('update:modelValue', this.cells);
    },
    mergeData(data) {
      if (data == null) return;
      this.cells = { ...this.cells, ...data };
    },
  },
});
</script>
<style scoped></style>
