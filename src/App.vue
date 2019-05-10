<template>
  <div id="app">
    <playerSelect v-if="!playerHand" />
  </div>
</template>

<script>
import playerSelect from './components/PlayerSelect.vue'
import { eventBus } from './main.js';

export default {
  name: 'app',
  components: {
    "playerSelect": playerSelect
  },
  data() {
    return {
      playerHand: null,
      hands: [
        {
          name: 'rock',
          counters: ['lizard', 'scissors']
        },
        {
          name: 'paper',
          counters: ['rock', 'spock']
        },
        {
          name: 'scissors',
          counters: ['paper', 'lizard']
        },
        {
          name: 'lizard',
          counters: ['spock', 'paper']
        },
        {
          name: 'spock',
          counters: ['scissors', 'rock']
        }
      ],
    }
  },
  mounted() {
    eventBus.$on('player-select', (index) => {
      this.playerHand = this.hands[index];
    });
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
