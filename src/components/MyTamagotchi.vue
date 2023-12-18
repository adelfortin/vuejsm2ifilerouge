<template>
  <div class="tamagotchi-container">
    <h1>Mon Tamagotchi</h1>
    <ul class="stats">
      <!-- Boucle sur les différentes statistiques du Tamagotchi -->
      <li v-for="(value, key) in tamagotchi" :key="key">
        {{ key.charAt(0).toUpperCase() + key.slice(1) }}: {{ value }}
        <!-- Boutons pour modifier les statistiques -->
        <button v-if="key === 'satiete'" @click="emitActionEvent('satiete', 10)">Manger</button>
        <button v-if="key === 'endurance'" @click="emitActionEvent('endurance', 10)">Repos</button>
        <button v-if="key === 'distraction'" @click="emitActionEvent('distraction', 10)">Jouer</button>
        <button v-if="key === 'proprete'" @click="emitActionEvent('proprete', 10)">Laver</button>
        <button v-if="key === 'intelligence'" @click="emitActionEvent('intelligence', 10)">Éduquer</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'MyTamagotchi',
  props: {
    // Propriété pour recevoir les données du Tamagotchi
    tamagotchi: {
      type: Object,
      required: true
    }
  },
  methods: {
    // Méthode pour émettre un événement lorsqu'une action est effectuée
    emitActionEvent(stat, amount) {
      this.$emit('edit-stat', { stat, amount });
    }
  }
};
</script>

<style scoped>
/* Styles CSS pour le composant MyTamagotchi */
.tamagotchi-container {
  text-align: center;
  margin: 20px auto;
  padding: 20px;
  border: 2px solid #f9f9f9;
  border-radius: 15px;
  background-color: #2c3e50;
  max-width: 400px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.tamagotchi-container h1 {
  color: #f9f9f9;
  margin-bottom: 20px;
  font-size: 24px;
  text-transform: uppercase;
  letter-spacing: 1.5px;
}

.stats {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.stats li {
  margin: 10px 0;
  font-size: 18px;
  color: #f9f9f9;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

button {
  padding: 5px 10px;
  margin-left: 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #45a049;
}

button:disabled {
  background-color: #ccc;
  cursor: default;
}
</style>

