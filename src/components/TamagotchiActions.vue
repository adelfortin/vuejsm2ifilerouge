<template>
  <div class="tamagotchi-actions">
    <button @click="emitActionEvent('satiete', 10)">Manger</button>
    <button @click="emitActionEvent('endurance', 10)">Repos</button>
    <button @click="emitActionEvent('distraction', 10)">Jouer</button>
    <button @click="emitActionEvent('proprete', 10)">Laver</button>
    <button @click="emitActionEvent('intelligence', 10)">Éduquer</button>
  </div>
</template>

<script>
export default {
  name: 'TamagotchiActions',
  methods: {
    emitActionEvent(stat, amount) {
      this.$emit('edit-stat', { stat, amount });
    }
  }
};
</script>

<style scoped>
.tamagotchi-actions button {
  padding: 8px 15px;
  margin: 0 5px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.tamagotchi-actions button:hover {
  background-color: #45a049;
}

.tamagotchi-actions button:focus {
  outline: none;
  box-shadow: 0 0 0 2px rgba(76, 175, 80, 0.5);
}
</style>

