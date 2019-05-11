<template>
  <div id="gameContainer">
    <h2 v-if="!opponentHand">Choosing opponent's hand...</h2>
    <h2 v-if="opponentHand">
      Your opponent selected {{opponentHand.name[0].toUpperCase() + opponentHand.name.substring(1)}}!
    </h2>
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
  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'opponentSelect',
  props: {
    playerHand: null,
    hands: null,
  },
  data() {
    return {
      opponentHand: null
    }
  },
  methods: {
    selectOpponent() {
      let index = this.getRandomNumber(this.hands.length);

      setTimeout(function () {
        if (this.hands) {
          this.opponentHand = this.hands[index];
        }
      }, 1000);


      setTimeout(function () {
        eventBus.$emit('opponent-select', index);
      }, 2000);
    },
    getRandomNumber(number) {
      return Math.floor(Math.random() * number);
    },
  },
  mounted() {
    this.selectOpponent();
  },
}
</script>

<style scoped>

</style>
