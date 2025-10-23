<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="wrapper">
      <h1>🚀 Vue.js Todo-List</h1>
      
      <nav>
        <RouterLink to="/">Todos</RouterLink>
        <RouterLink to="/settings">Configurações</RouterLink>
      </nav>
    </div>
  </header>

  <main>
    <RouterView />
  </main>
</template>

<style scoped>
header {
  background: var(--color-background-soft);
  border-bottom: 1px solid var(--color-border);
  padding: 1rem 0;
}

.wrapper {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h1 {
  color: var(--color-heading);
  margin: 0;
  font-size: 1.5rem;
}

nav {
  display: flex;
  gap: 1rem;
}

nav a {
  padding: 0.5rem 1rem;
  border-radius: 4px;
  text-decoration: none;
  color: var(--color-text);
  transition: background-color 0.3s;
}

nav a:hover {
  background-color: var(--color-background-mute);
}

nav a.router-link-exact-active {
  background-color: var(--color-background-mute);
  color: var(--color-heading);
}

main {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem 1rem;
}
</style>
