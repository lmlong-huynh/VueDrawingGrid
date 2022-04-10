# VueDrawingGrid
A simple drawing grid using HTML5 canvas for <a href="https://vuejs.org/" target="_blank">Vue.js</a>

## Demo
<p align="center">
  <img src="https://media.giphy.com/media/YOUNaY0g2Iy6bPbWJz/giphy.gif" alt="animated" />
</p>

## Requirements
<a href="https://vuejs.org/" target="_blank">Vue.js</a> >= 3.0.0

## Installation

Install my-project with npm

```bash
npm i vue-drawing-grid
```
    
## Usage


```js
import{ VueDrawingGrid } from 'vue-drawing-grid';
```

 If you want to pass a preloaded grid you can use the `data` prop. The model of the `data` prop is
 ```js
 { "y-x": {y: string, x:string, size: number, color: string} }
 ```

There is also a `VueDrawingGridColorPicker` component that can be imported, but is not neccessary.
```js
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
```js
    data: {
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
    cellSize: {
      type: Number,
      default: 20,
    },
    color: {
      type: String,
      default: '#FF9595',
    },
```

`VueDrawingGrid` emit `update` event that contains the updated grid model
```js
 <vue-drawing-grid @update="$event" />
```

```js
 {
    gridSize: number,
    cellSize: number,
    cells: object, // { "y-x": {y: string, x:string, size: number, color: string} }
  }
```