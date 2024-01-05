<script setup lang="ts">
const tasks: Ref<
  {
    id: number;
    title: string;
    description: string;
    complete: boolean;
  }[]
> = useState("tasks");
</script>

<template>
  <div>
    <h1 class="text-3xl font-semibold text-gray-600 text-center">
      Test Task Tasks
    </h1>
    <div class="mt-4">
      <TaskForm />
    </div>
    <div class="mt-8 text-center">
      <div class="grid grid-cols-1 gap-3">
        <div>
          <div class="h-full" v-if="tasks.length === 0">
            <p class="text-gray-400">Congratulations! You're out of tasks.</p>
          </div>
        </div>
        <ul role="list" class="divide-y divide-gray-200">
          <li
            v-for="(task, index) in tasks"
            :key="index + task.id"
            class="flex justify-between gap-x-6 py-5 p-1"
          >
            <NuxtLink :to="`/tasks/${task.id}`" class="flex w-full">
              <div class="flex min-w-0 gap-x-4">
                <div
                  :class="[
                    'min-w-0 flex-auto',
                    task.complete ? 'line-through' : '',
                  ]"
                >
                  <p class="text-left text-sm font-semibold leading-6 text-gray-900">
                    {{ task.title }}
                  </p>
                  <p class="mt-1 truncate text-xs leading-5 text-gray-500">
                    {{ task.description }}
                  </p>
                </div>
              </div>
            </NuxtLink>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>