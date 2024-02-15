<script setup>
import { defineProps } from "vue";

const props = defineProps([
  "gameStarted",
  "gameFinished",
  "score",
  "hideIcon",
  "hideQuestion",
]);
</script>
<template>
  <!-- <div class="info-section">
    <p v-if="gameStarted && !gameFinished">Score : {{ score }}</p>
    <p v-if="gameStarted && !hideIcon && !hideQuestion">
      You have 5 seconds to remember
    </p>
    <h1 v-if="gameFinished">Game Over</h1>
  </div> -->
</template>
<style></style>
