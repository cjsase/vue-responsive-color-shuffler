<template>
  <template v-for="tile in tiles" :key="tile.number">
    <div :style="{backgroundColor: tile.color, gridArea: `tile${tile.number}`}"
         v-on:click="shuffle()"
         v-bind:class="`tile${tile.number}`">
      <span>{{tile.number}}</span>
    </div>
  </template>
</template>

<script>
export default {
  name: 'App',
  methods: {
    shuffle() {
      this.tiles.forEach(tile => tile.color = this.generateRandomColor());
    },
    generateRandomColor() {
      return `rgb(${this.getRandomNumber()}, ${this.getRandomNumber()}, ${this.getRandomNumber()})`;
    },
    getRandomNumber() {
      return Math.floor(Math.random() * 256);
    }
  },
  data() {
    return {
      tiles: []
    }
  },
  created() {
    for(let i = 1; i <= 9; i++) {
      this.tiles.push({number: i, color: this.generateRandomColor()});
    }
  }
}
</script>

<style>
body {
  height: 100vh;
  margin: 0;
  padding: 0;
}
#app {
  display: grid;
  height: 100%;
  padding: 1em;
  box-sizing: border-box;
  gap: 1em;
  grid-template-areas:
    'tile1 tile1 tile2 tile2'
    'tile1 tile1 tile3 tile4'
    'tile5 tile7 tile7 tile8'
    'tile6 tile7 tile7 tile9'
;
}
@media only screen and (max-width: 600px) {
  #app {
    grid-template-areas:
    'tile1 tile1'
    'tile3 tile4'
    'tile2 tile2'
    'tile7 tile7'
    'tile5 tile8'
    'tile6 tile9'
  ;
  }
}
#app > div {
  display: flex;
  justify-content: center;
  align-items: center;
}
#app > div > span {
  user-select: none;
  cursor: default;
}
</style>
