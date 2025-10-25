<template>
  <form @submit.prevent="onSubmit">
    <input v-model="text" type="text" placeholder="Digite uma nova tarefa" />
    <button type="submit">Adicionar</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'
const text = ref('')
const emit = defineEmits(['add'])

function onSubmit() {
  if (!text.value.trim()) return
  emit('add', text.value)
  text.value = ''
}
</script>