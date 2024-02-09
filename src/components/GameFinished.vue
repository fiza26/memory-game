<script setup>
import { defineProps, defineEmits } from "vue";

const props = defineProps(["gameFinished", "score"]);

const emit = defineEmits(["restart"]);

</script>

<template>
  <div class="modal" v-if="gameFinished">
    <div class="modal-content">
      <h1>Your score : {{ score }}</h1>
      <p v-if="score > 60">Your memory is amazing</p>
      <p v-else>You need to work on your memory</p>
      <div class="diff-btn">
        <button @click="$emit('restart')" v-if="gameFinished">Restart</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.5s ease;
}
.modal-content {
  transform: scale(0);
  animation: moveUp 0.5s cubic-bezier(0.165, 0.84, 0.44, 1) forwards;
  background-color: #3498db;
  color: white;
  padding: 20px;
  border-radius: 15px;
  width: 70%;
  height: 100%;
  margin-top: 50%;
  margin-right: 7px;
  margin-left: 7px;
  text-align: center;
  box-shadow: rgba(0, 0, 0, 0.16) 0px 3px 6px, rgba(0, 0, 0, 0.23) 0px 3px 6px;
}
button {
  width: 10rem;
  height: 2rem;
  border: none;
  border-radius: 15px;
  cursor: pointer;
  background-color: #3498db;
  color: white;
}
button:hover {
  background-color: #51a8e2;
}
.modal-content .diff-btn button {
  outline: 1px solid white;
  margin: 5px;
  transition: ease-in-out 0.3s;
}
.modal-content .diff-btn button:hover {
  background-color: beige;
  color: black;
}

@keyframes moveUp {
  0% {
    transform: scale(0);
    opacity: 0;
  }

  50% {
    border-radius: 15px;
  }

  90% {
    border-radius: 15px;
  }

  100% {
    transform: scale(1);
    opacity: 1;
  }
}
</style>
