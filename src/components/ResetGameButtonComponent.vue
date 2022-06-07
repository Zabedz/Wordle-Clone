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
  name: "ResetGameButtonComponent",
  props: {
    showButton: {
      type: Boolean,
      value: false
    }
  }, methods: {
    onSubmit() {
      console.log("On reset game");
      this.$emit('reset-game');
    }
  }
}
</script>

<style scoped>

.container {
  padding: 20px;
}
</style>