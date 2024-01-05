<script setup lang="ts">
useState('tasks', () => [
  {
    id: 1,
    title: 'First Task',
    description: 'The first one'
  }
])
</script>

<template>
  <NuxtPage />
</template>

<style>
.page-enter-active,
.page-leave-active {
  transition: all 0.4s;
}
.page-enter-from,
.page-leave-to {
  opacity: 0;
  filter: blur(1rem);
}