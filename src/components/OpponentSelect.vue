<template>
  <div id="opponentSelect">
    <h2>Choosing an opposing hand...</h2>
    <div id="imageContainer">
      <img v-if="playerHand.name=='rock'" src="../assets/rock.png" alt='rock'>
      <img v-if="playerHand.name=='paper'" src="../assets/paper.png" alt='paper'>
      <img v-if="playerHand.name=='scissors'" src="../assets/scissors.png" alt='scissors'>
      <img v-if="playerHand.name=='lizard'" src="../assets/lizard.png" alt='lizard'>
      <img v-if="playerHand.name=='spock'" src="../assets/spock.png" alt='spock'>

      <img v-if="opponentHand" :src="opponentHand.image" alt='opponent'>
    </div>
  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'opponentSelect',
  props: {
    playerHand: null,
    opponentHand: null,
    hands: null,
  },
  methods: {
    selectOpponent() {

    },
    selectHand(index) {
      eventBus.$emit('opponent-select', index);
    },
  },
  mounted() {
    this.selectOpponent();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#opponentSelect {
  display: flex;
  flex-direction: column;
  text-align: center;
}

img {
  height: 100px;
  width: auto;
}

</style>
