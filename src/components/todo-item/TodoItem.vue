<template>
  <div class="todo-item">
    <input type="checkbox" :checked="todo.completed" @change="$emit('toggle', todo.id)" />
    <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
    <button @click="$emit('delete', todo.id)">Excluir</button>
  </div>
</template>

<script setup>
defineProps({
  todo: {
    type: Object,
    required: true,
  },
})
defineEmits(['toggle', 'delete'])
</script>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 0.5rem 0;
}

.todo-item .completed {
  text-decoration: line-through;
  color: #888;
}
button {
  background: none;
  border: none;
  color: #ff5555;
  cursor: pointer;
  font-size: 1rem;
  padding: 0.2rem 0.6rem;
  border-radius: 3px;
  transition: background 0.2s;
}
button:hover {
  background: #ffe5e5;
}
</style>
