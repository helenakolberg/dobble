<template>
  <div id="main-menu">
      <img class="logo" src="../assets/dobble.png" alt="dobble-logo"/>
      <button id="main-menu-start" class="btn" v-on:click="startGame">Start Game</button>
      <button id="menu-menu-computer" class="btn" v-on:click="startGameComputer">
        <div>Start Game</div>
        <div id="against-computer">Against Computer</div>
        </button>
      <button id="main-menu-scores" class="btn" v-on:click="highScores">High Scores</button>
      <button id="main-menu-tutorial" class="btn" v-on:click="tutorial">Tutorial</button>
  </div>
</template>

<script>
import { eventBus } from '@/main.js';

export default {
  methods: {

    // to App 
    startGame () {
      eventBus.$emit("start-game");
    },

    // to App
    startGameComputer () {
      eventBus.$emit("start-game-computer");
    },

    // to App
    highScores () {
      eventBus.$emit("high-scores");
    },

    // to App
    tutorial () {
      eventBus.$emit("tutorial");
    }
  }
}
</script>

<style scoped>
  #main-menu {
    background-color: rgb(141, 83, 141);
    width: 100vw;
    max-height: 720px;
    height: 100vh;
    position: relative;
  }
  #main-menu-start {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
  #menu-menu-computer {
    position: absolute;
    top: 65%;
    left: 50%;
    transform: translate(-50%, -65%);
  }
  #main-menu-scores {
    position: absolute;
    top: 79%;
    left: 50%;
    transform: translate(-50%, -79%);
  }
  #main-menu-tutorial {
    position: absolute;
    top: 92%;
    left: 50%;
    transform: translate(-50%, -92%);
  }
  #against-computer {
    font-size: small;
  }
</style>
