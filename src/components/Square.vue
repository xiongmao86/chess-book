<template>
  <div class="Square" v-bind:class="color">
    <Piece :color="piece_color" :type="piece_kind" v-if="piece !== ''" />
  </div>
</template>

<script>
import Piece from "./Piece.vue";

const COLORS = "W|B".split("|");
const KINDS = "K|Q|B|N|R|P".split("|");
const PIECE_NAMES = COLORS.map(color => KINDS.map(kind => color + kind)).flat();
const FULLNAME = {
  K: "king",
  Q: "queen",
  B: "bishop",
  N: "knight",
  R: "rook",
  P: "pawn"
};

export default {
  name: "Square",
  props: {
    color: String,
    piece: {
      type: String,
      default: "",
      validator(val) {
        return val === "" || PIECE_NAMES.indexOf(val) !== -1;
      }
    }
  },
  computed: {
    piece_color() {
      const color = this.piece.split("")[0];
      return color == "W" ? "white" : "black";
    },
    piece_kind() {
      const kind = this.piece.split("")[1];
      return FULLNAME[kind];
    }
  },
  methods: {
    add_piece: function(piece) {
      this.piece = piece;
    },
    remove_piece: function() {
      this.piece = "";
    }
  },
  components: {
    Piece
  }
};
</script>

<style scoped>
.black {
  background-color: brown;
}
.white {
  background-color: burlywood;
}

.Square {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* div {
  width: 64px;
  height: 64px;
} */
</style>
