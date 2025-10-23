<script setup>
// TodoView - Página principal do Todo-List
import { ref } from 'vue'

const todos = ref([
  { id: 1, text: 'Aprender Vue.js', completed: false },
  { id: 2, text: 'Criar Todo-List', completed: false },
  { id: 3, text: 'Dominar reatividade', completed: true }
])

const newTodo = ref('')

const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push({
      id: Date.now(),
      text: newTodo.value.trim(),
      completed: false
    })
    newTodo.value = ''
  }
}

const toggleTodo = (id) => {
  const todo = todos.value.find(t => t.id === id)
  if (todo) {
    todo.completed = !todo.completed
  }
}

const deleteTodo = (id) => {
  todos.value = todos.value.filter(t => t.id !== id)
}
</script>

<template>
  <div class="todo-view">
    <h2>📝 Minha Lista de Todos</h2>
    
    <!-- Formulário para adicionar todos -->
    <form @submit.prevent="addTodo" class="todo-form">
      <input 
        v-model="newTodo"
        type="text" 
        placeholder="Adicionar novo todo..."
        class="todo-input"
        required
      >
      <button type="submit" class="add-btn">Adicionar</button>
    </form>
    
    <!-- Lista de todos -->
    <div class="todo-list">
      <div 
        v-for="todo in todos" 
        :key="todo.id"
        class="todo-item"
        :class="{ completed: todo.completed }"
      >
        <input 
          type="checkbox" 
          :checked="todo.completed"
          @change="toggleTodo(todo.id)"
          class="todo-checkbox"
        >
        <span class="todo-text">{{ todo.text }}</span>
        <button @click="deleteTodo(todo.id)" class="delete-btn">×</button>
      </div>
    </div>
    
    <!-- Estatísticas -->
    <div class="todo-stats">
      <p>Total: {{ todos.length }} | 
         Completos: {{ todos.filter(t => t.completed).length }} | 
         Pendentes: {{ todos.filter(t => !t.completed).length }}</p>
    </div>
  </div>
</template>

<style scoped>
.todo-view {
  max-width: 600px;
  margin: 0 auto;
}

h2 {
  color: var(--color-heading);
  margin-bottom: 2rem;
  text-align: center;
}

.todo-form {
  display: flex;
  gap: 1rem;
  margin-bottom: 2rem;
}

.todo-input {
  flex: 1;
  padding: 0.75rem;
  border: 1px solid var(--color-border);
  border-radius: 4px;
  font-size: 1rem;
}

.add-btn {
  padding: 0.75rem 1.5rem;
  background: var(--color-button);
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
}

.add-btn:hover {
  background: var(--color-button-hover);
}

.todo-list {
  margin-bottom: 2rem;
}

.todo-item {
  display: flex;
  align-items: center;
  padding: 1rem;
  border: 1px solid var(--color-border);
  border-radius: 4px;
  margin-bottom: 0.5rem;
  background: var(--color-background);
  transition: all 0.3s;
}

.todo-item:hover {
  background: var(--color-background-soft);
}

.todo-item.completed {
  opacity: 0.6;
}

.todo-item.completed .todo-text {
  text-decoration: line-through;
}

.todo-checkbox {
  margin-right: 1rem;
  transform: scale(1.2);
}

.todo-text {
  flex: 1;
  font-size: 1rem;
}

.delete-btn {
  background: #ff4757;
  color: white;
  border: none;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  cursor: pointer;
  font-size: 1.2rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

.delete-btn:hover {
  background: #ff3742;
}

.todo-stats {
  text-align: center;
  color: var(--color-text-soft);
  font-size: 0.9rem;
}
</style>
