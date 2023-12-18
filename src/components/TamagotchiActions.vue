<template>
  <div class="tamagotchi-actions">
    <button @click="emitActionEvent('Satiété', 10)">Manger</button>
    <button @click="emitActionEvent('Endurance', 10)">Repos</button>
    <button @click="emitActionEvent('Distraction', 10)">Jouer</button>
    <button @click="emitActionEvent('Propreté', 10)">Laver</button>
    <button @click="emitActionEvent('Intelligence', 10)">Éduquer</button>
  </div>
</template>

<script>
export default {
  name: 'TamagotchiActions',
  methods: {
    emitActionEvent(stat, amount) {
      this.$emit('editStat', { stat, amount });
    }
  }
};
</script>

<style scoped>
.tamagotchi-actions {
  text-align: center;
  margin-top: 20px;
}

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

