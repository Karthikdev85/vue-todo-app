<template>
  <section class="container mx-auto mt-7 px-6">
    <ul v-if="todos">
      <li
        v-for="todo in todos"
        :key="todo.id"
        class="flex justify-between rounded-xl bg-[#25285d] px-2 py-1.5 items-center mb-3"
      >
        <div class="flex items-center">
          <input
            v-model="todo.completed"
            :value="todo.id"
            type="checkbox"
            @change="onCheck(todo)"
            class="rounded-full checked:bg-green-500 focus:text-green-500 hover:text-green-500 focus:ring-transparent checked:ring-transparent cursor-pointer"
          />
          <h3
            class="text-lg ml-3 tracking-wide text-gray-200"
            :class="{
              'line-through': todo.completed,
              'text-[#BDC1FF]': todo.completed,
            }"
          >
            {{ todo.title }}
          </h3>
        </div>
        <div>
          <button
            class="text-xl text-slate-400"
            :class="{ 'pointer-events-none hidden': todo.completed }"
            @click="onEdit(todo.id)"
          >
            <i class="fa-solid fa-pen"></i>
          </button>
          <button class="text-xl text-green-200 ml-4" @click="onShow(todo.id)">
            <i class="fa-regular fa-eye"></i>
          </button>
          <button class="text-xl text-red-500 ml-4" @click="onDelete(todo.id)">
            <i class="fa-solid fa-trash-can"></i>
          </button>
        </div>
      </li>
    </ul>
    <h2 v-else class="text-center text-3xl text-yellow-300 tracking-wide">
      Loading Todos...
    </h2>
    <edit-form
      :editTask="editTaskInput"
      v-show="editTaskState"
      @change-edit-state="changeState"
      @close-edit-form="closeEditForm"
    ></edit-form>
  </section>
</template>

<script>
import EditForm from "./form/EditForm.vue";
export default {
  name: "Todos",
  props: ["todos"],
  components: {
    EditForm,
  },
  emits: ["delete-todo", "show-todo"],
  data() {
    return {
      editTaskInput: "",
      editTaskState: false,
      checked: [],
    };
  },
  methods: {
    onDelete(id) {
      // console.log(id)
      this.$emit("delete-todo", id);
    },
    onShow(id) {
      this.$emit("show-todo", id);
    },
    onEdit(id) {
      // console.log(this.todos)
      this.editTaskInput = this.todos.find((todo) => todo.id === id);
      // console.log(this.editTaskInput)
      this.editTaskState = true;
    },
    changeState() {
      this.editTaskState = false;
      // console.log('change state')
    },
    closeEditForm() {
      this.editTaskState = false;
    },
    async onCheck(todo) {
      console.log(this.todos);
      // this.todos.forEach(item => {
      //     if (item.id === todo.id) {
      //         item.completed = todo.completed
      //     }
      // })

      const updateOptions = {
        method: "PATCH",
        body: JSON.stringify({
          completed: todo.completed,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      };
      await fetch("http://localhost:8000/todos/" + todo.id, updateOptions);
    },
  },
};
</script>
