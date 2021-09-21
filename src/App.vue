<template>
  <h1>Ninja reaction Timer</h1>
  <button @click="start" :disabled="isPlaying">play</button>
  <Block
    v-if="isPlaying"
    :delay="delay"
    @end="endGame"
    @placar="previousScoresEmit"
  />
  <p v-if="showResults">Reaction time: {{ score }} ms</p>
  <br />
  <teleport to="#previousResults">
    <h2>Previous Scores</h2>
    <slot>{{ previousResults }}</slot>
  </teleport>
</template>

<script>
import Block from './components/Block.vue'

export default {
  name: 'App',
  components: { Block },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false,
      previousResults: [],
    }
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true
      this.showResults = false
    },

    previousScoresEmit(scoresPlacar) {
      this.score = scoresPlacar
      this.previousResults.push({ Previous_Score: scoresPlacar })
      console.log('Scores ' + scoresPlacar)
    },

    endGame(reactionTime) {
      this.score = reactionTime
      this.isPlaying = false
      this.showResults = true
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
</style>
