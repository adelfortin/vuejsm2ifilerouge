<template>
  <div id="app">
    <!-- Utilisation du composant MyTamagotchi avec passage de données et écoute d'événements -->
    <my-tamagotchi :tamagotchi="tamagotchiData" @edit-stat="editStat" />
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
      // Données représentant les différents états du Tamagotchi
      tamagotchiData: {
        satiete: 100,
        endurance: 100,
        distraction: 100,
        proprete: 100,
        intelligence: 100,
      },
      // Tableau pour stocker les identifiants des intervalles
      intervals: []
    };
  },
  mounted() {
    // Définit des intervalles pour diminuer les états du Tamagotchi
    // Chaque intervalle a un timing différent
    this.intervals.push(setInterval(() => {
      if (this.tamagotchiData.satiete> 0) {
        this.tamagotchiData.satiete-= 1;
      }
    }, 2000));

    this.intervals.push(setInterval(() => {
      if (this.tamagotchiData.endurance > 0) {
        this.tamagotchiData.endurance -= 1;
      }
    }, 3000));

    this.intervals.push(setInterval(() => {
      if (this.tamagotchiData.distraction > 0) {
        this.tamagotchiData.distraction -= 1;
      }
    }, 4000));

    this.intervals.push(setInterval(() => {
      if (this.tamagotchiData.proprete > 0) {
        this.tamagotchiData.proprete -= 1;
      }
    }, 5000));

    this.intervals.push(setInterval(() => {
      if (this.tamagotchiData.intelligence > 0) {
        this.tamagotchiData.intelligence -= 1;
      }
    }, 6000));
  },
  unmounted() {
    // Nettoie les intervalles lors de la destruction du composant
    this.intervals.forEach(clearInterval);
  },
  methods: {
    // Méthode pour modifier les états du Tamagotchi
    editStat(data) {
      const { stat, amount } = data;
      if (this.tamagotchiData[stat] + amount <= 1000) {
        this.tamagotchiData[stat] += amount;
      } else {
        this.tamagotchiData[stat] = 10000;
      }
    }
  }
};
</script>

<style>
/* Styles CSS pour l'application */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

