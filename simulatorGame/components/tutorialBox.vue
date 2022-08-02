<template>
  <div class="tutorialBoxContainer sm:w-80 w-screen h-screen sm:h-5/6 sm:w-1/3">
    <div class="logoTutorialContainer mt-5 grid justify-items-center">
      <h1>Tutorial</h1>
    </div>
    <div class="textTutorialContainer grid justify-items-center">
      <p class="mt-10 text-center">
        Your goal is to have a valuation of $1 billion by the end of the year
      </p>

      <p class="mt-3">Use your time wisely!</p>
      <p class="mt-3">Also, make sure to keep your employees happy :)</p>
    </div>
    <div class="tutorialButtonArea grid grid-cols-6 mt-10 ">
      <button
        class="button-grow col-start-2 col-span-4 sm:col-start-3 sm:col-span-2 mt-72 sm:mt-64 mb-10"
        @click="changeTutorial"
      >
        I'm ready!
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    changeTutorial() {
      this.$emit('setTutorialUnActive', false)
    },
  },
}
</script>

<style>


.tutorialBoxContainer {
  background-color: #626275;
}

.tutorialButtonArea {
  background-color: #626275;
}

.textTutorialContainer {
  color: white;
}

.button-grow {
  color: black;
  background-color: white;
  border: 1px solid black;
  padding: 0 16px;
  cursor: pointer;
  height: 40px;
  transition: all 0.3s ease-in-out;
}

.button-grow:hover {
  transform: scale(1.2);
}

h1 {
  color: white;
  font-size: 30px;

}
</style>
