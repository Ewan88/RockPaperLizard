<template>
  <div id="app">
    <Game/>
  </div>
</template>

<script>
import Game from './components/Game.vue'

export default {
  name: 'app',
  components: {
    "Game": Game
  }
}
</script>

<style>

  body {
    background-color: black;
    color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding-top: 20px;
    margin: 0;
  }

</style>
