<template lang="html">
  <div class="">
    <div class="gameStatus" :class="gameStatusColor">
      {{ gameStatusMessage }}
    </div>
    <div class="grid">
      <Cell v-for="n in 9" :key="n" :marker="n" />
    </div>
  </div>
</template>

<script>
import Cell from "./Cell.vue";
import EventBus from "../eventBus.js";
export default {
  name: "Grid",
  components: {
    Cell
  },
  data() {
    return {
      activePlayer: "O",
      gameStatus: "turn",
      gameStatusMessage: "O's Turn",
      gameStatusColor: "statusTurn",
      moves: 0,
      winConditions: [
        // eslint-disable-next-line
        [1, 2, 3],[4, 5, 6],[7, 8, 9], // rows
        // eslint-disable-next-line
        [1, 4, 7],[2, 5, 8],[3, 6, 9], // columns
        // eslint-disable-next-line
        [1, 5, 9],[3, 5, 7] // diagonals
      ],
      cells: {
        // eslint-disable-next-line
        1: "", 2: "", 3: "",
        // eslint-disable-next-line
        4: "", 5: "", 6: "",
        // eslint-disable-next-line
        7: "", 8: "", 9: ""
      }
    };
  },
  computed: {
    nonActivePlayer() {
      if (this.activePlayer === "O") {
        return "X";
      }
      return "O";
    }
  },
  methods: {
    changePlayer() {
      this.activePlayer = this.nonActivePlayer;
      this.gameStatusMessage = `${this.activePlayer}'s Turn`;
    },
    checkForWin() {
      let cells = this.cells;
      return this.winConditions.some(condition => {
        let count = 0;
        condition.forEach(cell => {
          if (cells[cell] === this.activePlayer) {
            count++;
          }
        });
        if (count === 3) {
          return true;
        }
        return false;
      });
    },
    gameIsWon() {
      EventBus.$emit("win", this.activePlayer);
      this.gameStatusMessage = `${this.activePlayer} Wins`;
      EventBus.$emit("freeze");
      return "win";
    },
    changeGameStatus() {
      if (this.checkForWin()) {
        return this.gameIsWon();
      } else if (this.moves === 9) {
        return "draw";
      }
      this.changePlayer();
      return "turn";
    }
  },
  created() {
    EventBus.$on("shot", cellNumber => {
      this.cells[cellNumber] = this.activePlayer;
      this.moves++;
      this.gameStatus = this.changeGameStatus();
    });
    EventBus.$on("resetGrid", () => {
      Object.assign(this.$data, this.$options.data());
    });
  },
  watch: {
    gameStatus() {
      if (this.gameStatus === "win") {
        this.gameStatusColor = "statusWin";
        console.log(this.activePlayer);
        this.gameStatusMessage = `${this.activePlayer} Wins`;
        return;
      } else if (this.gameStatus === "draw") {
        this.gameStatusColor = "statusDraw";
        this.gameStatusMessage = `there's no winner`;
        return;
      }
    }
  }
};
</script>

<style lang="css" scoped>
.grid {
  display: grid;
  grid-template-columns: 120px 120px 120px;
  grid-gap: 10px;
  background-color: #34495e;
  color: #fff;
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
  position: relative;
}

.gameStatus {
  padding: 20px 0;
  border-top-left-radius: 50px;
  border-top-right-radius: 50px;
  font-size: 2em;
  font-weight: 800;
  color: white;
}

.statusTurn {
  background-color: #ffc107;
}

.statusWin {
  background-color: #8bc34a;
}

.statusDraw {
  background-color: #dedede;
}
</style>
