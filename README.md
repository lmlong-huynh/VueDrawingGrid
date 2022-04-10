# VueDrawingGrid
A simple vue 3 drawing grid using HTML5 canvas



## Demo
<p align="center">
  <img src="https://media.giphy.com/media/YOUNaY0g2Iy6bPbWJz/giphy.gif" alt="animated" />
</p>
## Installation

Install my-project with npm

```bash
npm i vue-drawing-grid
```
    
## Usage


```
import{ VueDrawingGrid } from 'vue-drawing-grid';
```

 If you want to pass a preloaded grid you can use the `data` prop. The model of the `data` prop is
 ```
 { "y-x": {y: string, x:string, size: number, color: string} }
 ```

There is also a `VueDrawingGridColorPicker` component that can be imported, but is not neccessary.
```
import{ VueDrawingGrid,VueDrawingGridColorPicker } from 'vue-drawing-grid';
export default {
  name: 'App',
  components: { VueDrawingGrid, VueDrawingGridColorPicker }
}

<template>
  <div class="app">
    <vue-drawing-grid />
    <vue-drawing-grid-color-picker @color="color = $event" />
  </div>
</template>
```


 There are also a few other props that can be used in `VueDrawingGrid`
```
    data: {
      type: Array,
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
    cellSize: {
      type: Number,
      default: 20,
    },
    color: {
      type: String,
      default: '#FF9595',
    },
```