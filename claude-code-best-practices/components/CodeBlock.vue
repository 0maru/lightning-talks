<template>
  <div class="code-block-wrapper">
    <div v-if="title" class="code-block-title">{{ title }}</div>
    <div class="code-block-content">
      <slot />
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps<{
  title?: string
}>()
</script>

<style scoped>
.code-block-wrapper {
  margin: 1rem 0;
  border-radius: 8px;
  overflow: hidden;
}

.code-block-title {
  background-color: #1A1A2E;
  color: #D97757;
  padding: 0.5rem 1rem;
  font-family: Consolas, Monaco, 'Courier New', monospace;
  font-size: 0.9rem;
  font-weight: bold;
}

.code-block-content {
  background-color: #2D2D3F;
  color: #E8E8E8;
  padding: 1.5rem;
  font-family: Consolas, Monaco, 'Courier New', monospace;
  font-size: 0.9rem;
  line-height: 1.6;
  overflow-x: auto;
}
</style>
