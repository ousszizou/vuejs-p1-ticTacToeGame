<template>
  <div id="app">
    <h1>Tic-Tac-Toe Game</h1>
    <h2 class="statistics">
      <span class="playerNames">X</span> has
      <span class="results">{{ wins["X"] }}</span> wins | Match
      <span class="results">#{{ matches + 1 }}</span> |
      <span class="playerNames">O</span> has
      <span class="results">{{ wins["O"] }}</span> wins
    </h2>
    <Grid />
    <button class="restart" @click="restart">Restart</button>
  </div>
</template>

<script>
import Grid from "./components/Grid.vue";
import EventBus from "./eventBus.js";
export default {
  name: "App",
  components: {
    Grid
  },
  data() {
    return {
      matches: 0,
      wins: {
        O: 0,
        X: 0
      }
    };
  },
  created() {
    EventBus.$on("win", winner => this.wins[winner]++);
  },
  methods: {
    restart() {
      EventBus.$emit("clearCells");
      EventBus.$emit("resetGrid");
      this.matches++;
    }
  }
};
</script>

<style>
#app {
  font-family: "Dosis", Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0 auto;
  max-width: 400px;
}

#app h1 {
  text-transform: uppercase;
  font-weight: bold;
  font-size: 3em;
}

#app button {
  width: 100%;
  margin: 0;
  background: #ff5722;
  color: white;
  border: navajowhite;
  padding: 20px 0;
  border-bottom-left-radius: 50px;
  border-bottom-right-radius: 50px;
  font-size: 2em;
  font-weight: 800;
  cursor: pointer;
  outline: none;
}

.statistics {
  font-weight: 400;
}

.statistics .results {
  color: #00bcd4;
  font-weight: 800;
}

.statistics .playerNames {
  color: #2c3e50;
  text-decoration: underline;
}
</style>
