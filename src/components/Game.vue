<template>
  <div id="game">
    <h2>Choose a hand</h2>
    <div class="top">
      <img id="rock" src="../assets/rock.png" alt="rock">
    </div>
    <div class="middle">
      <img id="spock" src="../assets/spock.png" alt="spock">
      <img id="paper" src="../assets/paper.png" alt="paper">
    </div>
    <div class="bottom">
      <img id="lizard" src="../assets/lizard.png" alt="lizard">
      <img id="scissors" src="../assets/scissors.png" alt="scissors">
    </div>
  </div>
</template>

<script>
export default {
  name: 'Game',
  props: {

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  #game {
    display: flex;
    flex-direction: column;
    text-align: center;
  }

  div.top {
    margin-bottom: 20px;
    border: 1px solid white;
    display: inline-flex;
    align-self: center;
  }

  div.middle {
    margin-bottom: 20px;
    border: 1px solid white;
    padding: 0px 50px;
  }

  div.bottom {
    border: 1px solid white;
    padding: 0px 50px;

  }

  img {
    height: 100px;
    width: auto;
    padding: 0 20px;
  }

  img:hover {
    cursor: pointer;
    transition-duration: 10s;
    transform: rotate(360deg);
  }

</style>
