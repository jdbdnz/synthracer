<template lang="pug">
#car.absolute.w-10.h-20.bg-pink-600(
  class='left-1/2'
  :class='`orientation-${orientation}`'
)
</template>

<script>
export default {
  name: 'Car',
  props: {
    orientation: { type: Number, required: true },
  },
}
</script>

<style>
#car {
  --orientation--2: -40deg;
  --orientation--1: -20deg;
  --orientation-0: 0deg;
  --orientation-1: 20deg;
  --orientation-2: 40deg;
  --orientation-current: 0deg;
  transform: perspective(60px) rotateX(40deg) rotateY(var(--orientation-current)) scale(1,1)
}
#car.orientation--2 { --orientation-current: var(--orientation--2) }
#car.orientation--1 { --orientation-current: var(--orientation--1) }
#car.orientation-0 { --orientation-current: var(--orientation-0) }
#car.orientation-1 { --orientation-current: var(--orientation-1) }
#car.orientation-2 { --orientation-current: var(--orientation-2) }
</style>
