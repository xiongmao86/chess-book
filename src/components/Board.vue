<template>
  <div class="board">
    <!-- <Square color="black" piece="BQ" /> -->
    <Square
      v-for="(square, index) in squares"
      v-bind:color="square.color"
      v-bind:piece="square.piece"
      v-bind:key="index"
    />
  </div>
</template>

<script>
import Square from "./Square.vue";

function notationToIndex(notation) {
  if (!notation.match(/^[A-H][1-8]$/)) {
    return undefined;
  } else {
    return (
      (notation.charCodeAt(0) - "A".charCodeAt(0)) * 8 +
      (notation.charCodeAt(1) - "1".charCodeAt(0))
    );
  }
}

let squares = [...Array(8).keys()]
  .map(row =>
    [...Array(8).keys()].map(line => {
      return {
        piece: "",
        color: color(row, line)
      };
    })
  )
  .flat();

function color(row, line) {
  return (row + line) % 2 ? "black" : "white";
}

const STATE = {
  A1: "WK",
  A8: "BK",
  H1: "WQ",
  H8: "BQ"
};

export default {
  name: "Board",
  data: function() {
    return {
      squares
    };
  },
  methods: {
    setState: function(state) {
      let instance = this;
      Object.keys(state).forEach(key => {
        const i = notationToIndex(key.toString());
        if (i !== undefined) instance.squares[i].piece = state[key];
      });
    }
  },
  components: {
    Square
  },
  mounted() {
    this.setState(STATE);
  }
};
</script>

<style scoped>
.board {
  display: grid;
  grid-template-rows: repeat(8, 1fr);
  grid-template-columns: repeat(8, 1fr);
  width: 640px;
  height: 640px;
}
</style>
