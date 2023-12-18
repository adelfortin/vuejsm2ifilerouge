<template>
  <div id="app">
    <img src="@/assets/logo.png" alt="Logo" />
    <my-tamagotchi :tamagotchi="tamagotchiData" @edit-stat="handleStatEdit" />
  </div>
</template>

<script>
import MyTamagotchi from './components/MyTamagotchi.vue';

export default {
  name: 'App',
  components: {
    MyTamagotchi
  },
  data() {
    return {
      tamagotchiData: {
        satiete: 100,
        endurance: 100,
        distraction: 100,
        proprete: 100,
        intelligence: 100,
      },
      lastStatValues: {
        satiete: 100,
        endurance: 100,
        distraction: 100,
        proprete: 100,
        intelligence: 100,
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

