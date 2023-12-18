<template>
  <div id="app">
    <my-tamagotchi :tamagotchi="tamagotchiData" />
  </div>
</template>

<script>
import MyTamagotchi from './components/MyTamagotchi.vue'; // Ensure this path matches the actual file location

export default {
  name: 'App',
  components: {
    MyTamagotchi // Registering the MyTamagotchi component
  },
  data() {
    return {
      tamagotchiData: { // Renamed for clarity
        satiety: 100,
        stamina: 100,
        fun: 100
        // You can add more properties here as needed
      }
    };
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

