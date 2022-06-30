<template>
  <section>
    <div class="fixed inset-0 bg-black opacity-40"></div>
    <div
      class="w-[40rem] bg-[#502050] py-16 rounded-xl fixed top-1/4 left-1/2 -translate-x-1/2"
    >
      <div class="relative">
        <div
          class="absolute -top-14 right-4 font-bold cursor-pointer text-yellow-200 text-3xl"
          @click="onCloseEditForm"
        >
          <i class="fa-solid fa-close"></i>
        </div>
      </div>
      <form @submit.prevent="handleEdit">
        <div class="mb-10 w-[35rem] mx-auto">
          <input
            v-model="editTask.title"
            class="border-none outline-none w-full text-xl rounded-lg py-1.5 px-1"
            type="text"
          />
        </div>
        <button
          class="block border-none rounded-[100vw] px-14 py-1.5 mx-auto bg-yellow-200 uppercase text-gray-800 text-lg font-semibold"
        >
          Edit
        </button>
      </form>
    </div>
  </section>
</template>

<script>
export default {
  name: "EditForm",
  props: ["editTask"],
  emits: ["change-edit-state", "close-edit-form"],

  methods: {
    async handleEdit() {
      const updateOptions = {
        method: "PATCH",
        body: JSON.stringify({
          title: this.editTask.title,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      };
      this.$emit("change-edit-state");

      await fetch(
        "http://localhost:8000/todos/" + this.editTask.id,
        updateOptions
      );
    },

    onCloseEditForm() {
      this.$emit("close-edit-form");
    },
  },
};
</script>
