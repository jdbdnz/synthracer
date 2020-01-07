<template lang="pug">
#ground.w-full.h-full(
  :class='`speed-${speed}`'
)
</template>

<script>
export default {
  name: 'Ground',
  props: {
    speed: { type: Number, default: 0 },
  },
}
</script>

<style>
@keyframes moving {
  from { background-position: 0 0; }
  to   { background-position: 60px 30px; }
}

#ground {
  --speed-0: 0s;
  --speed-1: 0.3s;
  --speed-2: 0.2s;
  --speed-3: 0.1s;
  --speed-4: 0.01s;
  --speed-current: var(--speed-0);
  transform: perspective(500px) rotateX(70deg) scale(0.8,2);
  background-size: 30px 30px;
  background-image: linear-gradient(
    transparent 28px,
    green 0px
  );  
  animation: moving var(--speed-current) linear infinite;
}
#ground.speed-1 { --speed-current: var(--speed-1) }
#ground.speed-2 { --speed-current: var(--speed-2) }
#ground.speed-3 { --speed-current: var(--speed-3) }
#ground.speed-4 { --speed-current: var(--speed-4) }
</style>