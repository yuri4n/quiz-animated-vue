<template>
  <div class="container mx-auto my-5">
    <transition name="slide" appear>
      <div class="mx-w-md mx-auto shadow-lg p-5 mb-5 bg-gray-100">
        <h1 class="text-5xl font-black inline-block">The super quiz</h1>
        <transition name="slide">
          <button
            v-if="notStarted"
            @click="notStarted = !notStarted"
            class="rounded-full bg-red-700 px-3 py-1 text-white font-black float-right inline-block"
          >
            END GAME
          </button>
        </transition>
      </div>
    </transition>
    <transition name="slide">
      <app-score v-if="notStarted"></app-score>
    </transition>
    <transition name="flip" mode="out-in" appear>
      <component
        @start-game="startGame"
        :is="!notStarted ? 'app-start' : 'app-question'"
      ></component>
    </transition>
    <app-answer v-if="notStarted"></app-answer>
  </div>
</template>

<script>
import Answer from "./components/Answer";
import Question from "./components/Question";
import Start from "./components/Start";
import Score from "./components/Score";

export default {
  components: {
    appAnswer: Answer,
    appQuestion: Question,
    appStart: Start,
    appScore: Score
  },
  data() {
    return {
      notStarted: false
    };
  },
  methods: {
    startGame(value) {
      this.notStarted = value;
    }
  }
};
</script>

<style scoped>
.flip-enter-active {
  animation: flip-in 0.3s ease-out forwards;
}
.flip-leave-active {
  animation: flip-out 0.3s ease-out forwards;
}

@keyframes flip-out {
  from {
    transform: rotateY(0deg);
  }
  to {
    transform: rotateY(90deg);
  }
}

@keyframes flip-in {
  from {
    transform: rotateY(90deg);
  }
  to {
    transform: rotateY(0deg);
  }
}
</style>
