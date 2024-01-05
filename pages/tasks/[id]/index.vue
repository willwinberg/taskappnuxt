<script setup lang="ts">
const route = useRoute();
const taskId = computed(() => {
  if (typeof route.params.id === "string") {
    return parseInt(route.params.id);
  }
  return undefined;
});
</script>

<template>
  <div>
    <div class="px-4 sm:px-0">
      <div class="flex justify-between">
        <h3 class="text-base font-semibold leading-7 text-gray-900">
          Edit Task
        </h3>
        <NuxtLink
          to="/"
          class="text-yellow-800 hover:text-yellow-900 font-semibold underline"
        >
          Go Back
        </NuxtLink>
      </div>
      <p class="mt-1 max-w-2xl text-sm leading-6 text-gray-500">
        Update your task here
      </p>
    </div>
    <TaskForm :task-id="taskId" />
  </div>
</template>