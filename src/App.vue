<template>
  <div class="w-screen h-screen">
    <Game />
  </div>
</template>

<script>
import Game from './components/Game.vue'

export default {
  name: 'app',
  components: {
    Game,
  }
}
</script>

<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>
