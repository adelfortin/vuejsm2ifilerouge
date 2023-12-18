<template>
  <div class="tamagotchi-container">
    <h1>My Tamagotchi</h1>
    <ul class="stats">
      <li v-for="(value, key) in tamagotchi" :key="key">
        {{ key.charAt(0).toUpperCase() + key.slice(1) }}: {{ value }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'MyTamagotchi', // Multi-word component name
  props: {
    tamagotchi: {
      type: Object,
      required: true
    }
  }
};
</script>

<style scoped>
.tamagotchi-container {
  text-align: center;
  margin: 20px;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #f9f9f9;
}

.tamagotchi-container h1 {
  color: #333;
  margin-bottom: 15px;
}

.stats {
  list-style-type: none;
  padding: 0;
}

.stats li {
  margin: 5px 0;
  font-size: 16px;
  color: #555;
}
</style>

