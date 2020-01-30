<template>
  <div>
    <b-jumbotron header="Can you identify the brands of these 4 trainers?">

      <div>
        <b-button 
          variant="primary"
          @click="startGame()"
          :disabled="isDisabled"
        >
          Start
        </b-button>
      </div>
      <hr class="my-4">

      <b-container class="bv-example-row">
        <b-row>
          <b-col
          v-for="(images, index) in gameData"
          :key="index"
          :class="[(selectedTrainer - 1) === index ? 'selected' : '']"
          ><img :src=images.image></b-col>
        </b-row>
      </b-container>

      <b-list-group>


        <b-list-group-item
          class="brand-box"
          v-for="(brands, index) in shuffledBrands"
          :key="index"
          :class="[
            (selectedBrand === brands.id) && (selectedBrand === selectedTrainer) ? 'correct' : '', 
            (selectedBrand === brands.id) && (selectedBrand != selectedTrainer) ? 'incorrect' : ''
          ]"
          @click="selectBrand(brands.id)"
        >
         {{ brands.brand }}
        </b-list-group-item>
      </b-list-group> 
      
      <div>
        <b-button 
          :class="[(selectedTrainer === 4) || (!selectedBrand) ? 'hidden' : '']"
          variant="outline-primary"
          @click="nextTrainer()"
        >
          Next
        </b-button>

        <b-button 
          :class="[(selectedTrainer === 4) && (selectedBrand) ? '' : 'hidden']"
          variant="outline-primary"
          @click="resetGame()"
        >
          Restart
        </b-button>
      </div>
      
    </b-jumbotron>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  props: {
    gameData: Array,
    increment: Function,
    resetIncrement: Function
  },
  mounted: function() {
    // eslint-disable-next-line
    // console.log(this.gameData);
  },
  data() {
    return {
      gameStarted: false,
      selectedTrainer: null,
      shuffledBrands: [],
      selectedBrand: null,
    }
  },
  computed: {
      isDisabled: function(){
        return !!this.selectedTrainer
      }
  },
  methods: {
    startGame(){
      
      if (!this.selectedTrainer) {
        this.shuffleBrands()
        this.selectedTrainer = 1
      }
    },
    nextTrainer(){
      if (this.selectedTrainer < 4){
        this.selectedBrand = null
        this.shuffleBrands()
        this.selectedTrainer++
      }
    },
    shuffleBrands(){
      this.shuffledBrands = _.shuffle(this.gameData)
      // eslint-disable-next-line
      console.log(this.shuffledBrands);
    },
    selectBrand(brand){
      this.selectedBrand = brand
      let isCorrect = false
      brand === this.selectedTrainer ? isCorrect = true : isCorrect = false
      this.increment(isCorrect)
    },
    resetGame(){
      this.gameStarted = "false",
      this.selectedTrainer = null,
      this.shuffledBrands = [],
      this.selectedBrand = null,
      this.resetIncrement()
    }
  } 
}
</script>

<style scoped>
  img {
    max-width: 200px;
  }
  .brand-box:hover{
    background-color: #EEEEEE
  }
  .selected {
    border: solid 2px rgb(158, 156, 156);
  }
  .list-group-item{
    padding: 10px;
  }
  .hidden{
    display:none;
  }
  .correct {
    background-color: lightgreen;
  }
  .incorrect {
    background-color: pink;
  }
</style>