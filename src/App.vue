<template>
  <h1>Reaction timer</h1>
  <button @click="start" :disabled="isPlaying">Play</button>
  <!-- Accessing the emmited data from block component -->
  <Block :delay="delay" v-if="isPlaying" @end="endGame" />
  <!-- <p v-if="showResults">Reaction Time{{ score }} ms</p> -->
  <Results v-if="showResults" :result="score" />
</template>

<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue'
export default {
  name: 'App',
  components: { Block, Results },
  data(){
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false
    }  
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true
      console.log(this.delay)
      this.showResults = false
    },
    endGame(reactionTime) {
      this.score = reactionTime
      this.isPlaying = false
      this.showResults = true
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
button {
  background: lightseagreen;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;

}
button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
