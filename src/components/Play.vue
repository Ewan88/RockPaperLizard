<template>
  <div id="gameContainer">
    <div v-if="gameState=='won'">
      <h2>
        {{playerHand.name[0].toUpperCase() + playerHand.name.substring(1)}}
        {{getVerb(playerHand, opponentHand)}}
        {{opponentHand.name[0].toUpperCase() + opponentHand.name.substring(1)}}
      </h2>
    </div>
    <div v-if="gameState=='draw'">
      <h2>Draw!</h2>
    </div>
    <div v-if="gameState=='lost'">
      <h2>
        {{opponentHand.name[0].toUpperCase() + opponentHand.name.substring(1)}}
        {{getVerb(opponentHand, playerHand)}}
        {{playerHand.name[0].toUpperCase() + playerHand.name.substring(1)}}
      </h2>
    </div>
    <div id="imageContainer">
      <div v-if="playerHand" id="playerImage">
        <img v-if="playerHand.name=='rock'" src="../assets/rock.png" alt='rock'>
        <img v-if="playerHand.name=='paper'" src="../assets/paper.png" alt='paper'>
        <img v-if="playerHand.name=='scissors'" src="../assets/scissors.png" alt='scissors'>
        <img v-if="playerHand.name=='lizard'" src="../assets/lizard.png" alt='lizard'>
        <img v-if="playerHand.name=='spock'" src="../assets/spock.png" alt='spock'>
      </div>
      <div v-if="opponentHand" id="opponentImage">
        <img v-if="opponentHand.name=='rock'" src="../assets/rock.png" alt='rock'>
        <img v-if="opponentHand.name=='paper'" src="../assets/paper.png" alt='paper'>
        <img v-if="opponentHand.name=='scissors'" src="../assets/scissors.png" alt='scissors'>
        <img v-if="opponentHand.name=='lizard'" src="../assets/lizard.png" alt='lizard'>
        <img v-if="opponentHand.name=='spock'" src="../assets/spock.png" alt='spock'>
      </div>
    </div>
    <h3 v-if="gameState=='won'" id="result">You win!</h3>
    <h3 v-if="gameState=='lost'" id="result">You lose!</h3>
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
        eventBus.$emit('game-won');
      } else if (this.opponentHand.counters.includes(this.playerHand.name)) {
        this.gameState = 'lost';
        eventBus.$emit('game-lost');
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

  #result {
    color: red;
  }

  #restartGameBtn:hover {
    color: red;
    cursor: pointer;
  }


</style>
