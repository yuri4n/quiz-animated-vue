<template>
  <div class="p-5 bg-gray-100 shadow-lg mb-5 text-center relative">
    <span class="text-3xl">Your score is: </span>
    <span
      class="text-3xl font-black transition-colors duration-700"
      :class="'text-' + color"
      >{{ corrects }}</span
    >
    <span class="text-3xl font-black"> / </span>
    <span class="text-3xl font-black">{{ total }}</span>
  </div>
</template>

<script>
import { dataBus } from "../main";

export default {
  name: "Score",
  created() {
    dataBus.$on("send-answer", correct => {
      if (correct) {
        this.corrects++;
      }
      this.total++;

      this.changeColor();
    });
  },
  data() {
    return {
      corrects: 0,
      total: 0,
      color: "gray-900"
    };
  },
  methods: {
    changeColor() {
      let percentage = this.corrects / this.total;

      if (percentage > 0.8) {
        this.color = "green-500";
      } else if (percentage > 0.6) {
        this.color = "yellow-500";
      } else {
        this.color = "red-600";
      }
    }
  }
};
</script>

<style scoped></style>
