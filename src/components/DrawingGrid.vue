<template>
  <canvas
    id="canvas"
    :width="gridSize"
    :height="gridSize"
    @click="onClick($event)"
  ></canvas>
</template>

<script>
export default {
  name: 'drawing-grid',
  props: {
    data: {
      type: Array,
      default: null,
    },
    mode: {
      type: String,
      default: 'Draw', // Draw, Delete
    },
    gridSize: {
      type: Number,
      default: 1000,
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
      cells: [],
    };
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

    if (this.data == null)
      this.calculateGridSizes(this.gridSize, this.cellSize);
    else this.cells = this.data;
    this.fillGrid(this.cells);
  },
  methods: {
    onClick(event) {
      const rect = this.canvas.getBoundingClientRect();
      const x = event.clientX - rect.left;
      const y = event.clientY - rect.top;
      const cell = this.getCell(x, y);
      if (this.mode === 'Draw') this.fillCell(cell, this.color);
      else this.clearCell(cell);
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
      this.ctx.strokeStyle = '#d9d9d9';
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
    getCell(x, y) {
      return this.cells.find(
        (cell) =>
          cell.x === Math.floor(x / this.cellSize) &&
          cell.y === Math.floor(y / this.cellSize)
      );
    },
    calculateGridSizes(gridSize, cellSize) {
      let xNodes, yNodes;
      if (!this.xNodes) {
        xNodes = Math.floor(gridSize / cellSize);
      }

      if (!this.yNodes) {
        yNodes = Math.floor(gridSize / cellSize);
      }

      let index = 0;
      for (let y = 0; y < yNodes; y++) {
        for (let x = 0; x < xNodes; x++) {
          this.cells[index] = {
            id: `${y}-${x}`,
            y,
            x,
            size: cellSize,
            color: null,
          };

          index++;
        }
      }
    },
    fillGrid(cells) {
      cells.forEach((p) => {
        if (p.color == null) return;
        this.fillCell(p, p.color);
      });
    },
    updateData(cell) {
      const id = `${cell.y}-${cell.x}`;
      const i = this.cells.findIndex((x) => x.id === id);
      if (i !== -1) this.cells.splice(i, 0, cell);

      this.$emit('update', {
        gridSize: this.gridSize,
        cellSize: this.cellSize,
        cells: this.cells,
      });
    },
  },
};
</script>
<style scoped></style>
