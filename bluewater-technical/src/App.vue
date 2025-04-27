<script setup>
import { onBeforeUnmount, onMounted } from 'vue'
import { useGameStore } from './stores/game'
import { useTrackerStore } from './stores/tracker'
import GameView from './views/GameView.vue'

const tracker = useTrackerStore()
const game = useGameStore()

onMounted(() => {
  tracker.updateLastInteraction()
})

onBeforeUnmount(() => {
  game.resetGame()
})
</script>

<template>
  <div @click="tracker.updateLastInteraction">
    <GameView></GameView>
  </div>
</template>

<style lang="scss">
html,
body {
  background-color: black;
  padding: 0;
  margin: 0;
  height: 100%;
  width: 100%;
}
</style>

<style scoped>
.ba-btn {
  position: absolute;
  top: 16px;
  left: 16px;
  width: 100px;
  height: 100px;
  background-color: orange;
  /* visibility: hidden; */
  outline: none;
  border: none;
}
</style>
