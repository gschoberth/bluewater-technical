<script setup lang="js">
import { onMounted } from 'vue'
import { storeToRefs } from 'pinia'
import { useGameStore } from '@/stores/game'
import RiveComponent from '@/components/RiveComponent.vue'
// import RandomizedAction from '@/components/RandomizedAction.vue'
import ButtonComponent from '@/components/ButtonComponent.vue'

const game = useGameStore()
const { showAction, showIntro, showOutcome, actionContent } = storeToRefs(game)

onMounted(() => {
  actionContent.value = 'Kick'
})
</script>

<template>
  <div class="intro-wrapper" v-if="showIntro">
    {{ useRandomized }}
    <div class="overlay"></div>
    <div class="title-wrapper">
      <div class="title-banner">
        <RiveComponent :path="'title'"> </RiveComponent>
      </div>
    </div>
  </div>

  <ButtonComponent
    class="btn-center"
    :isCentered="true"
    :callback="game.startNewGame"
    :content="'START'"
    v-if="showIntro"
  ></ButtonComponent>
  <ButtonComponent
    class="btn-center"
    :isCentered="true"
    :callback="game.resetGame"
    :content="'REPLAY'"
    v-if="showOutcome"
  ></ButtonComponent>

  <!-- <RandomizedAction v-if="showAction && useRandomizedAction"></RandomizedAction> -->
  <ButtonComponent
    class="btn-center"
    :isCentered="true"
    :callback="game.calculateGoal"
    :content="actionContent"
    v-else-if="showAction"
  ></ButtonComponent>
  <div class="action-text" v-if="showAction">GO!</div>
  <div class="visuals-wrapper">
    <RiveComponent :path="'soccer_field_v2'"></RiveComponent>
  </div>
  <!-- <RandomizedAction></RandomizedAction> -->
</template>

<style lang="scss" scoped>
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 9;
  background-color: gray;
  opacity: 0.5;
}

.title-wrapper {
  position: fixed;
  inset: 0 0 0 0;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;

  .title-banner {
    display: flex;
    justify-content: center;
    align-items: center;
    // background-color: white;
    height: 500px;
    width: 100%;

    position: relative;

    // padding: 32px 64px;
  }
}

.visuals-wrapper {
  position: fixed;
  inset: 0 0 0 0;
  width: 100%;
  height: 100%;
  z-index: 1;
}

.action-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 999;
  font-size: 96px;
  font-weight: bold;
  color: yellow;
}

// .outcome-wrapper {
//   position: fixed;
//   inset: 0 0 0 0;
//   display: flex;
//   justify-content: center;
//   align-items: center;
//   z-index: 2;

//   .outcome {
//     font-size: 128px;
//     color: white;
//     font-weight: bold;
//   }
// }
</style>
