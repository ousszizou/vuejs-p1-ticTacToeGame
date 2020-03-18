<template>
  <div id="app">
    <h1>Tic-Tac-Toe Game</h1>
    <h2 class="statistics">
      <span class="playerNames">X</span> has
      <span class="results">{{ wins["X"] }}</span> wins | Match
      <span class="results">{{ matches + 1 }}</span> |
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
  methods: {
    restart() {
      EventBus.$emit("clearCells");
      EventBus.$emit("resetGrid");
      this.matches++;
    }
  },
  created() {
    EventBus.$on("win", winner => this.wins[winner]++);
  }
};
</script>

<style>
#app {
  font-family: "Dosis", sans-serif;
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

.restart {
  width: 100%;
  margin: 0;
  background-color: #ff5722;
  border: none;
  color: white;
  padding: 20px 0;
  border-bottom-left-radius: 50px;
  border-bottom-right-radius: 50px;
  font-weight: 800;
  cursor: pointer;
  outline: none;
  font-size: 2em;
}

.statistics {
  font-weight: 400;
}
.statistics .results {
  color: #00bcd4;
  font-weight: 800;
}

.statistics .playerNames {
  text-decoration: underline;
  color: #2c3e50;
}
</style>
