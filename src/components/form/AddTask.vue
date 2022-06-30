<template>
  <section>
    <div class="fixed inset-0 bg-black opacity-40"></div>
    <div
      class="w-[40rem] bg-[#502050] py-16 rounded-xl fixed top-1/4 left-1/2 -translate-x-1/2"
    >
      <div class="relative">
        <div
          class="absolute -top-14 right-4 font-bold cursor-pointer text-yellow-200 text-3xl"
          @click="onCloseForm"
        >
          <i class="fa-solid fa-close"></i>
        </div>
      </div>
      <form @submit.prevent="handleSubmit">
        <div class="mb-10 w-[35rem] mx-auto">
          <input
            v-model="addTaskInput"
            class="border-none outline-none w-full rounded-lg py-1.5 px-1"
            type="text"
            placeholder="ADD TASK"
            required
          />
        </div>
        <!-- <button class="block rounded-[100vw] px-14 py-1.5 mx-auto bg-yellow-200 uppercase text-gray-800 text-lg font-semibold">Add</button> -->
        <v-button>Add</v-button>
      </form>
    </div>
  </section>
</template>

<script>
import VButton from "../ui/VButton.vue";
export default {
  name: "AddTask",
  emits: ["close-add-form", "new-Task"],
  components: {
    VButton,
  },
  data() {
    return {
      addTaskInput: "",
    };
  },
  methods: {
    onCloseForm() {
      this.$emit("close-add-form");
    },
    handleSubmit() {
      let addTask = this.addTaskInput;
      // console.log(addTask)
      this.$emit("new-Task", addTask);
      this.addTaskInput = "";
    },
  },
};
</script>

<style></style>
