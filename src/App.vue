<template>
  <app-header @new-task="addNewTask"></app-header>
  <todos
    :todos="todoLists"
    @delete-todo="tasks_delete"
    @show-todo="tasks_show"
  ></todos>
  <preview
    :todoPreview="selectedTodo"
    v-if="selectedTodo"
    @close-todo="closeTodo"
  ></preview>
</template>

<script>
import AppHeader from "./components/Header.vue";
import Todos from "./components/Todos.vue";
import Preview from "./components/Preview.vue";

export default {
  components: {
    AppHeader,
    Todos,
    Preview,
  },
  data() {
    return {
      todoLists: null,
      previewState: false,
      selectedTodo: null,
    };
  },
  methods: {
    async tasks_index() {
      const res = await fetch("http://localhost:8000/todos");

      const todos = await res.json();
      this.todoLists = todos;
    },
    tasks_delete(id) {
      if (this.todoLists) {
        this.todoLists = this.todoLists.filter((todo) => todo.id !== id);
      }

      fetch("http://localhost:8000/todos/" + id, {
        method: "DELETE",
      });
    },
    tasks_show(id) {
      this.previewState = true;
      // console.log(id)
      this.selectedTodo = this.todoLists.find((todo) => todo.id === id);
      // console.log(this.selectedTodo)
    },

    closeTodo() {
      this.previewState = !this.previewState;
      // console.log(this.previewState)
      this.selectedTodo = null;
    },
    async addNewTask(task) {
      // console.log(task)
      if (!task) return;
      //
      let newTask = {
        id: Math.floor(Math.random() * 100000),
        title: task,
        completed: false,
      };
      this.todoLists.push(newTask);
      const requestOptions = {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(newTask),
      };

      await fetch("http://localhost:8000/todos", requestOptions);
    },
  },
  mounted() {
    this.tasks_index();
  },
};
</script>
