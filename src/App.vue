<template>
  <div class="homeWrapper">
    <div class="reactionTimer">
      <h1>Reaction Timer</h1>
      <button @click="start" :disabled="isPlaying">Play</button>
      <Block v-if="isPlaying" :delay="delay" @end="endGame" />
      <Results v-if="showResults" :reactTime="score"></Results>
    </div>
    <div class="previousScores">
      <PreviousResults/>
    </div>
  </div>
  <!-- <p v-if="">ReactionTime: {{ score }}ms</p> -->
</template>

<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue'
import PreviousResults from './components/PreviousResults.vue'

export default {
  name: 'App',
  components: {
    Block,
    Results,
    PreviousResults
  },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false,
      formerTimes: []
    }
  },
  mounted() {
    console.log('OnMounted');
    if (localStorage.getItem('prevTimes')) {
      console.log(JSON.parse(localStorage.getItem('prevTimes')));
      this.formerTimes = JSON.parse(localStorage.getItem('prevTimes'))
      console.log(this.formerTimes);
    }
    // WHERE WAS I
    // I need to figure out how to pass formerTimes to PreviousResults
    // Right know this.formerTimes is console loggin = Proxy { <target>: (5) […], <handler>: {…} } and idk why
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true
      this.showResults = false
    },
    endGame(reactionTime) {
      this.score = reactionTime
      if (localStorage.getItem('prevTimes')) {
        let tempArr = JSON.parse(localStorage.getItem('prevTimes'))
        tempArr.push(this.score)
        console.log(tempArr);
        console.log(this.formerTimes);
        this.formerTime = tempArr


        localStorage.setItem('prevTimes', JSON.stringify(tempArr))
        console.log(JSON.parse(localStorage.getItem('prevTimes')))
      } else {
        localStorage.setItem('prevTimes', JSON.stringify([this.score]))
      }
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
  color: #b28c18;
  margin-top: 60px;
}
.homeWrapper {
  display: flex;
  flex-direction: column;
}
</style>
