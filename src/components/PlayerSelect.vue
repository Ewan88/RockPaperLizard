<template>
  <div id="playerSelect">
    <h2>Choose a hand</h2>
    <div class="top">
      <img id="rock" src="../assets/rock.png" alt="rock"
      v-on:click="selectPlayerHand(0)">
    </div>
    <div class="middle">
      <img id="spock" src="../assets/spock.png" alt="spock"
      v-on:click="selectPlayerHand(1)">
      <img id="paper" src="../assets/paper.png" alt="paper"
      v-on:click="selectPlayerHand(2)">
    </div>
    <div class="bottom">
      <img id="lizard" src="../assets/lizard.png" alt="lizard"
      v-on:click="selectPlayerHand(3)">
      <img id="scissors" src="../assets/scissors.png" alt="scissors"
      v-on:click="selectPlayerHand(4)">
    </div>
  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'playerSelect',
  props: {

  },
  methods: {
    selectPlayerHand(index) {
      eventBus.$emit('player-select', index);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#playerSelect {
  display: flex;
  flex-direction: column;
  text-align: center;
}

div.top {
  display: inline-flex;
  margin-bottom: 10px;
  display: inline-flex;
  align-self: center;
}

div.middle {
  display: inline-flex;
  margin-bottom: 30px;
  width: 120%;
  align-self: center;
  justify-content: space-between;
}

div.bottom {
  display: inline-flex;
}

img {
  height: 100px;
  width: auto;
  padding: 0 20px;
}

img:hover {
  cursor: pointer;
  transition-duration: 0.5s;
  transform: scale(1.1, 1.1);
}

</style>
