<template>



  <div 
    class="playerBoxContainer p-5 sm:w-80 w-screen h-screen sm:h-auto sm sm:w-1/3"
  >


<!-- Here goes the Win or Lose condition -->

<!-- Win -->
 <div v-if="winOn" class="winContainer grid grid-cols-1 place-items-center">

<h1>Victory!</h1>
   <br/>
   <br/>
   <br/>
   <br/>
<div class="textTutorialContainer grid justify-items-center">
      <p class="mt-10 text-center">
        You defeated the game! 
      </p>

      <p class="mt-3">May the Gods remember about your epic win!</p>
      <p class="mt-3">You can refresh the site to play again!</p>
    </div>
     <br/>
   <br/>
 </div>

<!-- Defeat -->

 <div v-if="loseOn" class="winContainer grid grid-cols-1 place-items-center">

<h1>Defeat! </h1>
   <br/>
   <br/>
   <br/>
   <br/>
<div class="textTutorialContainer grid justify-items-center">
      <p class="mt-10 text-center">
        You were defeated :(
      </p>

      <p class="mt-3">You didn't achieve your goals </p>
      <p class="mt-3">But you can refresh the site to play again!</p>
    </div>
     <br/>
   <br/>
 </div>













<!-- Game Init -->
<!-- TODO: I should make this cleaner with a single gameOn wrapper without messing with the layout -->
    <div  v-if="gameOn" class="hudContainer grid grid-cols-4 gap-4">
      <div  v-if="gameOn" class="moneyContainer">
        <p class="mb-0 text-base">$ {{ moneyDisplay }} M</p>
        <p>Valuation</p>
      </div>
      <div  v-if="gameOn" class="HappinessContainer grid justify-items-center col-span-2">
        <!-- <img
          class="smileyContainer mb-2"
          src="https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/happiness-06.a501ff39.png"
        /> -->
        <p>{{ happiness }}</p>
        <p>Happiness</p>
      </div>
      <div  v-if="gameOn" class="DateContainer">
        <p class="mb-2 text-base">{{ dateDisplay }}</p>
        <!-- <div class="progressBar"><p class="limit">111</p></div> -->
      </div>
    </div>

    <div  v-if="gameOn" class="playerActions">
      <div  class="avatar grid justify-items-center mt-5">
        <!-- Avatar from JSON -->
        <div v-for="item in currentEvent" :key="item.id">
          <img class="avatarContainer mb-2" v-bind:src="item.avatar" />
        </div>
        <!-- .................... -->
      </div>
      <div class="playerHud mx-10 p-5">
        <!-- Name from JSON -->
        <div v-for="item in currentEvent" :key="item.id">
          <h2 class="text-sm mt-14">{{ item.name }}</h2>
        </div>
        <!-- .................... -->

        <!-- Text from JSON -->
        <div v-for="item in currentEvent" :key="item.id">
          <vue-typed-js :typeSpeed="10" :strings="[item.text]">
            <h1 class="typing text-xs text-black"></h1>
          </vue-typed-js>
        </div>
        <!-- .................... -->
      </div>
    </div>
    <!-- Button text from JSON -->
    <div   v-for="item in currentEvent" :key="item.id">
      <div  v-if="gameOn" class="playerButtonArea grid grid-cols-6">
        <button
          class="button-growPlayer text-xs col-start-2 col-span-4 sm:col-start-3 sm:col-span-2"
          @click="nextItem"
        >
          {{ item.option1 }}
        </button>
        <button
          class="button-growPlayer text-xs col-start-2 col-span-4 sm:col-start-3 sm:col-span-2 mt-2 mb-5"
          @click="nextItem2"
        >
          {{ item.option2 }}
        </button>
      </div>
    </div>
    <!-- .................... -->


  </div>









</template>

<script>
import events from '../assets/events.json'
export default {
  data() {
    return {
      gameOn:true,
      winOn:false,
      loseOn:false,
      dates: [
        'January 3',
        'January 10',
        'January 15',
        'January 22',
        'January 25',
        'February 3',
        'February 10',
        'February 16',
        'February 27',
        'March 2',
        'March 9',
        'March 15',
        'March 17',
        'March 20',
        'March 29',
        'April 1',
        'April 15',
        'April 30',
        'May 2',
        'May 5',
        'May 10',
        'May 17',
        'May 19',
        'May 27',
        'May 29',
        'June 10',
        'June 12',
        'June 18',
        'June 28',
        'July 6',
        'July 7',
        'July 18',
        'July 20',
        'July 29',
        'August 1',
        'August 15',
        'August 30',
        'September 5',
        'September 12',
        'September 20',
        'September 22',
        'September 30',
        'October 2',
        'October 8',
        'October 16',
        'October 21',
        'November 1',
        'November 5',
        'November 13',
        'November 19',
        'November 21',
        'November 29',
        'November 30',
        'December 10',
        'December 20',
        'December 30',
      ],
      dateDisplay: 'January 1',
      moneyDisplay: 1,
      happiness: 50,
      arrayEvents: [],
      currentEvent: [],
      randomEvents: [],
      jsonLength: null,
      randomEvent: [],
      eventCounter: 0,
    }
  },
  computed: {},
  beforeMount() {
    this.fetchArrayEvents()
    this.fetchJsonLength()
  },
  methods: {
    fetchArrayEvents() {
      this.currentEvent.push(events[0])
      for (let index = 1; index < this.jsonLength; index++) {
        this.arrayEvents.push(events[index])
      }
    },
    fetchJsonLength() {
      this.jsonLength = Object.keys(events).length
      this.randomEvents = events
      this.randomEvents.sort(() => Math.random() - 0.5)
    },
    nextItem() {
      this.moneyDisplay = this.moneyDisplay + this.currentEvent[0].option1money
      this.happiness = this.happiness + this.currentEvent[0].option1happy

      if (
        this.happiness < 0 ||
        this.moneyDisplay < 0 ||
        (this.happiness > 0 &&
          this.moneyDisplay < 1000 &&
          this.dateDisplay === 'December 30')
      ) {
       
        // this.$emit('setSplashActive', false);
    // DEFEAT
    this.gameOn=false;
    this.loseOn=true;
      } else {
        if (
          this.happiness > 0 &&
          this.moneyDisplay > 0 &&
          this.dateDisplay !== 'December 30'
        ) {
          this.currentEvent.shift()
          this.eventCounter++
          this.currentEvent.push(this.randomEvents[this.eventCounter])
          this.dateDisplay = this.dates[this.eventCounter]
        }

        if (
          this.happiness > 0 &&
          this.moneyDisplay > 0 &&
          this.dateDisplay === 'December 30'
        ) {
          // alert('Victory! :D')
           // WIN
             this.gameOn=false;
    this.winOn=true;
//  this.$emit('setWinActive', false);
          this.currentEvent.shift()
          this.eventCounter++
          this.currentEvent.push(this.randomEvents[this.eventCounter])
          this.dateDisplay = this.dates[this.eventCounter]
        }
      }
    },

    nextItem2() {
      this.moneyDisplay = this.moneyDisplay + this.currentEvent[0].option2money
      this.happiness = this.happiness + this.currentEvent[0].option2happy

      if (
        this.happiness < 0 ||
        this.moneyDisplay < 0 ||
        (this.happiness > 0 &&
          this.moneyDisplay < 1000 &&
          this.dateDisplay === 'December 30')
      ) {
        // DEFEAT
       this.gameOn=false;
    this.loseOn=true;
        // this.$emit('setSplashActive', false);
      } else {
        if (
          this.happiness > 0 &&
          this.moneyDisplay > 0 &&
          this.dateDisplay !== 'December 30'
        ) {
          this.currentEvent.shift()
          this.eventCounter++
          this.currentEvent.push(this.randomEvents[this.eventCounter])
          this.dateDisplay = this.dates[this.eventCounter]
        }

        if (
          this.happiness > 0 &&
          this.moneyDisplay > 0 &&
          this.dateDisplay === 'December 30'
        ) {
          // alert('Victory! :D')

          // WIN
       this.gameOn=false;
    this.winOn=true;
//  this.$emit('setWinActive', false);
          this.currentEvent.shift()
          this.eventCounter++
          this.currentEvent.push(this.randomEvents[this.eventCounter])
          this.dateDisplay = this.dates[this.eventCounter]
        }
      }
    },
  },
}
</script>

<style>
.playerBoxContainer {
  background-color: #626275;
}

.button-growPlayer {
  color: black;
  background-color: white;
  border: 1px solid black;
  padding: 0 16px;
  cursor: pointer;
  min-height: 40px;

  transition: all 0.3s ease-in-out;
}

.button-growPlayer:hover {
  transform: scale(1.2);
}

.hudContainer {
  color: white;
}

.progressBar {
  background-color: #26bb26;
  width: auto;
  display: block;
}

.smileyContainer {
  height: 24px;
  width: 24px;
}

.avatarContainer {
  height: 170px;
  width: 170px;
  z-index: 5;
  transform: translateY(80px);
}

.playerHud {
  background-color: #efefef;
  border: 5px solid #968383;
}

.playerActions {
  transform: translateY(-80px);
}

.limit {
  visibility: hidden;
}

.typed-cursor {
  display: none;
}


</style>
