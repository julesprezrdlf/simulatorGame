<template>
  <div class =" mainPage grid justify-items-center ">
    <img src="https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/title-screen-background.7e3f9e2c.png" class="backgroundFix"/>
   <NavBox/>
    <SplashBox v-if="splashIsActive" @setSplashUnActive="setSplashUnActive"/>
    <TutorialBox v-if="tutorialIsActive" @setTutorialUnActive="setTutorialUnActive"/>
    <PlayerBox v-if="gameIsActive" @setLoseActive="setLoseActive"/>
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
            this.splashIsActive = false;
            this.tutorialIsActive = true;       
        },
            setTutorialUnActive(value) {
            this.tutorialIsActive = false;
            this.gameIsActive = true; 
        },
        setLoseActive(value){
           this.loseIsActive = true;
            this.gameIsActive = false;   
        }

    },

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