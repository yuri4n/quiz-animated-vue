<template>
  <div class="mx-w-md mx-auto shadow-lg">
    <div class="w-full bg-gray-900 p-5">
      <h5 class="text-xl text-white">What's {{ `${question[0]} + ${question[1]}` }}</h5>
    </div>
    <div class="w-full p-5 bg-gray-100">
      <div class="grid grid-cols-2 gap-4">
        <div
          v-for="(option, index) in options"
          :key="index"
          @click="verificateOption(option)"
          class="bg-gray-900 hover:bg-gray-800 p-5 cursor-pointer text-center text-white"
        >{{ option }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import { dataBus } from "../main";

export default {
  name: "Question",
  created() {
    dataBus.$on("next-question", () => {
      this.nextQuestion();
    });

    this.generateQuestion();
    this.generateOptions();
  },
  data() {
    return {
      question: [],
      options: [0, 0, 0, 0]
    };
  },
  methods: {
    generateQuestion() {
      let firstNumber = Math.floor(Math.random() * 100);
      let secondNumber = Math.floor(Math.random() * 100);

      this.question[0] = firstNumber;
      this.question[1] = secondNumber;
    },
    generateOptions() {
      let index = Math.floor(Math.random() * 4);
      this.options[index] = this.question[0] + this.question[1];

      for (let i = 0; i < 4; i++) {
        if (this.options[i] === 0) {
          if (i % 2 === 0) {
            this.options[i] =
              this.question[0] +
              this.question[1] +
              (Math.floor(Math.random() * 20) + 1);
          } else {
            this.options[i] =
              this.question[0] +
              this.question[1] -
              (Math.floor(Math.random() * 20) + 1);
          }
        }
      }
    },
    verificateOption(option) {
      dataBus.$emit(
        "send-answer",
        option === this.question[0] + this.question[1]
      );
    },
    nextQuestion() {
      this.options = [0, 0, 0, 0];
      this.generateQuestion();
      this.generateOptions();
    }
  }
};
</script>

<style>
</style>