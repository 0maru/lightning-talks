<template>
  <div class="comparison-table">
    <div class="comparison-column good">
      <h3 class="column-header">
        <span class="icon">✅</span>
        {{ goodTitle || 'Do' }}
      </h3>
      <ul>
        <li v-for="(item, index) in goodItems" :key="index">{{ item }}</li>
      </ul>
    </div>
    <div class="comparison-column bad">
      <h3 class="column-header">
        <span class="icon">❌</span>
        {{ badTitle || "Don't" }}
      </h3>
      <ul>
        <li v-for="(item, index) in badItems" :key="index">{{ item }}</li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps<{
  goodTitle?: string
  badTitle?: string
  goodItems: string[]
  badItems: string[]
}>()
</script>

<style scoped>
.comparison-table {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  margin: 2rem 0;
}

.comparison-column {
  border-radius: 8px;
  padding: 1.5rem;
  background-color: rgba(255, 255, 255, 0.5);
}

.comparison-column.good {
  border: 2px solid #4CAF50;
}

.comparison-column.bad {
  border: 2px solid #F44336;
}

.column-header {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 1rem;
  font-size: 1.5rem;
  font-weight: bold;
}

.icon {
  font-size: 1.8rem;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  padding: 0.5rem 0;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  line-height: 1.6;
}

li:last-child {
  border-bottom: none;
}
</style>
