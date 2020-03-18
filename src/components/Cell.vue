<template lang="html">
  <div class="cell" @click="shot">
    {{ mark }}
  </div>
</template>

<script>
import EventBus from "../eventBus.js";
export default {
  name: "Cell",
  props: ["marker"],
  data() {
    return {
      mark: "",
      canPlaceMark: true
    };
  },
  methods: {
    shot() {
      if (this.canPlaceMark) {
        this.mark = this.$parent.activePlayer;
        this.canPlaceMark = false;
        EventBus.$emit("shot", this.marker);
      }
    }
  },
  created() {
    EventBus.$on("freeze", () => {
      this.canPlaceMark = false;
    });
    EventBus.$on("clearCells", () => {
      this.mark = "";
      this.canPlaceMark = true;
    });
  }
};
</script>

<style lang="css" scoped>
.cell {
  height: 120px;
  line-height: 120px;
  font-size: 3.5em;
  background-color: #2c3e50;
  font-family: "Permanent Marker", cursive;
}
.cell:hover {
  background-color: #405971;
  cursor: pointer;
}
</style>
