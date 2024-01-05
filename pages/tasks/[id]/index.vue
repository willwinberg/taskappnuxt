<script setup lang="ts">
const route = useRoute();
</script>

<template>
  <div>
    <div class="px-4 sm:px-0">
      <h3 class="text-base font-semibold leading-7 text-gray-900">Edit Task</h3>
      <p class="mt-1 max-w-2xl text-sm leading-6 text-gray-500">
        Update your task here
      </p>
    </div>
    <TaskForm :task-id="route.params.id" />
  </div>
</template>