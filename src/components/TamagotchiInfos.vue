<template>
  <div v-if="isGameOver" class="game-over-message">
    <p>Game Over! All stats are at zero.</p>
  </div>
</template>

<script>
export default {
  name: 'TamagotchiInfos',
  props: {
    stats: {
      type: Array,
      required: true,
      default: () => [] 
    }
  },
  computed: {
    isGameOver() {
      return this.stats.length > 0 && this.stats.every(stat => stat.value === 0);
    }
  }
};
</script>

<style scoped>
.game-over-message {
  color: red;
  font-weight: bold;
}
</style>

