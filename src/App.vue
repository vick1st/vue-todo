<template>
  <div id="app">
    <h1>Todo-List Vue.js</h1>

    <TodoForm @add="addTodo" />

    <TodoFilter @updateFilter="filter = $event" />

    <TodoList
      :todos="filteredTodos"
      @toggle="handleToggle"
      @delete="handleDelete"
    />

    <p>Você tem {{ todos.filter(t => !t.completed).length }} tarefa(s) pendente(s)</p>
  </div>
</template>

<script>
import TodoForm from './components/todo-form/TodoForm.vue'
import TodoFilter from './components/todo-filter/TodoFilter.vue'
import TodoList from './components/todo-list/TodoList.vue'

export default {
  name: 'App',
  components: { TodoForm, TodoFilter, TodoList },
  data() {
    return {
      todos: [
        { id: 1, text: 'Criar componentes reutilizáveis', completed: false },
        { id: 2, text: 'Entender reatividade', completed: false },
        { id: 3, text: 'Aprender Vue', completed: false },
        { id: 4, text: 'Criar uma tarefa',
          completed: false }
      ],
      filter: 'all', // 'all' | 'active' | 'completed'
    }
  },
  computed: {
    filteredTodos() {
      if (this.filter === 'all') return this.todos
      if (this.filter === 'active') return this.todos.filter(t => !t.completed)
      if (this.filter === 'completed') return this.todos.filter(t => t.completed)
    }
  },
  methods: {
    addTodo(text) {
      this.todos.push({ id: Date.now(), text, completed: false })
    },
    handleToggle(id) {
      const todo = this.todos.find(t => t.id === id)
      if (todo) todo.completed = !todo.completed
    },
    handleDelete(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
  }
}
</script>