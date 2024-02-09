<script setup>
import { defineProps } from "vue";

// const props = defineProps(["hideQuestion", "gameStarted", "currentQuestion", "question"]);
const props = defineProps({
  hideQuestion: Boolean,
  gameStarted: Boolean,
  currentQuestion: Object,
  questions: Object,
  question: Object,
});


</script>

<template>
     <div class="question" :class="{ hide: hideQuestion }" v-if="gameStarted">
      <h2>{{ currentQuestion.question }}</h2>
    </div>
</template>

<style scoped>
.question {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}
.hide {
  opacity: 0;
  transition: ease-in-out 0.5s;
}


</style>