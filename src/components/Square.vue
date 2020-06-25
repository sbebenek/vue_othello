<template>
  <div class="square" v-on:click="setPiece($event)">
    <div v-if="gamePiece === 'white'">
      <div class="whitePiece"></div>
    </div>
    <div v-else-if="gamePiece === 'black'">
      <div class="blackPiece"></div>
    </div>
  </div>
</template>

<script>
module.exports = {
  props: ["piece", "row", "column"], //can be white, black, or null
  //watch for prop changes
  watch: {
    piece: function(newVal, oldVal) {
      console.log(
        "Piece changed inside the square: " + newVal + " | was: " + oldVal
      );
      if (newVal !== oldVal) {
        this.gamePiece = newVal;
      }
    }
  },

  data: function() {
    return {
      gamePiece: this.piece,
      squareRow: this.row,
      squareColumn: this.column
    };
  },
  methods: {
    setPiece: function(event) {
      this.$parent.setPiece(
        event,
        this.$props.piece,
        this.$props.row,
        this.$props.column
      );
    }
  }
};
</script>

<style scoped>
.square {
  width: 4vw;
  height: 4vw;
  background: green;
  border: 1px solid black;
  display: flex;
  align-items: center;
  justify-content: center;
}
.square:hover {
  background: lightgreen;
}

.whitePiece {
  width: 3vw;
  height: 3vw;
  border-radius: 50%;
  background: white;
}
.blackPiece {
  width: 3vw;
  height: 3vw;
  border-radius: 50%;
  background: black;
}
</style>