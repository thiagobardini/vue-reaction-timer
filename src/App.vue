<template>
  <h1>Ninja Reaction Timer</h1>
  <button @click="start" :disabled="isPlaying">play</button>
  <Block
    v-if="isPlaying"
    :delay="delay"
    @end="endGame"
    @placar="previousScoresEmit"
  />
  <Results v-if="showResults" :score="score" @end="endGame" />
  <br />
  <teleport to="#previousResults">
    <h2>Previous Scores</h2>
    <slot>{{ previousResults }}</slot>
  </teleport>
</template>

<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue'

export default {
  name: 'App',
  components: { Block, Results },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false,
      idData: '',
      previousResults: [
        {
          previous_Score: this.previous_Score,
        },
      ],
    }
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true
      this.showResults = false
    },

    endGame(reactionTime) {
      this.score = reactionTime
      this.isPlaying = false
      this.showResults = true
    },

    previousScoresEmit(scoresPlacar) {
      this.score = scoresPlacar
      this.previousResults.push({ previous_Score: scoresPlacar })
      console.log('Scores ' + scoresPlacar)
    },
  },
}
</script>

<style>
#app,
#previousResults {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}

button {
  background: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}

button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
