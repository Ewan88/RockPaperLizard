<template>
  <div id="gameContainer">
    <div id="won" v-if="gameState=='won'">
      <h2>
        {{playerHand.name[0].toUpperCase() + playerHand.name.substring(1)}}
        {{getVerb(playerHand, opponentHand)}}
        {{opponentHand.name[0].toUpperCase() + opponentHand.name.substring(1)}}
      </h2>
      <h3>You win!</h3>
    </div>
    <div id="draw" v-if="gameState=='draw'">
      <h2>Draw!</h2>
    </div>
    <div id="lost" v-if="gameState=='lost'">
      <h2>
        {{opponentHand.name[0].toUpperCase() + opponentHand.name.substring(1)}}
        {{getVerb(opponentHand, playerHand)}}
        {{playerHand.name[0].toUpperCase() + playerHand.name.substring(1)}}
      </h2>
      <h3>You lose!</h3>
    </div>
    <button id="restartGameBtn" v-on:click="restartGame">Play Again?</button>
  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'play',
  props: {
    playerHand: null,
    opponentHand: null,
  },
  data() {
    return {
      gameState: null,
    }
  },
  methods: {
    getVerb(left, right) {
      let concatenatedHands = `${left.name} ${right.name}`;
      let verb = '';
      switch (concatenatedHands) {
        case 'scissors paper':
          verb = 'cuts';
          break;
        case 'paper rock':
          verb = 'covers';
          break;
        case 'rock lizard':
        case 'rock scissors':
          verb = 'crushes';
          break;
        case 'lizard spock':
          verb = 'poisons';
          break;
        case 'spock scissors':
          verb = 'smashes';
          break;
        case 'scissors lizard':
          verb = 'decapitates';
          break;
        case 'lizard paper':
          verb = 'eats';
          break;
        case 'paper spock':
          verb = 'disproves';
          break;
        case 'spock rock':
          verb = 'vaporises';
          break;
      }
      return verb;
    },
    setGameState() {
      if (this.playerHand.counters.includes(this.opponentHand.name)) {
        this.gameState = 'won';
      } else if (this.opponentHand.counters.includes(this.playerHand.name)) {
        this.gameState = 'lost';
      } else {
        this.gameState = 'draw';
      }
    },
    restartGame() {
      eventBus.$emit('restart-game');
    }
  },
  mounted() {
    this.setGameState();
  }
}
</script>

<style scoped>

</style>
