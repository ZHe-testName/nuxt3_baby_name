<script setup lang="ts">

  const props = defineProps({
    name: [String],
  });

  const emit = defineEmits(['removeCard']);
</script>

<template>
  <div 
    class="card"
    @click="emit('removeCard', name)"
  >
    <h4>{{ name }}</h4>

    <p>x</p>
  </div>
</template>

<style scoped>
  .card {
    position: relative;
    background-color: rgb(27, 60, 138);
    width: 28%;
    color: white;
    border-radius: 1rem;
    padding: 0.1rem;
    margin-right: 0.5rem;
    margin-bottom: 1rem;
  }

  .card p {
    position: absolute;
    top: -20%;
    left: 90.5%;
    cursor: pointer;
    color: rgba(255, 255, 255, 0.17);
  }
</style>