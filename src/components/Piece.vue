<template>
  <!-- <div class="Piece"> -->
    <img :src="src" />
  <!-- </div> -->
</template>

<script>
export default {
  name: "Piece",
  props: {
    color: String,
    type: String
  },
  data: function() {
    return {
      src: require("../assets/" + this.color + "-" + this.type + ".svg")
    };
  }
};
</script>

<style scoped>
.Piece {
  height: 70px;
  width: 70px;
  background-color: white;
  border: solid 2px white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

img {
  height: 60px;
  width: 60px;
}
</style>
