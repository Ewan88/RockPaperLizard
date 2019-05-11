<template>
  <div id="app">
    <playerSelect v-if="!playerHand" />
    <opponentSelect
      v-if="playerHand && !opponentHand"
      :playerHand="playerHand"
      :hands="hands"
    />
  </div>
</template>

<script>
import playerSelect from './components/PlayerSelect.vue'
import opponentSelect from './components/OpponentSelect.vue'

import { eventBus } from './main.js';

export default {
  name: 'app',
  components: {
    "playerSelect": playerSelect,
    "opponentSelect": opponentSelect
  },
  data() {
    return {
      playerHand: null,
      opponentHand: null,
      hands: [
        {
          name: 'rock',
          counters: ['lizard', 'scissors'],
        },
        {
          name: 'paper',
          counters: ['rock', 'spock'],
        },
        {
          name: 'scissors',
          counters: ['paper', 'lizard'],
        },
        {
          name: 'lizard',
          counters: ['spock', 'paper'],
        },
        {
          name: 'spock',
          counters: ['scissors', 'rock'],
        }
      ],
    }
  },
  mounted() {
    eventBus.$on('player-select', (index) => {
      this.playerHand = this.hands[index];
    }),
    eventBus.$on('opponent-select', (index) => {
      this.opponentHand = this.hands[index];
    })
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
