<template>
  <div class="splashBoxContainer sm:w-80 w-screen h-screen sm:h-96 sm:w-1/3">
    <div class="logoContainer mt-10 grid justify-items-center">
        <img src="https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/start-screen-logo.4e78ede5.png" alt="logo" width="200" height="200">
     
    </div>




    <div class="buttonArea grid grid-cols-6  ">
        <button class="button-grow col-start-2 col-span-4 sm:col-start-3 sm:col-span-2 mt-72  sm:mt-60" @click="changeSplash" >Start Game</button>
        
    </div>
  </div>
</template>

<script>
export default {
methods:{
   changeSplash(){
    this.$emit('setSplashUnActive', false);

    },
  },
}
</script>

<style>

.splashBoxContainer{
  /* border: solid 1px red; */
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

.logoContainer{
    transform: translateY(100px);
}

</style>