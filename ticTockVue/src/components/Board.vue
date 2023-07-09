<template>
  <div class="winner_div"> <h1> {{ winner }}</h1>
  </div>
  <div class="board_container" :class="{X : player , O: !player}">
    <div class="board_cell top left" @click="game_system" data-id="1">
      <h1 data-id="1">{{ cell1 }}</h1>
    </div>
    <div class="board_cell top middle" @click="game_system" data-id="2">
      <h1>{{ cell2 }}</h1>
    </div>
    <div class="board_cell top right" @click="game_system" data-id="3">
      <h1>{{ cell3 }}</h1>
    </div>
    <div class="board_cell middle left" @click="game_system" data-id="4">
      <h1>{{ cell4 }}</h1>
    </div>
    <div class="board_cell middle" @click="game_system" data-id="5">
      <h1>{{ cell5 }}</h1>
    </div>
    <div class="board_cell middle right" @click="game_system" data-id="6">
      <h1>{{ cell6 }}</h1>
    </div>
    <div class="board_cell bottom left" @click="game_system" data-id="7">
      <h1>{{ cell7 }}</h1>
    </div>
    <div class="board_cell bottom middle" @click="game_system" data-id="8">
      <h1>{{ cell8 }}</h1>
    </div>
    <div class="board_cell bottom right" @click="game_system" data-id="9">
      <h1>{{ cell9 }}</h1>
    </div>
  </div>
</template>

<script>
export default {
  name: "Board",
  props: {
    // msg: {
    //   type: String,
    //   required: true,
    // },
  },

  data() {
    return {
      cell1:'',
      cell2:'',
      cell3:'',
      cell4:'',
      cell5:'',
      cell6:'',
      cell7:'',
      cell8:'',
      cell9:'',
      cells:['','','','','','','','','',],
      player: false,
      current_player: "X",
      winner: null
    };
  },

  methods: {
  
    winning_examples_function(){
      const winning_examples_arr = [

        // horizantol win
        [this.cell1, this.cell2, this.cell3],
        [this.cell4, this.cell5, this.cell6],
        [this.cell7, this.cell8, this.cell9],

        // vertical win
        [this.cell1, this.cell4, this.cell7],
        [this.cell2, this.cell5, this.cell8],
        [this.cell3, this.cell6, this.cell9],

        //diaginol win
        [this.cell1, this.cell5, this.cell9],
        [this.cell3, this.cell5, this.cell7]
      ]
      return winning_examples_arr
    },

    turn_validator(current_player){
      const winning_examples = this.winning_examples_function() 
      return winning_examples.some( example =>{
        console.log(example);
        if(example.every(cell => cell === current_player)){
          this.winner = `${current_player} won!!`;
          return true
        } else {
          return false
        }
      })
    },

    fill_cell(data_id){
      const current_cell = `cell${data_id}`;
      this[current_cell] = this.current_player;
    },

    switch_player(){
      this.player = !this.player;
      this.current_player = this.player ? "O": "X";
    },

    game_system(event) { 
      if(this.winner) return; // checks if there is already a winner.
      const data_id = event.target.dataset.id;  
      this.fill_cell(data_id)
      this.turn_validator(this.current_player);
      this.switch_player();
      //this.$set(this.cells, data_id-1, current_turn);
    },
  },
};
</script>

<style scoped>
: root{
  --border-board:8px solid #41b883;
}

template{
  display: flex;
}
.winner_div{
  opacity: 90%;
  text-align: center;
  position: fixed;
  top: 10px;
  background: #41b883;
  color: white;
  font-size: 8rem;
  font-weight: bold;
  height: 100px;
  width: 80%;
  transition: font-size 3s ease-in-out;
}

.X{
  color: red;
}

.O{
  color: greenyellow;
}

h1 {
  font-weight: 500;
  font-size: 5.6rem;
}

h3 {
  font-size: 1.2rem;
}

.board_container {
  display: grid;
  grid-template-columns: repeat(3, 200px);
  grid-template-rows: repeat(3, 200px);
}
.board_cell {
  display: flex;
  justify-content: center;
  align-items: center;
}
.top {
  border-bottom: 8px solid #41b883;
}

.left {
  border-right: 8px solid #41b883;
}

.right {
  border-left: 8px solid #41b883;
}

.bottom {
  border-top: 8px solid #41b883;
}



@media (min-width: 1024px) {
  
}
</style>
