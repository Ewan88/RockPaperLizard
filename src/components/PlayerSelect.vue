<template>
  <div id="gameContainer">
    <h2>Choose a hand</h2>
    <div class="top">
      <img id="rock" :class="{'clicked': clicked.rock}"
      src="../assets/rock.png" alt="rock"
      v-on:click="selectHand(0, 'rock')">
    </div>
    <div class="middle">
      <img id="spock" :class="{'clicked': clicked.spock}"
      src="../assets/spock.png" alt="spock"
      v-on:click="selectHand(4, 'spock')">
      <img id="paper" :class="{'clicked': clicked.paper}"
      src="../assets/paper.png" alt="paper"
      v-on:click="selectHand(1, 'paper')">
    </div>
    <div class="bottom">
      <img id="lizard" :class="{'clicked': clicked.lizard}"
      src="../assets/lizard.png" alt="lizard"
      v-on:click="selectHand(3, 'lizard')">
      <img id="scissors" :class="{'clicked': clicked.scissors}"
      src="../assets/scissors.png" alt="scissors"
      v-on:click="selectHand(2, 'scissors')">
    </div>
  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: 'playerSelect',
  props: {

  },
  data () {
    return {
      clicked: {
        rock: false,
        paper: false,
        scissors: false,
        lizard: false,
        spock: false,
      }
    }
  },
  methods: {
    selectHand(index, key) {
      this.clicked[key] = !this.clicked[key];
      setTimeout(function () {
        eventBus.$emit('player-select', index);
      }, 1000);
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

div.top {
  display: inline-flex;
  align-self: center;
}

div.middle {
  display: inline-flex;
  margin-bottom: 30px;
  justify-content: space-between;
}

div.bottom {
  display: inline-flex;
  justify-content: space-around;
}

img:hover {
  cursor: pointer;
  transition-duration: 0.5s;
  transform: scale(1.1, 1.1);
}

.clicked {
  transition-duration: 0.8s;
}

#rock.clicked {
  transform: translate(-114px, 0);
}

#paper.clicked {
  transform: translate(-200px, -100px);
}

#scissors.clicked {
  transform: translate(-192px, -230px);
}

#lizard.clicked {
  transform: translate(-30px, -230px);
}

#spock.clicked {
  transform: translate(0, -100px);
}

</style>
