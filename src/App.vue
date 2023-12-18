<template>
  <div id="app">
    <my-tamagotchi :tamagotchi="tamagotchiData" @editStat="editStat" />
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
        Satiété: 100,
        Endurance: 100,
        Distraction: 100,
        Propreté: 100,
        Intelligence: 100,
      }
    };
  },
  mounted() {
    this.intervals.push(setInterval(() => {
      if (this.tamagotchiData.Satiété > 0) {
        this.tamagotchiData.Satiété -= 1;
      }
    }, 20000);

    this.intervals.push(setInterval(() => {
      if (this.tamagotchiData.Endurance > 0) {
        this.tamagotchiData.Endurance -= 1;
      }
    }, 30000));

    this.intervals.push(setInterval(() => {
      if (this.tamagotchiData.Distraction > 0) {
        this.tamagotchiData.Distraction -= 1;
      }
    }, 40000));

    this.intervals.push(setInterval(() => {
      if (this.tamagotchiData.Propreté > 0) {
        this.tamagotchiData.Propreté -= 1;
      }
    }, 50000));

    this.intervals.push(setInterval(() => {
      if (this.tamagotchiData.Intelligence > 0) {
        this.tamagotchiData.Intelligence -= 1;
      }
    }, 60000));
  },
  unmounted() {
    this.intervals.forEach(clearInterval);
  },
  methods: {
    editStat(data) {
      const { stat, amount } = data;
      if (this.tamagotchiData[stat] + amount <= 10000) {
        this.tamagotchiData[stat] += amount;
      } else {
        this.tamagotchiData[stat] = 10000;
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

