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
    <h5 id="counter">
      Games won: {{winCount}}
      lost: {{lostCount}}
    </h5>
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
      winCount: 0,
      lostCount: 0,
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
    }),
    eventBus.$on('game-won', () => {
      this.winCount++;
    }),
    eventBus.$on('game-lost', () => {
      this.lostCount++;
    })
  }
}
</script>

<style>

  body {
    font-family: sans-serif;
    background-color: black;
    color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 0;
    margin: 0;
  }

  #app {
    display: flex;
    flex-direction: column;
    text-align: center;
    padding: 20px;
    margin: 50px;
    width: 330px;
    height: 460px;
    border-radius: 30px;
    box-shadow: 0 0 50px red;
  }

  #gameContainer {
    display: inherit;
    flex-direction: inherit;
    text-align: inherit;
    padding: 0;
    margin: 0;
    width: auto;
    height: 400px;
  }

  img {
    height: 100px;
    width: auto;
  }

  #imageContainer {
    display: inline-flex;
    justify-content: space-between;
  }

  #counter {
    position: relative;
  }

</style>
