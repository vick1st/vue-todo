<template>
  <div>
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @toggle="$emit('toggle', $event)"
      @delete="$emit('delete', $event)"
    />
  </div>
</template>

<script setup>
import TodoItem from '../todo-item/TodoItem.vue'
defineProps({ todos: Array })
defineEmits(['toggle', 'delete'])
</script>