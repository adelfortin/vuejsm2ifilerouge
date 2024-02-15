<template>
  <div v-if="isGameOver" class="modal-overlay">
    <div class="modal">
      <h2>Game Over!</h2>
      <p>Votre Tamagotchi est mort ! 😢</p>
      <button @click="closeModal">Close</button>
    </div>
  </div>
</template>
<script>
export default {
  name: 'TamagotchiInfos',
  props: {
    tamagotchiData: {
      type: Object,
      required: true,
      default: () => ({
        satiete: 100,
        endurance: 100,
        distraction: 100,
        proprete: 100,
        intelligence: 100,
      })
    }
  },
  computed: {
    isGameOver() {
      return Object.values(this.tamagotchiData).every(value => value === 0);
    }
  },
  methods: {
    closeModal() {
      this.$emit('closeModal');
    }
  }
};
</script>

<style scoped>
.game-over-message {
  color: red;
  font-weight: bold;
}
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
  text-align: center;
}
</style>

