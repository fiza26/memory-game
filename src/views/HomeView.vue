<script setup>
import { reactive, ref, computed } from "vue";
import GameFinished from "../components/GameFinished.vue";
import HardModeModal from "../components/HardModeModal.vue";
import EasyModeModal from "../components/EasyModeModal.vue";
import ChooseDifficulty from "../components/ChooseDifficulty.vue";
import CurrentQuestion from "../components/CurrentQuestion.vue";
import InfoSection from "../components/InfoSection.vue";
// import GameWrapper from "../components/GameWrapper.vue";

const images = reactive([
  {
    name: "star",
    icon: "https://static.vecteezy.com/system/resources/previews/012/959/036/original/cute-star-emoji-free-png.png",
  },
  {
    name: "care",
    icon: "https://static.vecteezy.com/system/resources/previews/019/782/556/original/care-reaction-face-emoticon-free-png.png",
  },
  {
    name: "laugh",
    icon: "https://static.vecteezy.com/system/resources/previews/022/538/054/original/3d-smile-emoji-happy-funny-cute-character-3d-render-illustration-free-png.png",
  },
  {
    name: "love",
    icon: "https://static.vecteezy.com/system/resources/previews/018/824/830/original/heart-emoji-file-free-png.png",
  },
  {
    name: "cool",
    icon: "https://static.vecteezy.com/system/resources/previews/024/125/562/original/cute-emoji-with-line-style-free-png.png",
  },
  {
    name: "crying",
    icon: "https://static.vecteezy.com/system/resources/thumbnails/024/993/763/small/crying-emoji-sad-emoticon-face-with-tear-drop-png.png",
  },
  {
    name: "wlee",
    icon: "https://static.vecteezy.com/system/resources/previews/022/094/905/original/cartoon-emoji-with-facial-expression-free-png.png",
  },
  {
    name: "angry",
    icon: "https://static.vecteezy.com/system/resources/thumbnails/009/931/816/small/angry-face-emoji-file-png.png",
  },
  {
    name: "sad",
    icon: "https://static.vecteezy.com/system/resources/thumbnails/009/687/647/small/yellow-sad-face-emoji-file-png.png",
  },
  {
    name: "salute",
    icon: "https://static.vecteezy.com/system/resources/thumbnails/009/687/645/small_2x/yellow-salute-emoji-file-png.png",
  },
  {
    name: "thinking",
    icon: "https://i.pinimg.com/originals/2d/e5/ff/2de5ffcd2ddda77165d4103697c5e90e.png",
  },
  {
    name: "smile",
    icon: "https://static.vecteezy.com/system/resources/thumbnails/010/313/700/small/emoji-feel-good-smile-happy-file-png.png",
  },
]);

const questions = reactive([
  {
    question: "Find care emoji",
    key: "care",
    number: 1,
  },
  {
    question: "Find star emoji",
    key: "star",
    number: 2,
  },
  {
    question: "Find laugh emoji",
    key: "laugh",
    number: 3,
  },
  {
    question: "Find love emoji",
    key: "love",
    number: 4,
  },
  {
    question: "Find cool emoji",
    key: "cool",
    number: 5,
  },
  {
    question: "Find crying emoji",
    key: "crying",
    number: 6,
  },
  {
    question: "Find wlee emoji",
    key: "wlee",
    number: 7,
  },
  {
    question: "Find angry emoji",
    key: "angry",
    number: 8,
  },
  {
    question: "Find sad emoji",
    key: "sad",
    number: 9,
  },
  {
    question: "Find salute emoji",
    key: "salute",
    number: 10,
  },
  {
    question: "Find smile emoji",
    key: "smile",
    number: 11,
  },
  {
    question: "Find thinking emoji",
    key: "thinking",
    number: 12,
  },
]);

const gameStarted = ref(false);
const hideIcon = ref(false);
const hideQuestion = ref(false);

const difficultyState = ref(false);
const easyMode = ref(false);
const hardMode = ref(false);
const easyModeInfo = ref(false);
const hardModeInfo = ref(false);

const difficulty = () => {
  difficultyState.value = true;
};

const easyModeInfoShow = () => {
  easyModeInfo.value = true;
  setTimeout(() => {
    easyModeInfo.value = false;
  }, 1000);
};

const hardModeInfoShow = () => {
  hardModeInfo.value = true;
  setTimeout(() => {
    hardModeInfo.value = false;
  }, 1000);
};

const easySelected = () => {
  easyMode.value = true;
  difficultyState.value = false;
  easyModeInfoShow();
};

const hardSelected = () => {
  hardMode.value = true;
  difficultyState.value = false;
  hardModeInfoShow();
};

const start = () => {
  images.sort(() => Math.random() - 0.5);
  gameStarted.value = true;

  setTimeout(() => {
    hideIcon.value = true;
  }, 5000);
};

const currentQuestionIndex = ref(0);
const currentQuestion = computed(() => {
  return questions[currentQuestionIndex.value];
});

const answered = ref(false);
const gameFinished = computed(() => {
  return (
    currentQuestionIndex.value === questions.length 
  );
});

images.forEach((image) => {
  image.isSelected = false;
  image.isSelectedWrong = false;
});

const score = ref(0);

const select = (image) => {
  if (image.name === currentQuestion.value.key && easyMode.value === true) {
    score.value += 10;
    answered.value = true;
    image.isSelected = true;
    setTimeout(() => {
      currentQuestionIndex.value++;
      answered.value = false;
    }, 1500);
    hideIcon.value = false;
    hideQuestion.value = true;
    setTimeout(() => {
      hideIcon.value = true;
      hideQuestion.value = false;
      image.isSelected = false;
    }, 5000);
  } else if (
    image.name === currentQuestion.value.key &&
    hardMode.value === true
  ) {
    score.value += 10;
    answered.value = true;
    image.isSelected = true;
    setTimeout(() => {
      currentQuestionIndex.value++;
      answered.value = false;
      images.sort(() => Math.random() - 0.5);
    }, 1500);
    hideIcon.value = false;
    hideQuestion.value = true;
    setTimeout(() => {
      hideIcon.value = true;
      hideQuestion.value = false;
      image.isSelected = false;
    }, 7000);
  } else if (score.value === 0) {
    score.value += 0;
    image.isSelectedWrong = true;
    setTimeout(() => {
      image.isSelectedWrong = false;
    }, 1000);
  } else {
    score.value -= 10;
    image.isSelectedWrong = true;
    setTimeout(() => {
      hideIcon.value = true;
      image.isSelectedWrong = false;
    }, 1000);
  }
};

const restart = () => {
  window.location.reload();
};
</script>

<template>
  <main>
    <ChooseDifficulty
      :difficultyState="difficultyState"
      @easySelected="easySelected"
      @hardSelected="hardSelected"
    />
    <EasyModeModal :easyModeInfo="easyModeInfo" />
    <HardModeModal :hardModeInfo="hardModeInfo" />
    <GameFinished
      :gameFinished="gameFinished"
      :score="score"
      @restart="restart"
    />
    <CurrentQuestion
      :hideQuestion="hideQuestion"
      :gameStarted="gameStarted"
      :currentQuestion="currentQuestion"
      :questions="questions"
      :question="question"
    />
    <InfoSection
      :gameStarted="gameStarted"
      :gameFinished="gameFinished"
      :score="score"
      :hideIcon="hideIcon"
      :hideQuestion="hideQuestion"
    />
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
  </main>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
}
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
.info-section {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.wrapper {
  display: flex;
  justify-content: space-around;
  align-items: center;
  flex-wrap: wrap;
  max-width: 25rem;
  min-height: 25rem;
  margin: auto;
  margin-top: 20px;
  border-radius: 15px;
}
.box-one {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #ddd;
  width: 70px;
  height: 70px;
  padding: 10px;
  cursor: pointer;
  border-radius: 15px;
  transition: ease-in-out 0.2s;
  overflow: hidden;
}
.box-one:hover {
  background-color: #3498db;
}
.disabled {
  pointer-events: none;
}
.selectedCorrect {
  outline: 2px solid #2ecc71;
  transition: ease-in-out;
}
.selectedWrong {
  outline: 2px solid #e74c3c;
  transition: ease-in-out;
}
.box-one img {
  width: 50px;
  height: 50px;
}
.hide {
  opacity: 0;
  transition: ease-in-out 0.5s;
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
