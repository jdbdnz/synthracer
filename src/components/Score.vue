<template lang="pug">
#score.absolute.right-0.bottom-0.text-4xl.font-bold.font-mono
  .text-green-300 {{ displayScore }}
</template>

<script>
export default {
  name: 'Score',
  props: {
    score: { type: Number, default: 0 },
  },
  computed: {
    displayScore() {
      if (this.score < 10) return `00${this.score}`
      if (this.score < 100) return `0${this.score}`
      return this.score
    },
  },
}
</script>
