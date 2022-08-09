<template>
  <div class="tutorialBoxContainer sm:w-80 w-screen h-screen sm:h-5/6 sm:w-1/3">
    <div class="logoTutorialContainer mt-5 grid justify-items-center">
      <h1>Victory</h1>
    </div>
    <div class="textTutorialContainer grid justify-items-center">
      <p class="mt-10 px-5 text-center">
       You beat the game! Awesome!
      </p>

      <p class="mt-3">You can play again if you'd like</p>
    </div>
    <div class="tutorialButtonArea grid grid-cols-6 mt-10 ">
      <button
        class="button-grow col-start-2 col-span-4 sm:col-start-3 sm:col-span-2 mt-72 sm:mt-64 mb-10"
        @click="changeGame"
      >
        Play again
      </button>
    </div>
  </div>
</template>

<script>
export default {
 methods: {
    changeGame() {
      this.$emit('setWinUnActive', false)
    },
  },
}

</script>

<style>

</style>