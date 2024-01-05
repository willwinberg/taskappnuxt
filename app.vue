<script setup lang="ts">
const tasks = useState("tasks", () => [
  {
    id: 1,
    title: "First Task",
    description: "The first one",
    complete: false,
  },
  {
    id: 2,
    title: "Second Task",
    description: "The second one",
    complete: true,
  },
]);

onMounted(() => {
  const storedTasks = localStorage.getItem("task-list");
  if (storedTasks !== null) {
    const parsedTasks = JSON.parse(storedTasks);
    tasks.value = parsedTasks;
  } else {
    localStorage.setItem("task-list", JSON.stringify(tasks.value));
  }
});
</script>

<template>
  <div class="container mx-auto px-10 md:px-0">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
      <div></div>
      <div>
        <div class="mt-10">
          <NuxtPage></NuxtPage>
        </div>
      </div>
      <div></div>
    </div>
  </div>
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
</style>
