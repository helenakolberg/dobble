<template>
  <div class="symbol-div" v-if="card">
    <!-- need click.native to make it use the built-in click event rather than something from a component -->
    <card-symbol
                 v-for="(oneSymbol, index) of card.symbols" 
                 v-on:click.native="handleClick(oneSymbol)" 
                 :cardSymbol="oneSymbol" 
                 :key="index"
                 v-bind:class= "(selectedSymbol === oneSymbol) ? 'selected symbol' : (computerSymbol === oneSymbol) ? 'computer symbol' : 'symbol' "/>
  </div>
</template>

<script>
    import { eventBus } from "@/main.js";
    import CardSymbol from './Symbol.vue'

    export default {
      name: 'card',

      data () {
        return {
          selectedSymbol: null,
          computerSymbol: null
        }
      },

      props: ['card'],

      components: {
        'card-symbol': CardSymbol
      },

      mounted() {
        // from GameBoard (required to make symbols deselect after a guess)
        eventBus.$on('guess-over', () => this.selectedSymbol = null);

        // cleans selected symbol when game ends
        eventBus.$on("game-over", () => this.selectedSymbol = null);

        // cleans selected symbol when game ends
        eventBus.$on("main-menu", () => this.selectedSymbol = null);

        // from ComputerOpponent
        eventBus.$on("computer-wins", (matchingSymbol) => this.computerSymbol = matchingSymbol);

        eventBus.$on("new-round", () => this.computerSymbol = null);
      },

      methods: {
        handleClick(clickedSymbol) {
          // if no symbol has been selected, sets selectedSymbol to the clicked symbol,
          // then sends that symbol on event bus to GameBoard as "symbol-selected"
          if (this.selectedSymbol === null) {
            this.selectedSymbol = clickedSymbol;
            eventBus.$emit('symbol-selected', this.selectedSymbol);
          // if a symbol has already been selected, sets selectedSymbol to the clicked symbol,
          // then sends that symbol on event bus to GameBoard as "symbol-changed"
          } else {
            this.selectedSymbol = clickedSymbol;
            eventBus.$emit('symbol-changed', this.selectedSymbol);
          }
        }
      }

}
</script>


<style scoped>
  .symbol-div {
    display: grid;
    grid-template-columns: auto auto;
    justify-items: center;
    align-items: center;
    padding: 20px;
    overflow: hidden;
  }
  .selected {
    border: 2px red solid;
  }
  .computer {
    border: 2px #1601d1 solid;
  }
</style>
