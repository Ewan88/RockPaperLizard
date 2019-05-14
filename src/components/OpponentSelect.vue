<template>
  <div id="gameContainer">
    <h2>Choosing opponent's hand...</h2>
    <div id="imageContainer">
      <div v-if="playerHand" id="playerImage">
        <img v-if="playerHand"
          :src="getImageUrl(playerHand.image)" alt='player'
        />
      </div>
      <div id="opponentImage">
        <img :src="getImageUrl(currentImage)" alt='opponent'>
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
      images: [
        "rock.png",
        "paper.png",
        "scissors.png",
        "lizard.png",
        "spock.png"
      ],
      currentImage: "rock.png",
      imageChanges: 0,
    }
  },
  methods: {
    selectOpponent() {
      let index = this.getRandomNumber(this.hands.length);

      setTimeout(function () {
        eventBus.$emit('opponent-select', index);
      }, 2000);
    },

    getRandomNumber(number) {
      return Math.floor(Math.random() * number);
    },

    getImageUrl(image) {
      return require('../assets/' + image);
    },

    changeImage() {
      let index = this.getRandomNumber(this.images.length);
      this.currentImage = this.images[index];

      /*
      following block prevents an infinite loop
      and makes recursive calls for 2 seconds
      */

      if (this.imageChanges < 26) {
        setTimeout(() => {
          this.changeImage();
        }, 80);
      }
      this.imageChanges++;
    }
  },
  mounted() {
    this.selectOpponent();
    this.changeImage();
  },
}
</script>
