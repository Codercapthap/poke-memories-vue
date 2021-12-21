<template>
  <main-screen v-if="statusMatch === 'default'" @onStart="onHandleBeforeStart($event)"></main-screen>
  <play-screen 
    v-else-if="statusMatch === 'playing'"
    :cardsContext = "settings.cardsContext"
    @onFinish = "onGetResult"
  ></play-screen>
  <result-screen
    v-else-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="statusMatch = 'default'"
  ></result-screen>
</template>

<script>
import MainScreen from "./components/MainScreen"
import PlayScreen from "./components/PlayScreen"
import ResultScreen from "./components/ResultScreen.vue"

import { shuffled } from "./utils/array"

export default {
  name: "App",
  data() {
    return {
      statusMatch: "default",
      timer: 0,
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
    }
  },
  components: {
    MainScreen,
    PlayScreen,
    ResultScreen,
  },
  methods: {
    onHandleBeforeStart(config){
      this.settings.totalOfBlocks = config.totalOfBlocks
      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
        )
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards]
      this.settings.cardsContext = shuffled(cards)
      this.settings.startedAt = new Date().getTime()


      this.statusMatch = 'playing'
    },
    onGetResult(){
      this.timer = new Date().getTime() - this.settings.startedAt;

      this.statusMatch = "result"
    }
  }
};
</script>