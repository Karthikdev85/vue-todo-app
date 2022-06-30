<template>
  <button
    class="block rounded-[100vw] px-14 py-1.5 mx-auto bg-yellow-200 uppercase text-gray-800 text-lg font-semibold"
    :class="{ 'bg-blue-400': primary }"
  >
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: {
    primary: {
      type: Boolean,
      default: false,
      required: false,
    },
  },
};
</script>
