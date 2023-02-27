<template>
  <home-page
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <game-page
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
  />
</template>

<script>
import HomePage from "./components/HomePage.vue";
import GamePage from "./components/GamePage.vue";
import { shuffled } from "./utils/array";
export default {
  name: "App",
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
    };
  },
  components: {
    HomePage,
    GamePage,
  },
  methods: {
    onHandleBeforeStart(config) {
      console.log(config);
      this.settings.totalOfBlocks = config.totalOfBlocks;
      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      this.settings.cardsContext = shuffled(shuffled(shuffled(cards)));
      this.settings.startedAt = new Date().getTime();

      this.statusMatch = "match";
    },
  },
};
</script>

<!-- <style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style> -->
