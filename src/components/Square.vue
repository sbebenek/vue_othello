<template>
  <div class="square" v-on:click="setPiece($event)">
    <div v-if="this.isAnimated === true">
      <div v-if="gamePiece === 'white'">
        <div class="whitePiece animated" :style="cssVars"></div>
      </div>
      <div v-else-if="gamePiece === 'black'">
        <div class="blackPiece animated" :style="cssVars"></div>
      </div>
    </div>
    <div v-else>
      <div v-if="gamePiece === 'white'">
        <div class="whitePiece"></div>
      </div>
      <div v-else-if="gamePiece === 'black'">
        <div class="blackPiece"></div>
      </div>
    </div>
  </div>
</template>

<script>
module.exports = {
  props: ["piece", "row", "column", "isAnimated", "animationDelay", "sound"], //can be white, black, or null
  //animation delay will delay the time the animation is set to play, allowing each piece to be flipped incrementally
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
      squareColumn: this.column,
      //isAnimated: this.isAnimated,
      //animationDelay: this.animationDelay //will be a whole number ie 1,2,3,4, etc.
    };
  },
  methods: {
    setPiece: function(event) {
      console.log("animation delay " + this.animationDelay)

      this.$parent.setPiece(
        event,
        this.$props.piece,
        this.$props.row,
        this.$props.column
      );
    }
  },


  

  computed: {
    cssVars() {
      return {
        'animation-delay': this.animationDelay * 0.05 + 's' //convert the whole number to a small, incremental ms value
      }
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
  border: 1px solid whitesmoke;
}
.blackPiece {
  width: 3vw;
  height: 3vw;
  border-radius: 50%;
  background: black;
  border: 1px solid rgb(100, 100, 100);
}

.animated {
  opacity: 0.0;
  animation: dropPiece 0.1s ease-out 1 forwards;
}

@keyframes dropPiece {
  from {
    opacity: 0;
    transform: translateY(-100px);
  }
  to {
    opacity: 1;
    transform: translateY(0px);
  }
}
</style>