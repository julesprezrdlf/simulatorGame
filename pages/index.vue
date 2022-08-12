<template>
  <div class="mainPage grid justify-items-center">
    <img
      src="https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/title-screen-background.7e3f9e2c.png"
      class="backgroundFix"
    />
    <NavBox />
    <SplashBox v-if="splashIsActive" @setSplashUnActive="setSplashUnActive" />
    <TutorialBox
      v-if="tutorialIsActive"
      @setTutorialUnActive="setTutorialUnActive"
    />
    <PlayerBox v-if="gameIsActive" @setSplashActive="setSplashActive" @setWinActive="setWinActive" />
    <LoseBox v-if="loseIsActive" @setLoseUnActive="setLoseUnActive" />
    <WinBox v-if="winIsActice"/>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      splashIsActive: true,
      tutorialIsActive: false,
      gameIsActive: false,
      loseIsActive: false,
      winIsActice: false,
    }
  },
  methods: {
    setSplashUnActive(value) {
      this.splashIsActive = false
      this.tutorialIsActive = true
    },
    setTutorialUnActive(value) {
      this.tutorialIsActive = false
      this.gameIsActive = true
    },
    setSplashActive(value) {
      this.gameIsActive = false
      this.loseIsActive = true
    },
    setLoseUnActive(value) {
      this.loseIsActive = false
      this.splashIsActive = true
    },
    setWinActive(value){
        this.gameIsActive = false
      this.winIsActive = true
    }
  },
}
</script>

<style>
html {
  background-color: #9ac7ff;
}
h1 {
  color: white;
  font-size: 30px;
}

.backgroundFix {
  position: fixed;
  bottom: 0px;
  left: 0%;
  z-index: -1;
}

div{
 border: solid 1px red; 
}
</style>
