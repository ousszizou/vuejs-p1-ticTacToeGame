<template lang="html">
  <div class="cell" @click="shot">
    {{ mark }}
  </div>
</template>

<script>
import EventBus from "../eventBus.js";
export default {
  props: ["marker"],
  name: "Cell",
  data() {
    return {
      canPlaceMark: false,
      mark: ""
    };
  },
  created() {
    EventBus.$on("freeze", () => (this.canPlaceMark = true));
    EventBus.$on("clearCells", () => {
      this.mark = "";
      this.canPlaceMark = false;
    });
  },
  methods: {
    shot() {
      if (!this.canPlaceMark) {
        this.mark = this.$parent.activePlayer;
        this.canPlaceMark = true;
        EventBus.$emit("shot", this.marker);
      }
    }
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
