<script setup>
// SettingsView - Página de configurações
import { ref, onMounted } from 'vue'

const theme = ref('light')
const sortOrder = ref('newest')

const saveSettings = () => {
  localStorage.setItem(
    'todoSettings',
    JSON.stringify({
      theme: theme.value,
      sortOrder: sortOrder.value,
    }),
  )
  alert('Configurações salvas!')
}

const resetSettings = () => {
  theme.value = 'light'
  sortOrder.value = 'newest'
}

onMounted(() => {
  const saved = localStorage.getItem('todoSettings')
  if (saved) {
    const settings = JSON.parse(saved)
    theme.value = settings.theme
    sortOrder.value = settings.sortOrder
  }
})
</script>

<template>
  <div class="settings">
    <h2>⚙️ Configurações</h2>

    <div class="setting-group">
      <h3>🎨 Tema</h3>
      <div class="radio-group">
        <label>
          <input type="radio" v-model="theme" value="light" />
          <span>☀️ Claro</span>
        </label>
        <label>
          <input type="radio" v-model="theme" value="dark" />
          <span>🌙 Escuro</span>
        </label>
      </div>
    </div>

    <div class="setting-group">
      <h3>📋 Ordem dos Todos</h3>
      <select v-model="sortOrder" class="select-input">
        <option value="newest">Mais recentes primeiro</option>
        <option value="oldest">Mais antigos primeiro</option>
        <option value="alphabetical">Alfabética</option>
      </select>
    </div>

    <div class="actions">
      <button @click="saveSettings" class="save-btn">💾 Salvar</button>
      <button @click="resetSettings" class="reset-btn">🔄 Resetar</button>
    </div>
  </div>
</template>

<style scoped>
.settings {
  max-width: 500px;
  margin: 0 auto;
}

h2 {
  color: var(--color-heading);
  margin-bottom: 2rem;
  text-align: center;
}

.setting-group {
  margin-bottom: 2rem;
  padding: 1.5rem;
  border: 1px solid var(--color-border);
  border-radius: 8px;
  background: var(--color-background-soft);
}

.setting-group h3 {
  margin: 0 0 1rem 0;
  color: var(--color-heading);
}

.radio-group {
  display: flex;
  gap: 1rem;
}

.radio-group label {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
  padding: 0.5rem;
  border-radius: 4px;
  transition: background-color 0.3s;
}

.radio-group label:hover {
  background: var(--color-background-mute);
}

.radio-group input[type='radio'] {
  margin: 0;
}

.select-input {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid var(--color-border);
  border-radius: 4px;
  background: var(--color-background);
  color: var(--color-text);
  font-size: 1rem;
}

.actions {
  display: flex;
  gap: 1rem;
  justify-content: center;
  margin-top: 2rem;
}

.save-btn,
.reset-btn {
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: all 0.3s;
}

.save-btn {
  background: var(--color-button);
  color: white;
}

.save-btn:hover {
  background: var(--color-button-hover);
}

.reset-btn {
  background: var(--color-background-mute);
  color: var(--color-text);
  border: 1px solid var(--color-border);
}

.reset-btn:hover {
  background: var(--color-background);
}
</style>
