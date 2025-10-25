<template>
  <div class="filters">
    <button @click="$emit('updateFilter', 'all')">Todas</button>
    <button @click="$emit('updateFilter', 'active')">Pendentes</button>
    <button @click="$emit('updateFilter', 'completed')">Concluídas</button>
  </div>
</template>

<script setup>
defineEmits(['updateFilter'])
</script>