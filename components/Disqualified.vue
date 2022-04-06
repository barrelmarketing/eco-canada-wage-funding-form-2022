<template>
  <div>
    <div class="note conditional p-4 border text-center" v-html="message"></div>
  </div>
</template>

<script>
export default {
  name: "Disqualified",
  props: {
    message: {
      type: String,
      required: true,
    },
  },
};
</script>

<style>
</style>