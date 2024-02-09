<script setup>
import { defineProps, defineEmits } from "vue";

const props = defineProps(["gameFinished", "hideIcon", "image.isSelected", "image.isSelected.isSelectedWrong", ]);

const emit = defineEmits(["restart"]);

</script>

<template>
  <div class="wrapper" v-if="!gameFinished">
      <div
        class="box-one"
        :class="{
          disabled: hideIcon === false,
          selectedCorrect: image.isSelected,
          selectedWrong: image.isSelectedWrong,
        }"
        v-for="(image, index) in images"
        :key="index"
        @click="select(image)"
      >
        <img :src="image.icon" :class="{ hide: hideIcon }" />
      </div>
      <button @click="start" v-if="!gameStarted && (easyMode || hardMode)">
        Start
      </button>
      <button @click="difficulty" v-if="!gameStarted">Difficulty</button>
    </div>
</template>

<style>

</style>
