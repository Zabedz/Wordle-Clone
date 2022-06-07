<template>
  <button
      v-if="showButton"
      v-on:click="onSubmit"
      type="button"
      class="btn btn-secondary">Reset Game
  </button>
</template>

<script>
export default {
  name: "ResetGameComponent",
  props: {
    showButton: {
      type: Boolean,
      value: false
    }
  }, methods: {
    onSubmit() {
      this.$emit('reset-game');
    }
  }
}
</script>

<style scoped>

</style>