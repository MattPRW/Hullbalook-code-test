<template>
  <div id="app">
    <Header 
      :numCorrect="numCorrect"
    />
    <b-container class="bv-example-row">
        <b-row>
          <b-col>
            <GameBoard 
              v-if="gameData.length"
              :gameData="gameData"
              :increment="increment"
              :resetIncrement="resetIncrement"
            />
          </b-col>
        </b-row>
      </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import GameBoard from './components/GameBoard.vue'
import gamedata from './assets/gamedata.json'

export default {
  name: 'app',
  components: {
    Header,
    GameBoard
  },
  data() {
    return {
      gameData: gamedata,
      index: 0,
      numCorrect: 0
    }
  },
  methods: {
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++
      }
    },
    resetIncrement(){
      this.numCorrect = 0
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
