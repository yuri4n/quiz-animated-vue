<template>
  <transition name="slide">
    <div v-if="success" class="w-full p-5 bg-gray-100 mt-5">
      <div class="bg-indigo-500 rounded-full inline-flex px-2 text-white font-bold">NICE</div>
      <span class="inline-block ml-5 font-bold">YOUR ANSWER IS CORRECT</span>
      <button
        @click="nextQuestion"
        class="bg-green-400 hover:bg-green-500 font-bold border-none text-white px-3 rounded-full float-right"
      >NEXT</button>
    </div>
    <div v-if="failed" class="w-full p-5 bg-red-600 mt-5">
      <div class="bg-gray-900 shadow-lg rounded-full inline-flex px-2 text-white font-bold">FAILED</div>
      <span class="inline-block ml-5 font-bold text-white">YOUR ANSWER IS INCORRECT</span>
      <button
        @click="nextQuestion"
        class="bg-white hover:bg-gray-200 font-bold text-red-600 border-none px-3 rounded-full float-right"
      >NEXT</button>
    </div>
  </transition>
</template>

<script>
import { dataBus } from "../main";

export default {
  name: "Answer",
  props: {
    inExcecution: {
      default: false
    }
  },
  created() {
    dataBus.$on("send-answer", value => {
      value ? (this.success = true) : (this.failed = true);
    });
  },
  data() {
    return {
      failed: false,
      success: false
    };
  },
  methods: {
    nextQuestion() {
      dataBus.$emit("next-question");
      this.failed = false;
      this.success = false;
    }
  }
};
</script>

<style>
.slide-enter-to,
.slide-leave-active {
  transform: translateY(0);
  transition-duration: 0.4s;
}
.slide-leave-to,
.slide-enter {
  transform: translateY(-100%);
  opacity: 0;
}
</style>
