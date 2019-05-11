<template>
  <div id="app">
    <playerSelect v-if="!playerHand" />
    <opponentSelect
      v-if="playerHand && !opponentHand"
      :playerHand="playerHand"
      :hands="hands"
    />
    <play
      v-if="playerHand && opponentHand"
      :playerHand="playerHand"
      :opponentHand="opponentHand"
    />
  </div>
</template>

<script>
import playerSelect from './components/PlayerSelect.vue'
import opponentSelect from './components/OpponentSelect.vue'
import play from './components/Play.vue'

import { eventBus } from './main.js';

export default {
  name: 'app',
  components: {
    "playerSelect": playerSelect,
    "opponentSelect": opponentSelect,
    "play": play
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
    }),
    eventBus.$on('restart-game', () => {
      this.playerHand = null;
      this.opponentHand = null;
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
    padding: 0;
    margin: 0;
  }

  #gameContainer {
    display: flex;
    flex-direction: column;
    text-align: center;
    padding: 20px;
    margin: 50px;
    width: 300px;
    height: 400px;
    border-radius: 30px;
    box-shadow: 0 0 50px;
  }

  img {
    height: 100px;
    width: auto;
  }

  #imageContainer {
    display: inline-flex;
    justify-content: space-between;
  }

</style>
