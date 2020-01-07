<template lang="pug">
button#game.w-full.h-full.bg-black.flex.flex-col.overflow-hidden(
  @click='resumeGame'
  @blur='stayFocused'
  v-on:keyup.esc='togglePause'
  v-on:keyup.up='faster'
  v-on:keyup.down='slower'
  v-on:keyup.left='turnLeft'
  v-on:keyup.right='turnRight'
)
  .flex-grow
    .text-white Speed: {{ speed }}
    .text-white Location: {{ carLocation }}
    .text-white(v-if='paused') Paused
  .flex-grow.relative
    ground(:speed='speed')
    score(:score='score')
    car(
      :style='`left: ${carLocation}%; bottom: 30%`'
      :orientation='orientation'
    )
</template>

<script>
import Ground from './Ground'
import Score from './Score'
import Car from './Car'

export default {
  name: 'Game',
  components: {
    Ground,
    Score,
    Car,
  },
  computed: {
    paused() {
      return this.speed === 0
    },
  },
  data() {
    return {
      MAX_SPEED: 3,
      loopId: 0,
      speed: 0,
      score: 0,
      orientation: 0,
      carLocation: 50,
    }
  },
  mounted() {
    this.stayFocused()
    window.setInterval(this.gameLoop, 100)
  },
  methods: {
    stayFocused() {
      let gameElement = document.getElementById("game")
      if (gameElement !== document.activeElement) document.getElementById("game").focus(); 
    },
    resumeGame() {
      this.speed = 1
      this.stayFocused()
    },
    togglePause() {
      if (this.paused) this.resumeGame()
      else this.speed = 0
    },
    gameLoop() {
      if (this.paused) return
      this.updateCarLocation()
      this.loopId += 1
    },
    updateCarLocation() {
      let distance = this.orientation * this.speed
      this.carLocation = Math.max(
        Math.min(this.carLocation + distance, 88),
        8,
      )
    },
    faster() { this.speed = Math.min(this.speed+=1, this.MAX_SPEED) },
    slower() { this.speed = Math.max(this.speed-=1, 0) },
    turnRight() {
      if (this.paused) this.speed = 1
      this.orientation = Math.min(this.orientation+=1, 2)
    },
    turnLeft() {
      if (this.paused) this.speed = 1
      this.orientation = Math.max(this.orientation-=1, -2)
    },
  },
}
</script>
