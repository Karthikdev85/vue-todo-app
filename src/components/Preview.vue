<template>
  <section>
    <div class="fixed inset-0 bg-black opacity-40"></div>
    <div
      class="fixed w-[35rem] top-1/4 left-1/2 bg-[#8cf5ff] -translate-x-1/2 px-4 py-10 rounded-3xl"
    >
      <div class="relative mb-4">
        <button
          class="absolute -top-9 right-0 font-bold cursor-pointer text-4xl text-gray-800"
          @click="onClosePreview"
        >
          <i class="fa-solid fa-close"></i>
        </button>
      </div>
      <h2
        v-show="todoPreview.completed"
        class="text-2xl mb-4 uppercase text-center text-green-500 font-semibold"
      >
        <i class="fa-solid fa-circle-check"></i> Done
      </h2>
      <h2
        v-show="!todoPreview.completed"
        class="text-2xl mb-4 uppercase text-center text-red-500 font-bold"
      >
        Not Done
      </h2>
      <h2
        class="text-2xl text-blue-800 leading-6 text-center tracking-wide font-medium"
      >
        {{ todoPreview.title }}
      </h2>
    </div>
  </section>
</template>

<script>
export default {
  name: "Preview",
  props: ["todoPreview"],
  emits: ["close-todo"],
  methods: {
    onClosePreview() {
      this.$emit("close-todo");
    },
  },
};
</script>
