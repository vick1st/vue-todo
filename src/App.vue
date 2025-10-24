<template>
  <div id="app">
    <h1>Todo-List Vue.js</h1>
    <TodoItem
      :todo="{ id: 1, text: 'Aprender Vue.js', completed: false }"
      @toggle="handleToggle"
      @delete="handleDelete"
    />
  </div>
</template>

<script>
import TodoItem from './components/todo-item/TodoItem.vue'

export default {
  name: 'App',
  components: {
    TodoItem,
  },
  methods: {
    handleToggle(id) {
      console.log('Toggle todo:', id)
    },
    handleDelete(id) {
      console.log('Delete todo:', id)
    },
  },
}
</script>
