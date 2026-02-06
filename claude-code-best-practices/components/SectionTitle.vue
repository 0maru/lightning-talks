<template>
  <div class="section-title-wrapper">
    <h1 class="section-title">{{ title }}</h1>
    <p v-if="subtitle" class="section-subtitle">{{ subtitle }}</p>
  </div>
</template>

<script setup lang="ts">
defineProps<{
  title: string
  subtitle?: string
}>()
</script>

<style scoped>
.section-title-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
  background-color: #1A1A2E;
  color: #FFFFFF;
  padding: 2rem;
}

.section-title {
  font-size: 3.5rem;
  font-weight: bold;
  margin-bottom: 1rem;
  font-family: 'Arial Black', Arial, sans-serif;
}

.section-subtitle {
  font-size: 1.5rem;
  color: #D97757;
  font-family: Calibri, Arial, sans-serif;
}
</style>
