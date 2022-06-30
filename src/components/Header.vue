<template>
  <header class="flex justify-center gap-10 items-center pt-5 mb-12">
    <h1
      class="text-3xl font-bold uppercase text-white cursor-pointer px-4 py-3 rounded-[100vw] bg-blue-700"
      @click="onAddTask"
    >
      New Task<i class="fa-solid fa-plus ml-2"></i>
    </h1>
    <!-- <h2 class="text-3xl font-bold uppercase cursor-pointer">Completed</h2> -->
  </header>
  <add-task
    v-show="addTaskState"
    @close-add-form="closeAddForm"
    v-bind="$attrs"
    @new-task="addNewTask"
  ></add-task>
</template>

<script>
import AddTask from "./form/AddTask.vue";

export default {
  name: "AppHeader",
  components: {
    AddTask,
  },
  data() {
    return {
      addTaskState: false,
    };
  },
  methods: {
    onAddTask() {
      this.addTaskState = !this.addTaskState;
    },
    closeAddForm() {
      this.addTaskState = false;
    },
    addNewTask(task) {
      this.addTaskState = false;
    },
  },
};
</script>

<style></style>
