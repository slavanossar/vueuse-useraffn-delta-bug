<template>
  <div class="flex flex-col justify-center items-center space-y-4 h-screen">
    <p>
      useRafFn without fpsLimit
      {{ hasRunWithoutFpsLimit ? 'has' : "hasn't" }} run (delta:
      {{ lastDeltaWithoutFpsLimit }})
    </p>
    <p>
      useRafFn with fpsLimit
      {{ hasRunWithFpsLimit ? 'has' : "hasn't" }} run (delta:
      {{ lastDeltaWithFpsLimit }})
    </p>
  </div>
</template>

<script lang="ts" setup>
const hasRunWithoutFpsLimit = ref(false)
const lastDeltaWithoutFpsLimit = ref(0)

const hasRunWithFpsLimit = ref(false)
const lastDeltaWithFpsLimit = ref(0) // Will never change

useRafFn(({ delta }) => {
  lastDeltaWithoutFpsLimit.value = delta
  hasRunWithoutFpsLimit.value = true
})

useRafFn(
  ({ delta }) => {
    lastDeltaWithFpsLimit.value = delta
    hasRunWithFpsLimit.value = true
  },
  { fpsLimit: 60 },
)
</script>
