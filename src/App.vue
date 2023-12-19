<template>
  <div id="app">
    <img src="@/assets/logo.png" alt="Logo" />
    <my-tamagotchi :tamagotchi="tamagotchiData" @edit-stat="handleStatEdit" />
    <tamagotchi-infos :tamagotchi-data="tamagotchiData" @closeModal="handleCloseModal" />
  </div>
</template>

<script>
import TamagotchiInfos from './components/TamagotchiInfos.vue';
import MyTamagotchi from './components/MyTamagotchi.vue';

export default {
  name: 'App',
  components: {
    MyTamagotchi,
    TamagotchiInfos,
  },
  data() {
    return {
      tamagotchiData: {
        satiete: 10,
        endurance: 10,
        distraction: 10,
        proprete: 10,
        intelligence: 10,
      },
      lastStatValues: {
        satiete: 10,
        endurance: 10,
        distraction: 10,
        proprete: 10,
        intelligence: 10,
      },
      intervals: []
    };
  },
  mounted() {
    this.intervals.push(setInterval(() => this.decreaseStat('satiete'), 2000));
    this.intervals.push(setInterval(() => this.decreaseStat('endurance'), 3000));
    this.intervals.push(setInterval(() => this.decreaseStat('distraction'), 4000));
    this.intervals.push(setInterval(() => this.decreaseStat('proprete'), 5000));
    this.intervals.push(setInterval(() => this.decreaseStat('intelligence'), 6000));
  },
  unmounted() {
    this.intervals.forEach(clearInterval);
  },
  methods: {
     handleCloseModal() {
      console.log("Modal fermé. faire un restart pour le jeu.");
      this.resetGame();
    },
    resetGame() {
      this.tamagotchiData = {
        satiete: 10,
        endurance: 10,
        distraction: 10,
        proprete: 10,
        intelligence: 10,
      };
    },
    decreaseStat(stat) {
      if (this.tamagotchiData[stat] > 0) {
        this.tamagotchiData[stat] -= 1;
      }
    },
    handleStatEdit({ stat, amount }) {
      if (this.tamagotchiData[stat] + amount <= 10000) {
        this.tamagotchiData[stat] += amount;
      } else {
        this.tamagotchiData[stat] = 10000;
      }
      this.updateLastStatValues();
    },
    updateLastStatValues() {
      this.lastStatValues = { ...this.tamagotchiData };
    }
  },
  watch: {
    tamagotchiData: {
      deep: true,
      handler() {
        this.updateLastStatValues();
      }
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

