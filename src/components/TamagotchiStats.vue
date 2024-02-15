<template>
  <div class="tamagotchi-stats">
    <div v-for="(stat, index) in statValues" :key="index" :class="getClass(stat)">
      {{ stat.name }}: {{ stat.value }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'TamagotchiStats',
  props: {
    statValues: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      animatedStats: {},
      lastValues: {}
    };
  },
  watch: {
    statValues: {
      deep: true,
      handler(newStats) {
        newStats.forEach(stat => {
          const oldValue = this.lastValues[stat.name] || stat.value;
          const isIncreasing = stat.value > oldValue;
          const isDecreasing = stat.value < oldValue;

          if (isIncreasing || isDecreasing) {
            this.triggerAnimation(stat.name, stat.value, isIncreasing);
          }

          this.lastValues[stat.name] = stat.value;
        });
      }
    }
  },
  methods: {
    triggerAnimation(statName, newValue, isIncreasing) {
      this.animatedStats[statName] = {
        value: newValue,
        animation: 'changing',
        isIncreasing: isIncreasing
      };

      setTimeout(() => {
       if (this.animatedStats[statName]) {
          this.animatedStats[statName] = {
            value: newValue,
            animation: '',
            isNeutral: true 
          };
	}
      }, 500);
    },
    getClass(stat) {
      const statAnimation = this.animatedStats[stat.name];
      return {
        'stat-changing': statAnimation?.animation === 'changing',
        'stat-increasing': statAnimation?.isIncreasing,
        'stat-decreasing': !statAnimation?.isIncreasing,
        'stat-neutral': statAnimation?.isNeutral 
      };
    }
  }
};
</script>

<style scoped>
@keyframes changeAnimation {
  0% { transform: scale(1); }
  50% { transform: scale(1.2); }
  100% { transform: scale(1); }
}

.stat-changing {
  animation: changeAnimation 0.5s ease;
}

.stat-increasing {
  color: green;
}
.stat-decreasing {
  color: red;
}
.stat-neutral {
  color: black;
}
</style>

