<template>
  <div id="container">
    <h1>Ninja Reaction Timer</h1>
    <button @click="start" :disabled="isPlaying">play</button>
    <Block
      v-if="isPlaying"
      :delay="delay"
      @end="endGame"
      @scoreDB="previousScores"
    />
    <Results v-if="showResults" :score="score" @end="endGame" />
    <br />
    <teleport to="#previousResults" v-if="showPreviousScores">
      <h2>Previous Reactions Times in Milliseconds</h2>
      <div v-for="item in scores" :key="item" class="pill">
        <span>{{ item }} ms</span>
      </div>
    </teleport>
  </div>
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
      scores: [],
      showPreviousScores: false,
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

    previousScores(scoreSaved) {
      this.scores.push(scoreSaved)
      console.log('Scores ' + scoreSaved)
      this.showPreviousScores = true
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
  color: #fff;
  margin-top: 20px;
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
#container {
  max-width: 420px;
  margin: 10px auto;
  background: #2c3e50;
  padding: 40px;
  border-radius: 10px;
}
.pill {
  display: inline-block;
  margin: 10px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
}

#previousResults {
  font-size: 0.8em;
  max-width: 420px;
  margin: 10px auto;
  color: #2c3e50;
  /* background: #2c3e50; */
  padding: 40px;
  border-radius: 10px;
}
</style>
