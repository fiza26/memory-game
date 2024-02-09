<script setup>
import { defineProps } from "vue";

const props = defineProps(["hardModeInfo"]);
</script>

<template>
  <div class="modal" v-if="hardModeInfo">
    <div class="modal-content-mode">
      <h1>Hard Mode Selected</h1>
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

.modal-content-mode {
  transform: scale(0);
  animation: moveUpSelectedMode 0.5s cubic-bezier(0.165, 0.84, 0.44, 1) forwards;
  background-color: #3498db;
  color: white;
  padding: 20px;
  width: 100%;
  height: 10%;
  text-align: center;
  box-shadow: rgba(0, 0, 0, 0.16) 0px 3px 6px, rgba(0, 0, 0, 0.23) 0px 3px 6px;
}

@keyframes moveUpSelectedMode {
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
