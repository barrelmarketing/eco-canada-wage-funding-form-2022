<template>
  <div>
    <div class="card conditional p-4 text-center">
      <p v-html="text"></p>

      <a :href="link">
        <button
          v-if="link"
          type="submit"
          class="btn mt-2 w-100 btn-success rounded-0"
        >
          Begin Application
        </button>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: "Qualified",
  props: {
    text: {
      type: String,
      required: false,
    },
    link: {
      type: String,
      required: false,
    },
  },
};
</script>

<style>
</style>