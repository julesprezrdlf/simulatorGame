<template>
  <div class="tutorialBoxContainer sm:w-80 w-screen h-screen sm:h-5/6 sm:w-1/3">
    <div class="logoTutorialContainer mt-5 grid justify-items-center">
      <h1>Defeat</h1>
    </div>
    <div class="textTutorialContainer grid justify-items-center">
      <p class="mt-10 text-center">
       You didn't get to your goal and your company collapses.
      </p>

      <p class="mt-3">You go back driving for Uber, or being alcoholic. Who knows.</p>
      <p class="mt-3">But hey! You can play again</p>
    </div>
    <div class="tutorialButtonArea grid grid-cols-6 mt-10 ">
      <button
        class="button-grow col-start-2 col-span-4 sm:col-start-3 sm:col-span-2 mt-72 sm:mt-64 mb-10"
        @click="changeLose"
      >
        Play again
      </button>
    </div>
  </div>
</template>

<script>
export default {
 methods: {
    changeTutorial() {
      this.$emit('setLoseUnActive', false)
    },
  },
}

</script>

<style>

</style>