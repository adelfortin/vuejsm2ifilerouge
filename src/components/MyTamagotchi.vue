<template>
  <div class="tamagotchi-container">
    <tamagotchi-stats :stat-values="formattedStats" />
    <tamagotchi-actions @edit-stat="editStat" />
  </div>
</template>

<script>
import TamagotchiStats from './TamagotchiStats.vue';
import TamagotchiActions from './TamagotchiActions.vue';

export default {
  name: 'MyTamagotchi',
  components: {
    TamagotchiStats,
    TamagotchiActions
  },
  props: {
    tamagotchi: {
      type: Object,
      required: true
    }
  },
  computed: {
    formattedStats() {
      // Transform the stats object into a format suitable for <transition-group>
      return Object.entries(this.tamagotchi).map(([key, value]) => ({
        name: key,
        value: value
      }));
    }
  },
  methods: {
    editStat(data) {
      this.$emit('edit-stat', data);
    }
  }
};
</script>

<style>
.tamagotchi-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f0f0f0;
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  text-align: center;
}

.tamagotchi-container h1 {
  color: #333;
  margin-bottom: 20px;
}

/* Styles for the slots/stat values */
.tamagotchi-container span {
  display: block;
  margin-bottom: 10px;
  font-size: 18px;
  color: #555;
}

/* Additional styles for specific elements can be added here */
</style>

