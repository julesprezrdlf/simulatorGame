<template>
  <div class =" mainPage grid justify-items-center ">
    <img src="https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/title-screen-background.7e3f9e2c.png" class="backgroundFix"/>
   <NavBox/>
    <SplashBox v-if="splashIsActive" @setSplashUnActive="setSplashUnActive"/>
    <TutorialBox v-if="tutorialIsActive" @setTutorialUnActive="setTutorialUnActive"/>
    <PlayerBox v-if="gameIsActive" @setSplashActive="setSplashActive"/>
    <!-- <LoseBox v-if="loseIsActive" @setLoseUnActive="setLoseUnActive"/> -->
  </div>
</template>

<script>


export default {
    name: "IndexPage",
    data() {
        return {
            splashIsActive: true,
            tutorialIsActive: false,
            gameIsActive: false,
            loseIsActive: false,
            midWinIsActive: false,
            winIsActice: false,
        };
    },
    methods: {
        setSplashUnActive(value) {
            this.splashIsActive = !this.splashIsActive;
            this.tutorialIsActive = !this.tutorialIsActive;       
        },
            setTutorialUnActive(value) {
            this.tutorialIsActive = !this.tutorialIsActive;
            this.gameIsActive = !this.gameIsActive; 
        },
        setSplashActive(value){
           this.gameIsActive = false;
            this.splashIsActive = true;   
        },
        // setLoseUnActive(value){
        //    this.loseIsActive = !this.loseIsActive;
        //     this.splashIsActive = !this.splashIsActive;   
        // },

    },

    // head: {  link: [    { rel: 'stylesheet', href="https://fonts.googleapis.com/css2?family=VT323&display=swap" }  ]},

}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=VT323&display=swap');
*{
    font-family: 'VT323', monospace;
/* border:1px solid red !important; */
}

html{
  background-color:#9AC7FF;
}
h1{
  color: white;
  font-size: 30px;
}

.backgroundFix{
    position:fixed;
    bottom:0px;
    left:0%;
    z-index:-1;
}
</style>