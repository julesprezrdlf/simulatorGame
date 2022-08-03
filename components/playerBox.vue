<template>
  <div
    class="playerBoxContainer p-5 sm:w-80 w-screen h-screen sm:h-auto sm sm:w-1/3"
  >
    <div class="hudContainer grid grid-cols-4 gap-4">
      <div class="moneyContainer">
        <p class="mb-2">$ 150M</p>
        <p>Valuation</p>
      </div>
      <div class="HappinessContainer grid justify-items-center col-span-2">
        <img
          class="smileyContainer mb-2"
          src="https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/happiness-06.a501ff39.png"
        />
        <p>Happiness</p>
      </div>
      <div class="DateContainer">
        <p class="mb-2">{{ dateDisplay }}</p>
        <!-- <div class="progressBar"><p class="limit">111</p></div> -->
      </div>
    </div>

    <div class="playerActions">
      <div class="avatar grid justify-items-center mt-5">
        <!-- Avatar from JSON -->
        <div v-for="item in currentEvent" :key="item.id">
          <img class="avatarContainer mb-2" v-bind:src="item.avatar" />
        </div>
        <!-- .................... -->
      </div>
      <div class="playerHud mx-10 p-5">
        <!-- Name from JSON -->
        <div v-for="item in currentEvent" :key="item.id">
          <h2 class="text-2xl mt-14">{{ item.name }}</h2>
        </div>
        <!-- .................... -->

        <!-- Text from JSON -->
        <div v-for="item in currentEvent" :key="item.id">
          <vue-typed-js :typeSpeed="10" :strings="[item.text]">
            <h1 class="typing text-xl text-black"></h1>
          </vue-typed-js>
        </div>
        <!-- .................... -->
      </div>
    </div>
    <!-- Button text from JSON -->
    <div v-for="item in currentEvent" :key="item.id">
      <div class="playerButtonArea grid grid-cols-6">
        <button
          class="button-growPlayer col-start-2 col-span-4 sm:col-start-3 sm:col-span-2"
          @click="nextItem"
        >
          {{ item.option1 }}
        </button>
        <button
          class="button-growPlayer col-start-2 col-span-4 sm:col-start-3 sm:col-span-2 mt-2 mb-5"
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
        eventos: [{
        "id": "01",
        "avatar": "https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/product-manager.413996be.png",
        "name": "Eric, product manager",
        "text": "People love our product, but I think it's because we're cheap. Should we raise the price?",
        "option1": "Only for new users",
        "option2": "Hit them hard!",
        "option1money": 250,
        "option1happy": 0,
        "option2money": 250,
        "option2happy": 0
    },
    {
        "id": "02",
        "avatar": "https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/cfo.37f1896d.png",
        "name": "Sheryl, CFO",
        "text": "We're about to raise series A funding. Where are those documents you promised?",
        "option1": "Blame if on Chad",
        "option2": "Put something together",
        "option1money": 250,
        "option1happy": 0,
        "option2money": 250,
        "option2happy": 0
    },
    {
        "id": "03",
        "avatar": "https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/chad-marketing.e66c8d32.png",
        "name": "Chad, marketing",
        "text": "Can I have a standing desk? I have a bad back.",
        "option1": "Come on!",
        "option2": "Sure",
        "option1money": 250,
        "option1happy": 0,
        "option2money": 250,
        "option2happy": 0
    },
    {
        "id": "04",
        "avatar": "https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/support-01.37b49faa.png",
        "name": "Bubba, support",
        "text": "One of our account managers just told a client to eat dog shit...",
        "option1": "Fire them",
        "option2": "Sit them out",
        "option1money": 250,
        "option1happy": 0,
        "option2money": 250,
        "option2happy": 0
    },
    {
        "id": "05",
        "avatar": "https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/tanya-frontend.b4f5241f.png",
        "name": "Tanya, developer",
        "text": "Your lead developer calls you a n00b in front of the whole team.",
        "option1": "Call them \"Fired!\"",
        "option2": "Laugh it off",
        "option1money": 250,
        "option1happy": 0,
        "option2money": 250,
        "option2happy": 0
    },
    {
        "id": "06",
        "avatar": "https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/support-01.37b49faa.png",
        "name": "Bubba, support",
        "text": "Twitter is enraged because you bragged about your \"all-man wreckin crew\"",
        "option1": "Whatever",
        "option2": "Hire 2 female developers",
        "option1money": 250,
        "option1happy": 0,
        "option2money": 250,
        "option2happy": 0
    },
    {
        "id": "07",
        "avatar": "https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/vc-raiden.9e9b980a.png",
        "name": "Raiden, mentor",
        "text": "You should hire way more people.",
        "option1": "Check overtime hours",
        "option2": "Hire HR manager",
        "option1money": 250,
        "option1happy": 0,
        "option2money": 250,
        "option2happy": 0
    },
    {
        "id": "08",
        "avatar": " https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/journalist.fd0c84f9.png",
        "name": "Journalist",
        "text": "One of your ex-employees went to the press saying you spend all your days googling yourself",
        "option1": "Google the article",
        "option2": "Write an article",
        "option1money": -150,
        "option1happy": 0,
        "option2money": 250,
        "option2happy": 0
    },
    {
        "id": "09",
        "avatar": "https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/assistant.4f84b31e.png",
        "name": "Kevin, assistant",
        "text": "You remember you have a pitch coming up early tomorrow morning, right?",
        "option1": "I will improvise",
        "option2": "Prepare slideshow",
        "option1money": -60,
        "option1happy": 0,
        "option2money": 250,
        "option2happy": 0
    },
    {
        "id": "10",
        "avatar": " https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/seo-manager.52c653b3.png",
        "name": "Stella, growth hacker",
        "text": "Verizon wants to feature our product in their newsletter to 50k people.",
        "option1": "Let's celebrate!",
        "option2": "Awesome",
        "option1money": 80,
        "option1happy": 0,
        "option2money": 250,
        "option2happy": 0
    },
    {
        "id": "11",
        "avatar": "https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/designer-01.51c7138e.png",
        "name": "Clive, designer",
        "text": "I want a $10 000 raise or I will quit.",
        "option1": "Give the raise",
        "option2": "Negotiate",
        "option1money": 250,
        "option1happy": 0,
        "option2money": 250,
        "option2happy": 0
    },
    {
        "id": "12",
        "avatar": "https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/victor-frontend.947aa64c.png",
        "name": "Victor, developer",
        "text": "Uhmmm, I just learned our codebase has no unit tests...",
        "option1": "Fix it",
        "option2": "YOLO",
        "option1money": 250,
        "option1happy": 0,
        "option2money": 250,
        "option2happy": 0
    },
    {
        "id": "13",
        "avatar": "https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/backend-dev-01.9ea7e42b.png",
        "name": "Lars, backend",
        "text": "Our site just got banned in China.",
        "option1": "Ok",
        "option2": "Whatever",
        "option1money": 250,
        "option1happy": 0,
        "option2money": 250,
        "option2happy": 0
    },
    {
        "id": "14",
        "avatar": "   https://public-assets.toggl.com/b/assets/@toggl/startup-simulator/images/vc-mike.4e6da46b.png",
        "name": "Mike, investor",
        "text": "You have been ignoring us for the past month and we are really pissed off.",
        "option1": "Schedule some meetings",
        "option2": "Go dark",
        "option1money": 250,
        "option1happy": 0,
        "option2money": 250,
        "option2happy": 0
    }],
      // dates longitud = 56
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
      this.randomEvents=events;
      this.eventos.sort(() => Math.random() - 0.5);
      this.randomEvents.sort(() => Math.random() - 0.5);
    },
    nextItem() {
      // this.currentEvent.shift()
      // this.eventCounter++
      // this.currentEvent.push(events[this.eventCounter])
      // this.dateDisplay = this.dates[this.eventCounter]

            this.currentEvent.shift()
      this.eventCounter++
      this.currentEvent.push(this.randomEvents[this.eventCounter])
      this.dateDisplay = this.dates[this.eventCounter]
    }
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
  height: 40px;
  min-width: 200px;

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
