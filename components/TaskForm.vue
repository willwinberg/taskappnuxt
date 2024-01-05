<script setup lang="ts">
const props = defineProps<{ taskId?: number }>();
const tasks: Ref<
  {
    id: number;
    title: string;
    description: string;
    complete: boolean;
  }[]
> = useState("tasks");
const task = tasks.value.find((t) => t.id === props.taskId);

const taskModel = ref({
  title: "",
  description: "",
  complete: false,
});
const valid = computed(() => taskModel.value.title.length > 0)

// isUpdate
if (task) {
  taskModel.value.title = task.title;
  taskModel.value.description = task.description;
  taskModel.value.complete = task.complete;
}

const router = useRouter();
const handleForm = () => {
  if (valid.value) {
    // isUpdate
    if (task) {
      const idx = tasks.value.findIndex((t) => t.id === props.taskId);
      tasks.value.splice(idx, 1, { ...tasks.value[idx], ...taskModel.value });
      router.push("/");
    } else {
      tasks.value = [
        { ...taskModel.value, id: tasks.value.length + 1 },
        ...tasks.value,
      ];
    }
  }
};
const deleteTask = () => {
  if (task) {
    const idx = tasks.value.findIndex((t) => t.id === props.taskId);
    tasks.value.splice(idx, 1);
    router.push("/");
  }
};
</script>

<template>
  <form @submit.prevent="handleForm">
    <div class="grid grid-cols-1 gap-4">
      <div class="mt-10 grid grid-cols-1 gap-4 sm:grid-cols-6">
        <div class="col-span-full">
          <label
            for="title"
            class="block text-sm font-medium leading-6 text-gray-900"
            >Title</label
          >
          <div
            class="flex rounded-md shadow-sm ring-1 ring-inset ring-gray-300 focus-within:ring-2 focus-within:ring-inset focus-within:ring-indigo-600 sm:max-w-md"
          >
            <input
              type="text"
              name="title"
              id="title"
              autocomplete="title"
              class="block flex-1 border-0 bg-transparent py-1.5 pl-1 text-gray-900 placeholder:text-gray-400 focus:ring-0 sm:text-sm sm:leading-6"
              placeholder="Task Title"
              v-model="taskModel.title"
            />
          </div>
        </div>
        <div class="col-span-full">
          <label
            for="description"
            class="block text-sm font-medium leading-6 text-gray-900"
            >Description</label
          >
          <textarea
            id="description"
            name="description"
            rows="3"
            class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            v-model="taskModel.description"
          ></textarea>
        </div>
        <div class="flex items-center">
          <input
            :checked="taskModel.complete"
            id="complete"
            type="checkbox"
            v-model="taskModel.complete"
            class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600"
          />
          <label for="complete" class="ms-2 text-sm font-medium text-gray-900"
            >Complete</label
          >
        </div>
        <div class="col-span-full grid grid-cols-2 gap-2">
          <div>
            <button
              :class="['text-white py-2 px-4 shadow-md w-full rounded bg-blue-400 hover:bg-blue-600 font-semibold', valid ? '' : 'bg-gray-300 px-4 py-2 rounded-md cursor-not-allowed opacity-50']"
              type="submit"
              :disabled="!valid"
            >
              {{ task ? "Update " : "Add " }} Task
            </button>
          </div>
          <div v-if="task">
            <button
              class="text-white py-2 px-4 shadow-md w-full rounded bg-red-400 hover:bg-red-600 font-semibold"
              @click="deleteTask"
            >
              Delete
            </button>
          </div>
        </div>
      </div>
    </div>
  </form>
</template>