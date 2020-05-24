<template>
  <div class="mx-w-md mx-auto bg-green-500 shadow-lg text-center p-5 text-white">
    <h1 class="text-xl font-black">Welcome!</h1>
    <h1 class="text-3xl font-bold">Do you want to start a new game?</h1>
    <button @click="startGame" class="rounded-full font-black px-5 py-1 bg-gray-900 mt-5">START</button>
  </div>
</template>

<script>
export default {
  methods: {
    startGame() {
      this.$emit("start-game", true);
    }
  }
};
</script>

<style>
</style>