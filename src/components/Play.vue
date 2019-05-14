<template>
  <div id="gameContainer">
    <div v-if="gameWon">
      <h2>
        {{playerHand.name[0].toUpperCase() + playerHand.name.substring(1)}}
        {{getVerb(playerHand, opponentHand)}}
        {{opponentHand.name[0].toUpperCase() + opponentHand.name.substring(1)}}
      </h2>
    </div>
    <div v-if="gameDraw">
      <h2>Draw!</h2>
    </div>
    <div v-if="gameLost">
      <h2>
        {{opponentHand.name[0].toUpperCase() + opponentHand.name.substring(1)}}
        {{getVerb(opponentHand, playerHand)}}
        {{playerHand.name[0].toUpperCase() + playerHand.name.substring(1)}}
      </h2>
    </div>
    <div id="imageContainer">
      <div v-if="playerHand" id="player">
        <img v-if="playerHand" :class="{'fade': gameLost}"
          :src="getImageUrl(playerHand.image)" alt='player'
        >
      </div>
      <div v-if="opponentHand" id="opponent">
        <img v-if="opponentHand" :class="{'fade': gameWon}"
          :src="getImageUrl(opponentHand.image)" alt='opponent'
        >
      </div>
    </div>
    <h3 v-if="gameWon" id="result">You win!</h3>
    <h3 v-if="gameLost" id="result">You lose!</h3>
    <h3 id="restartGameBtn" v-on:click="restartGame">Play Again?</h3>
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
      gameWon: false,
      gameLost: false,
      gameDraw: false,
    }
  },
  methods: {
    getImageUrl(image) {
      return require('../assets/' + image);
    },

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
        this.gameWon = true;
        eventBus.$emit('game-won');
      } else if (this.opponentHand.counters.includes(this.playerHand.name)) {
        this.gameLost = true;
        eventBus.$emit('game-lost');
      } else {
        this.gameDraw = true;
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

  #result {
    color: red;
  }

  #restartGameBtn:hover {
    color: red;
    cursor: pointer;
  }

  .fade {
    transition-duration: 3s;
    opacity: 0.5;
  }

</style>
